# p2:panda_face: Ideas

These use cases describe how we imagine p2panda to be used. This does not preclude other use cases – on the contrary, our design decisions should allow for flexibility and hackability.

## Decentralization

p2panda just runs on your own computer, which makes it interesting for different sorts of contexts:

- Spontaneous setups since no server setup is required. Can be realized by everyone, even without technical knowledge (a client has to be downloaded or hosted / accessed on a website somewhere though).
- Use p2panda in places where there is no internet access.
- Use short-distance protocols like Bluetooth to talk to each other / exchange / replicate data.
- Ephemeral data / setups, they might disappear as soon as every computer is shut off.

## Users

p2panda generates a unique cryptographic key-pair on every first start, this is enough to make sure that every message the key owner sends can be verified and connected to it (if someone changed the message afterwards it will fail). This is a rather radical setup as it does not distinct between a "admin", "participant" and a "visitor". Everyone has the same permissions to interact with p2panda. The only things you can control individually are what you share with others on p2panda (block malicious peers) and how you authorize your resources. A client should implement good UX / UI to build "trust" into other peers (see below for some ideas).

## Clients

p2panda is strictly speaking just a definition of data schemas which can be distributed and interpreted by any kind of client which follows this definition. However, the use, interface and purpose on how p2panda is used is not further defined, which gives some freedom in what a client actually could be. Examples:

- A festival tool which displays a calendar and gives the user the possibility to create own events, manage and share resources with others (this is the [BLATT 3000](https://hoffnung3000.de) use-case).
- A simple widget one can display on a page / dashboard / projector to show the next events.
- A client which holds many resources owned by a collective / organization, it could be used as a more "professional" tool to overview where items are right now and where they are being used. Also one could think of a special procedure to authorize the use of items (for example by majority vote).
- An independent piece of software which does not require a user interface as it acts upon p2panda autonomously. It could scrape other platforms / protocols (Twitter feeds, RSS feeds, Facebook events) and remix them, or it could be an AI bot curating the festival, actually enacting upon a real infrastructure of places, people and resources.
- An archiving client which gathers the data it gets and re-configures / displays / exports it in some other feed in some way for documentation / presentation. It could be connected to Dat and IPFS to automatically store the data there.
- A client which organizes random meetings between users and assigns resources to these meeting events (random meeting bot).
- Have a Zine client which prints a Zine / generates a pdf file every 10 minutes based on what it currently "sees" in the p2panda universe.

Using p2p protocol raises many UI/UX questions, here are a few ideas on how to communicate some "p2p-quirks" to the users:

- Indicate the current "health" status of yourself, how much do you "replicate" your data with others right now / how connected are you with others? This is an important indicator to make users understand about their impact on the "reach ability" by others. Since everyone serves their own data it comes with a larger responsibility to distribute it yourself / make yourself available.
- Indicate the "last active" status of others (not necessarily in time). This can be an indicator on how reliable a peer is.
- Show to everyone (not only to the organizer) how much an event is confirmed, so you can get a feeling on how realistic it is that this event will take place. This is realized by showing the confirmed state of all the requested event resources. Eg. "The event is 75% confirmed".

![UX ideas](https://raw.githubusercontent.com/p2panda/design-document/master/images/client.jpg)

![UX ideas](https://raw.githubusercontent.com/p2panda/design-document/master/images/client-pro.jpg)

## Resources

Since a resource is just defined by an arbitrary title, description and image, it can be anything. Examples and possible use-cases could be:

- A festival token you only get authorized to use when you checked in at an official festival deck. Other users will see if an event has this festival token and can "trust" this event as it got "officially" confirmed. Obviously, this is a more traditional use-case of p2panda.
- Money can be a resource (for example in 1, 10 or 100 Euro quantities) which can be requested by anyone to realize their events. A special client holding these resources could have an authorization mechanism which distributes the funds accordingly.
- Any URL, virtual address is a resource, so events can take place in shared documents, live streams, chats etc. Also external programs can be addressed this way, for example Dat / IPFS / SSB hashes.
- A 3D position could be a resource, which could be used for events taking place in [virtual spaces](https://github.com/RangerMauve/local-first-cyberspace), like a computer game / VR world or any other 3D environment. One could think of a sound installation where users place sound sources and 3D objects on a X/Y/Z axis.

## Authorization

Authorization is simply a client broadcasting a signed message if a certain resource request was confirmed or rejected. The requesting peer will eventually be informed about this message during replication. Why this confirmation or rejection message was sent is not further defined and is up to the peers implementation. Examples:

- An straightforward way would be to use a "first come, first serve" logic, "random" or a manual user feedback, asking the user to click "confirm" or "reject" in an interface.
- A movie has to be watched first, a game played, a question asked .. time and duration are interesting "validators".
- A group of people has to vote first.
- An AI decides based on a trained neural network how to decide.

## Festival ideas

- p2panda can be used to "hijack" other festivals. Groups can enter other festivals and register their infrastructure / events etc. to enact p2panda upon it.
- Have sub-curators during a defined (festival) time-frame. Do a "call for festivals" or a "call for collectives", curating independently but interdependently their festival logic within p2panda. They can be based on competently different clients / plugins / aesthetics / ideas / philosophies, take place in different parts of the world, but still be parse-able by others as long as they follow the p2panda data structure.
- Have a "call for AIs" and ask for teams who want to contribute bot curators.

## Philosophies

- **Offline first:** Data can directly be created as no server has to be requested first. This is interesting for local and global dynamics: A group might be active with p2panda for one week doing something without internet, go back into the city and start to sync with the global space again.
- **Energy saving:** A bunch of laptops or raspberry PIs needs much less electricity than a server farm.
- **Chaos:** One might get surprised by who is entering the festival as there are no predefined entrance thresholds like ticket-sales etc. (if you need a place for yourself you could still create a p2panda with a different discovery key).
- **Constant belonging / sudden bursts:** p2panda is basically running "all the time". A "time-frame" is rather a social agreement happening outside of the technical context. Activities on p2panda can happen globally or locally focussed at any time.
- **Local first / small first:** p2panda should encourage people to make festivals / setups for their local communities rather than flying people in (prefer video / audio streaming). Through p2panda it is still possible to build links between international groups / festivals / collectives as they are part of the same protocol.
- **Plurality:** p2panda is decentralized and therefore not consistent by nature, meaning that every peer sees a different part and state of it.
- **Anonymity:** p2panda only needs the cryptographic key-pair to verify peers and therefore does not need any authentication through email address etc. - technically speaking its not anonymous (you are still being connected to your IP address for example), but even this can be solved with the SSB Tor interface.
- **Recycling:** The data is not necessarily owned by anyone, it (for example venues in your city) could be reused / recycled / forked to organize something else in the future.
- **Resilience:** Festival servers might be shut off one day, but since the data is stored on everyones machine it automatically got "backed up" by many (dynamic archive).