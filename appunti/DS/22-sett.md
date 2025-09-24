Computational systems are pervasive and are at the core of most *artificial systems*, so that every principled discipline of modelling / engineering computational systems affects the modelling and engineering of almost every sort of artificial system.

Almost every computational system of today comes equipped with ICT tech for interacting with other computational systems.

Distribution, dictated by the physical nature of artificial systems:
- Spatial
- Temporal
in terms of ==unpredictability== of *environment* where they have to work.
Time in a distributed system is different from time in a centralized system.

- Computational units
- communication channels
- data / information / knowledge
- sensors and actuators
are all distributed *spatially*

Events are distributed *temporally*, things happen but no longer in a clearly-ordered sequence
Events are scattered, and the trivial before/after temporal relation simply cannot be applied to many pairs of events.

The *Spatio-temporal* unity of systems is lost, there is no longer a notion of system *time*, or system location.
System components, at different levels of abstraction, are only partially correlated temporally and spatially.

A number of assumptions over centralized systems no longer hold.

Distributed systems are needed for geographically distributed environments, computation speedup, resource sharing and fault tolerance.

Being able to keep on providing services in spite of failures is supposed
to be one of the main benefit of distributed systems over centralized
ones

Intuitive assumption: distributed systems can be designed so that if
one component of the system fails – or, it becomes disconnected /
partitioned – other components can replace it so as to hide failures
from the outside world

---
## CAP theorem

The CAP theorem is one example of a more general trade off between
safety and liveliness in unreliable systems.

It is only possible to simultaneously provide any two of the three following properties in distributed applications:
- (C) **Consistency**: the replicated data is always consistent with each other
- (A) **Availability**: the data is highly available to the users
- (P) **Partition tolerance**: the system can continue providing services to its users even when the network partitions

We can ignore one property and maintain the other two.

the three properties are not exactly of the same sort, both technically
and conceptually
consistency and availability range over a spectrum of options, whereas
partition tolerance can somehow be seen more as an on/off feature
all of them are desirable, yet forfeiting partition tolerance is not really
an option in real-world systems
particularly with pervasive systems in the IoT era, where instability (of
the network) rules

==**CAP theorem most often forces us to choose between
availability and consistency==**

### CAP in location-based games

Location-based services use information about the position of a user / device to provide information, entertainment and security.
Since the architecture is built around the notion of millions of players
rooming physical space worldwide with their mobile devices (and,
playing through them), forfeiting partition tolerance is not an option:
- mobile devices are inherently unstable in their network connectivity
- players are inherently mobile, and so they can move in and out of network coverage
- players tend to concentrate in some areas, e.g., during special events
- scalability is a multi-level issue: not just the number of players overall, but also the number of places they can be at, and the number of players at each place

**Consistency** of the game data is essential to keep players going, these games are usually built around logically-centralized architecture using spatial replication in order to reduce user-perceived latency and improve scalability; when consistency is required (in-game transactions) players might be forced to wait for the app servers to confirm the operation.
**Usually we remove availability**.