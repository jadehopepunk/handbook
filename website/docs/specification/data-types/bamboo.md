---
id: bamboo
title: Bamboo
---

_Requirements in this section refer only to how p2panda specifies use of bamboo._

:::caution Requirement BA1

p2panda uses [Bamboo][bamboo_spec] with Ed25519 (Digital Signature Algorithm) and YASMF (Multihash) to encode and secure data.

:::

- p2panda is built on top of the [Bamboo][bamboo_spec] data type.
  - This handbook doesn't repeat everything that's in the Bamboo specification, so it might be helpful to have a look at that (it's not too long).
- Bamboo is an append-only log data type that ensures security and authenticity of arbitrary data in order to share it in a decentralised and trustless setting.
  - Bamboo organises data by _author_.
  - Every author can have many [_logs_](#logs), each of which contains many _entries_.
  - Entries contain p2panda data that we want to publish.
- The following sections explain how these concepts from bamboo are used in p2panda.

```
struct Entry {
  /// PublicKey of this entry.
  public_key: Bytes(32),

  /// Used log for this entry.
  log_id: U64,

  /// Sequence number of this entry.
  seq_num: NonZeroU64,

  /// Hash of skiplink Bamboo entry.
  skiplink?: Bytes(34),

  /// Hash of previous Bamboo entry.
  backlink?: Bytes(34),

  /// Byte size of payload.
  payload_size: U64,

  /// Hash of payload.
  payload_hash: Bytes(34),

  /// Ed25519 signature of entry.
  signature: Bytes(64),
}
```

### Hashing

:::caution Requirement BA2

[\_Yet Another Smol Multi-Hash (YASMF)][yasmf] MUST be used to produce hashes for Bamboo entries and payloads.

:::

- The original Bamboo requires [_YAMF-hashes_][yamf] to verify the integrity of entries and logs.
  - YAMF is a multiformat hash that only adds new hashing algorithms when previous ones have been discovered to be broken.
- However, p2panda uses bamboo with [_YASMF_-hashes][yasmf].
  - YASMF has the additional requirement that hashing algorithms should be chosen that produce shorter hashes (256 bits).
  - At the time of writing, YASMF only contains the BLAKE3 hash, which therefore is the hash function used throughout p2panda. It is fast, safe, and produces hashes that are just 32 bytes long.

### Encoding

:::caution Requirement BA3

Bamboo entries MUST be encoded using hexadecimal encoding when being transported through the Client API via GraphQL.

:::

p2panda prefers hex-encoding to make it nicer for humans to look at the data.

### Authors

:::info Definition: Author

An p2panda author is a human or bot who publishes data using p2panda. Authors may have more than one key pair.

:::

- Data published using Bamboo always belongs to the public key that signed it, this key is called _author_ in Bamboo.
- People and bots who use p2panda can have access to more than one key pair, which is why we don't call public keys _author_, as Bamboo does, we call them _public key_.
  - Data in p2panda belongs to the _key pair_ that signed it.
  - p2panda uses Ed25519 as the Bamboo signature scheme.
  - p2panda users may have more than one key because every device and client uses an additional key.
- Have a look at the [key pairs][key_pairs] section of this handbook for more detailed information on this topic.

### Logs

- When a key pair publishes data it is assigned to a Bamboo _log_, which is identified by an integer number.
  - Every key pair has 2^64 logs available to them.
- In p2panda every Bamboo log is used to collect a key pair's contributions to one [document][documents].
- Every log contains up to 2^64 - 1 entries.

:::caution Requirement BA4

Bamboo log ids for any public key MUST increment monotonically by one.

:::

### Entries

- p2panda uses Bamboo entries to record changes of data while giving us cool features like partial replication, cryptographic integrity and authenticity.
  - Every atomic change is recorded inside an entry.
  - We call these changes _operations_.
- Have a look at the [operations][operations] section of this handbook for more detailed information on this topic.

### End of log flag

Currently p2panda doesn't reserve a special use for the end of log flag. This may change in future versions.

[bamboo_spec]: https://github.com/AljoschaMeyer/bamboo
[documents]: /specification/data-types/documents
[key_pairs]: /specification/data-types/key-pairs
[operations]: /specification/data-types/operations
[yamf]: https://github.com/AljoschaMeyer/yamf-hash
[yasmf]: https://github.com/bamboo-rs/yasmf-hash-spec
