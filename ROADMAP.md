# Roadmap

## 0.1.0 - Initial release

The goal of this release was to take the source code written for [Building a Game Network Protocol](http://gafferongames.com/building-a-game-network-protocol/) and harden it so that it is unit tested, secure and ready to be used as a library.

Features implemented for this release:

1. Client/server connection management and timeouts
2. Secure client connect with connect token
3. Insecure connect for use in development (connection to server IP without authentication or encryption)
4. Packet encryption (requires connection via connect token)
5. Packet serialization with bitpacker
6. Can extend protocol to add new packet types
7. Unit tests for all of the functionality above
8. Integrated client/server test program that demonstrates secure connect with tokens
9. Separate client/server test programs that connect insecure connection (dev mode)
10. Network simulator support with latency, packet loss, jitter and duplicate packets
11. Socket network interface (send packets over UDP)

## 0.2.0 - Docker integration

This release extended libyojimbo to support a web backend for clients who need to securely connect to dedicated servers with 'connect tokens'. The connect token and packet encryption feature has already been implemented in 0.1.0, but it is necessary to setup a backend matchmaker and dedicated server infrastructure to show how this would be used in production. 

Docker is being used in this release as an example, not to tie libyojimbo to any particular architecture (Docker is not required to use libyojimbo) but because it is a really convenient way to distribute and run a web application across Mac, Windows and Linux. This lets me share example web backends and trust that they'll work on different platforms.

This release added support for: 

1. Running a libyojimbo server inside a container "premake5 docker"
2. A simple matcher web service in golang: "premake5 matcher"
3. An example showing how to connect a client to the server via the matcher: "premake5 connect"
4. A way to run a secure server: "premake5 secure_server"
5. A way to spawn 64 clients and connect to the server via the matcher to stress test the system: "premake5 stress"

Some pretty good progress. Stopping now and calling this release done!

## 0.3.0 - Reliable messages

Now that a demonstration of backend infrastructure is in place, the focus for this release returns to the network protocol. The goal with this release is to get the internal network protocol to a stable API and feature set.

This release will extend the internal UDP-based network protocol to support: 

1. Reliable-ordered messages (done)
2. Data blocks larger than MTU in the same reliable-ordered stream as messages (done)
3. Multiple user configurable message channels with different reliability and ordering guarantees (done)
4. Support for channels with unreliable, unordered messages and blocks (done)

Completed, but moved immediately on to documentation and finalizing the API. Expect a new 0.4.0 release shortly.

## 0.4.0 - Document and finalize API (current)

Document the API with doxygen. Review and finalize all APIs where possible. Security audit and check.

In progress. Estimate, aprox. 75% complete as of 12/26/2016.

## 0.5.0 - Snapshots

Add support for sending large messages across the unreliable-unordered channel, as required for a snapshot based system with delta encoding as used by first person shooters.

## 0.6.0 - Matchmaker

Extend matcher.go to support multiple dedicated servers reporting to it via HTTPS.

The matcher will satisfy client requests to join matches by directing clients towards servers with empty slots, sorting servers in the order of servers with the least free slots (1) to the most free slots (maxClients) so clients tend to cluster.

I may even setup a swarm of fake clients as well for stress test behavior, this could be very interesting. As a stretch goal, it would be cool to implement a web visualization showing the behavior of clients and servers in this simulated system so you can see everything that is going on.

## Feedback

Yojimbo is released on github for feedback and collaboration. Release early and release often!

Please let me know if there are any features missing from the libyojimbo roadmap that would benefit your team.

cheers

- Glenn
