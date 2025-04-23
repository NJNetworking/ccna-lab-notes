# STP

---

## Broadcast Storms

A broadcast storm is when too many broadcast packets flood the network, overwhelming devices and causing major slowdowns or outages.
Because of how switches work, in a circular array they will forever flood their ports and perhaps create infinite loops.
The TTL is a layer 3 protocol relating to TCP/IP that will drop packets after they exist for long enough, destroying loops.
However, the L2 ethernet headers do not have TTL or any type of method like this to stop infinite loops created by switches or badly configured topologies.

### MAC Address Flapping/Port Flapping

Network congestion isn't the only issue. Each time a frame arrives on a switchport, the switch uses the source MAC address field to 'learn' the MAC address and update its MAC address table.
When frames with the same source MAC Address repeatedly arrive on different interfaces, the switch is continuously updating the interface in its MAC address table, known as MAC address flapping.

## What is STP?

STP is an industry standard protocol called 802.1D. Switches from all vendors include STP by default to prevent L2 loops.
STP works by placing redundant ports in a blocking state, but these interfaces can act as backups and enter a forwarding state if the active connection fails.
Interfaces in a forwarding/active state function normally, they relay all traffic. Interfaces in a blocking state only receive BPDU messages from STP.
By selecting which ports are **forwarding** and which ports are **blocking**, STP creates a single path to/from the network. This prevents L2 loops.
There is a set proccess that STP uses to determine what interfaces should be forwarding and which ones should be blocking:
STP-enabled switches send Hello BPDU's out of all interfaces every two seconds. If another switch receives the Hello BPDU, it knows that interface is connected to another switch, because other nodetypes do not utilize STP.

### Steps

1. The switch with the lowest bridge ID is elected as the rootbridge. All ports on the rootbridge are designaed ports (forwarding state).
2. Each remaining switch will select one of its ports to be it's root port. The interface with the lowest root cost will be the root port, in a forwarding state.
   Each interface has an associated STP cost, a 10Mb/s Ethernet has a cost of 100, FastEthernet has a cost of 19, 1GB/s has a cost of 4, and 10GIG ethernet has a cost of 2.
   If the switch has multiple ports with the same root cost, the interface connected to the neighbor with the lowest bridge ID will be selected as the root port.
   The final tiebreaker is the interface connected to the interface on the neighbor switch with the lowest port ID will become the root port.
3. Each remaining collision domain will select one interface to be a designated port (forwarding). The other port will be non-designated (blocking).
   The interface on the switch with the lowest root cost will be selected, if thats a tie, then the interface on the switch with the lowest bridge ID will be designated.

