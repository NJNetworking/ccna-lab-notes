# Dynamic Routing Overview

---

## Connected & Local Routes

Connected otherwise known as network routes are routes that point to subnets with a CIDR lesser than /32. This is relatively straightforward.
A local route is a /32 CIDR route that is routed to a single host or interface IP. To config a static route to a host, use ip add (ip) 255.255.255.255

## Types of Dynamic Routing Protocols

* IGP (Interior Gateway Protocol) : An IGP is a routing method use to share routes inside a **SINGLE** autonomous system (AS) like a company.
* EGP/BGP (Exterior Gateway Protocol : An EGP is a routing method used to share routes between diverse ASes.

### Algorithm Types

EGP uses an algorithm called the Path-Vector Algorithm. Modern EGP is generally synonymous with BGP because that is the standard path-vector based dynamic routing protocol in use in today's networks.

* IGP'S : There are MANY IGP models with different algorithms. There are two main processes/algorithms:
* Distance Vectors : Distance-vector protocols share only information on how to access an area by sending the necessary information to each router on trip. The main types of distance-vectors are RIP (Routing Information Protocol) and EIGRP (Enhanced Interior Gateway Routing Protocol)/IGRP designed by Cisco.
* Link State: Link-state protocols share network topology throughout all routers, so routers know routes beyond their network neighbors and have a far better grasp on how the routing should occur. The main type of Link State IGP routing protocol is known as OSPF (Open Shortest Path First), but there is also another named ISIS (Intermediate System to Intermediate System).

* # Link-State vs Distance-Vector Routing Protocols

## What are Link-State Protocols?

Link-State protocols like **OSPF** and **IS-IS** build a complete map of the network inside each router's memory.  
Each router floods **LSAs (Link-State Advertisements)** to the entire area, describing its own links.

### Link-State Pros:
- Each router knows the full network topology like a detailed GPS map.
- Fast convergence during network changes.
- Makes highly efficient routing decisions.

### Link-State Cons:
- Requires more CPU and RAM resources to process and store the full topology.
- More complex to configure and maintain.

---

## What are Distance-Vector Protocols?

Distance-Vector protocols like **RIP** and **EIGRP (early versions)** only know about their directly connected neighbors.  
Routers tell their neighbors, "To reach Network X, go through me," without knowing the full path.

### Distance-Vector Pros:
- Simple and easy to configure.
- Low CPU and RAM usage.

### Distance-Vector Cons:
- Slower convergence during network changes.
- Higher risk of routing loops unless mechanisms like Split Horizon or Hold-down timers are used.
- No full knowledge of the network topology.

---

## Key Understanding

Even though Distance-Vector routers don't have full maps, redundancy still naturally forms because all routers keep advertising reachable networks to each other.  
Link-State just does it faster, smarter, and with full network awareness.

---

## Metric Numbers 

Metric numbers are ways for the routing protocol to autodetermine what the best route is WITHIN the same protocol. Each protocol has it's own metric evaluating system so it is useless to compare them if employing multiple methods.
If the same protocol has the same metric number, both routes are used and they are equally load-balanced. If one goes down or is changed, the router can adjust to use the other one at max capacity.

### Routing Protocol Metrics Summary

- **RIP**: Metric = **Hop Count** (how many routers between source and destination). Max 15 hops.

- **EIGRP**: Metric = **Bandwidth + Delay** (optionally considers Load and Reliability if configured).

- **OSPF**: Metric = **Cost** (based on interface Bandwidth, default Cost = 100,000,000 / bandwidth in bps).

- **IS-IS**: Metric = **Cost** (manually assigned per link, flexible; doesn't depend on bandwidth by default).

## Administrative Distance

Administrative Distance, otherwise known as AD, is just a arbitrary tier-list made by vendors to say what the best Dynamic routing protocol is. Local is 0, static is 1, EIGRP 90, OSPF, 110, ISIS 115, RIP 120, etc etc blablabla...
This is completely useless and arbitrary as I mentioned because you can just manually change the AD yourself. The default AD tierlist is just the generic tiers they put together for general use, you can change it yourself by doing ```ip route (ip) (subnet mask) (to ip) (NEW ADMINISTRATIVE VALUE)```.

---


  
