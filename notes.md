# RIP & EIGRP

---

## RIP (Routing Information Protocol)

RIP is an industry standard dynamic routing protocol that is a distance-vector IGP. It only uses hop count as its metric. One router = one hop. This is rudimentary and seen as one of the worse dynamic protocols because it doesn't take into account bandwidth of connections like OSPF or its other distance vector compatriot EIGRP.
The maximum hop count within RIP is 15 (anything beyond that is considered unreachable).

---

RIP has three versions 
* RIPv1 & RIPv2 which are both for IPv4
* RIPv3 which is for IPv6 addresses

RIP uses two distinct message types
- Request: To ask the RIP-enabled neighbor routers to send their routing tables
- Response: To send the local router's routing table to neighboring routers, which happens naturally every 30 seconds.

RIPv1 is a very old protocol that should not be used and only advertises classful addressing so doesn't support VLSM or CIDR. It is basically useless for that reason.

--

RIPv2 doesn't have to be classful and supports VLSM and CIDR and includes subnet mask information in its advertisements. RIPv2 messages are not broadcast but multicast to 224.0.0.9 in the D range.

### CLI Commands to Enable RIP

* ```router rip``` is the command to enter the modification mode for the RIprotocol.
* ```version 2``` specifies the version of RIP, it's version 1 by default which we do not want so either do version 2 for IPv4 or version 3 for IPv6
* ```no auto-summary``` should always be used to remove the automatic summarization of classful addresses which we definitely do not want provided we use VSLM and CIDR subnetting.
* The `network` command in RIP tells the router:

- Which interfaces should **run RIP** (send/receive RIP updates).
- Which networks should be **advertised** to RIP neighbors.

If an interface's IP address matches the `network` statement of the classful input, RIP is activated on that interface.

Without any `network` commands, RIP will not send or receive any routing updates.

* ```passive-interface (int)``` tells the router to stop sending out RIP advertisements out of a specified interface.
* ```default-information originate``` tells all RIP interfaces to advertise the default gateway of the router to all the other routing-tables in the network.
* ```maximum-paths (path#)``` shows how many paths are allowed concurrently, from 1 to 32 but defaulted at 4 for ECMP load-balancing between similar routes.

## EIGRP (Enhanced Interior Gateway Routing Protocol)

EIGRP is an enhanced or improved version of IGRP and it was Cisco proprietary but released publically but no one wants it on their equipment so its still kinda Cisco-only protocol.
It is considered a hybrid distance vector routing protocol, improving on the areas that it's fellow DVP RIP dropped the ball on. It is much faster than RIP to react to changes within the network.
It doesn't have the 15 hop count limit of RIP so it may support very large networks and sends messages using the multicast address 224.0.0.10.
EIGRP is the **ONLY** IGP that can load balance and use multiple paths that do not share the same metric.

### CLI Commands to Enable EIGRP

* ```router eigrp (#)``` is the command to enter the modification mode for the EIGRP followed by the AS number, which must match between routers otherwise they will not form an adjacency and share route information.
* ```no auto-summary``` does the exact same thing as in RIP, advertises classful networks instead of the network configured on its interfaces.
* ```network (ip)``` command in EIGRP uses the IP address range with a network mask:
* A wildcard mask is used to match a range of IP addresses by telling the router which parts of the address must match exactly and which parts can vary.
* In the wildcard, a 0 means the corresponding bit must match exactly, while a 1 means the bit can be anything. In EIGRP, when you type the network command followed by an IP address and a wildcard mask, you are telling the router which interfaces should participate in EIGRP by matching their IP addresses to the network and wildcard you specified.
* It makes it easier to include entire subnets or ranges without manually adding each IP.

#### EIGRP Metric Calculation

EIGRP calculates its metric using two factors:
- The slowest bandwidth along the entire path.
- The sum of the delays across all links in the path.

The formula is: metric = (10^7 / slowest bandwidth in kbps) + sum of delays (in tens of microseconds)

###### Example:

Suppose we have a path across 3 links:
- Link 1: 100 Mbps, 1000 microseconds delay
- Link 2: 10 Mbps, 2000 microseconds delay
- Link 3: 100 Mbps, 1000 microseconds delay

Step 1: Find the slowest bandwidth.  
Slowest = 10 Mbps = 10000 kbps

Step 2: Add all the delays.  
Total delay = 1000 + 2000 + 1000 = 4000 microseconds  
Converted to tens of microseconds: 4000 ÷ 10 = 400

Step 3: Plug into the formula.
metric = (10^7 / 10000) + 400  
metric = 1000 + 400  
metric = 1400

So the EIGRP metric for that path would be 1400.

---

### EIGRP Router ID

The EIGRP Router ID is a unique 32-bit value used to identify a router in an EIGRP autonomous system.

#### How the Router ID is Chosen
1. **Manual Configuration**: 
   - Use `eigrp router-id [ID]` to manually set the router ID.
2. **Highest Loopback Interface IP**: 
   - If no manual ID is set, the router ID is the highest IP address of any configured loopback interface.
3. **Highest Active Physical Interface IP**: 
   - If no loopback interfaces are configured, the router ID is the highest IP address of any active physical interface.

##### Example
- **Loopback0**: 10.0.0.1
- **GigabitEthernet0/1**: 192.168.1.1

  Router ID: 10.0.0.1 (highest loopback IP)

###### Importance
- The router ID is used to identify the router in EIGRP routing tables and messages.
- It's essential for establishing and maintaining EIGRP neighbor relationships.

---



  
