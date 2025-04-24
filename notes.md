# EtherChannel

---

## What is EtherChannel?

Etherchannel is a regroupment of interfaces that behave as a single link otherwise known as a logical interface, it gives us redundancy AND increased bandwidth.
STP sees the four real interfaces as one logical interface and won't set it to blocking as it shouldn't form a L2 loop. Other names for a EtherChannel include PortChannel or LAG (Link Aggregation Group).
For the ports to succesfully form into one logical interface, they must ALL have the same speed, duplex setting, mode, allowed VLANs, native VLANs...

### EtherChannel Load Balancing

EtherChannel loadbalances based on flows, which is a communication between two nodes in the network. Frames in the same flow will be forwarded using the same physical interface.
The calculation that is done to determine which interface takes into account a few inputs:
* Source MAC Address
* Dest MAC Address
* Both MAC
* Source IPv4
* Dest IPv4
* Both IPv4

## EtherChannel config in CLI

```show etherchannel load-balance``` is the command to see relevant configuration on the etherchannel interface load-balancing.
```port-channel load-balance (method``` changes the method for load balancing through Etherchannel.
```channel-group (virtual interface #) mode auto/desirable (PAgP) on (static) passive/active (LACP)``` use to change the Etherchannel method.
```do show etherchannel summary``` shows Etherchannels with legends and information.

## Etherchannel Methods

* PAgP (PORT AGGREGATION PROTOCOL): This is a Cisco propriety protocol only that only functions on Cisco switches. It dynamically negotiates creation of Etherchannels between two switches.
* LACP (Link Aggregation Control Protocol): Industry standard, 802.3ad, does the exact same thing as PAgP but with different criteria.
* Static Etherchannel: manual configuration of a static Etherchannel connection, discouraged as there is no protocol making sure the load-balancing is maintained after failure.

Up to 8 interfaces can be formed into one logical Etherchannel interface, however in LACP this is 16 but 8 are in standby and therefore only present to take over in case of failure.

# What is Layer 3 EtherChannel?

Layer 3 EtherChannel is a method of bundling multiple physical links between devices into a single logical Layer 3 interface for routing purposes. Unlike traditional Layer 2 EtherChannel, which works like a switchport (Access or Trunk), Layer 3 EtherChannel works as a routed port and participates directly in the routing process (no MAC address learning or STP).

## Key Differences from L2 EtherChannel

- No switchport configuration (use `no switchport`)
- Functions as a routed interface, not a bridging interface
- Can have an IP address assigned directly
- Used between routers, or between switch SVIs and routed interfaces
- Does not participate in STP (Spanning Tree)

## Configuration Overview

1. Create the port-channel interface
2. Convert physical interfaces to routed mode (`no switchport`)
3. Assign the interfaces to a port-channel group
4. Configure an IP address on the port-channel interface

## Example

```bash
interface range g0/1 - 2
  no switchport
  channel-group 1 mode active

interface port-channel 1
  no switchport
  ip address 10.1.1.1 255.255.255.0

---
