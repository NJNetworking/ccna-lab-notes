# RSTP

---

## What is RSTP?

Rapid Spanning-tree Protocol (802.1W) is much faster at converging/adapting to network changes than 802.1D (STP). However, the industry standard 802.1w can only run STP in one instance over all VLANs.
Cisco developped their proprietary RPVST+ which combines the rapid converging/adapting speeds with per-vlan capabilities and dot1q trunking support. It can therefore loadbalance by block different ports in each VLAN.

## What is 802.1s?

802.1s, also known as Multiple Spanning Tree Protocol (MSTP), is an enhancement to the Spanning Tree Protocol (STP) that allows for multiple spanning tree instances, each with its own topology. This enables more efficient use of network resources by providing the ability to load-balance traffic across multiple VLANs.

### How 802.1s works

MSTP allows the network to define multiple regions, and each region can have a separate spanning tree instance. This is particularly useful in large networks with multiple VLANs, as it enables network administrators to optimize traffic flow and prevent bottlenecks. Instead of having a single spanning tree for all VLANs (as in 802.1D or RSTP), MSTP enables a more flexible approach by mapping VLANs to specific spanning tree instances.

#### Key Features:
* **Multiple Spanning Tree Instances**: It can support multiple instances, unlike 802.1D and 802.1w which run a single spanning tree instance.
* **Improved Load Balancing**: By mapping different VLANs to different spanning tree instances, MSTP allows for better load balancing and utilization of network paths.
* **Backward Compatibility**: MSTP is compatible with 802.1Q trunking and can coexist with legacy protocols like 802.1D.

MSTP helps overcome the limitations of 802.1D and 802.1w by offering more granular control over how traffic is handled across multiple VLANs in a network.

### Similarities & Differences

RSTP uses all the same rules and tiebreakers are normal 802.1D STP. However, root costs are updated.
* 10Mb/s = 2,000,0000
* 100Mb/s = 200,000
* 1Gb/s = 20,000
* 10 Gb/s = 2,000
* 100 Gb/s = 200
* 1 Tb/s = 20

An **extremely** important thing to note about RSTP vs STP is that in STP only the rootbridge outputs BPDU's from it's desginated ports and the other switches just flood/forward them through their open interfaces.
However, in RSTP, **ALL** switches originate and send their own BPDU's from their designated ports. Switches also age the BPDU information much more quickly: in STP a switch waits 10 hello intervals (20 sec) vs RSTP which waits 3 hellos (6 seconds)

Blocking state and disabled states are combined into one and the listening state is skipped in RSTP.
The root port role remains unchanged in RSTP and the designated port role as well.
However, the non-designated port role was divided into two seperate parts in RSTP: **alternate** & **backup**


## RSTP alternate port role

The alternate port role is a discarding port that receives a superior BPDU from another switch. Alternates essentially function as a backup to the root port.
If the root port fails, the switch can instantly move its best alternate port to forwarding in RSTP. The RSTP automatically uses backbonefast and uplinkfast (what was just explained), this is just a description of them.

## What is UplinkFast?

UplinkFast is a Cisco proprietary enhancement to 802.1D STP that provides faster convergence for access-layer switches with redundant uplinks. If the root port fails, UplinkFast enables an immediate transition to an alternate port, skipping the usual STP listening/learning states and going straight to forwarding.

### How UplinkFast works

* Typically used on access switches with multiple uplinks to distribution/core layer.
* UplinkFast keeps all potential backup root ports in a blocking state and immediately moves one to forwarding if the primary fails.
* Prevents temporary loops by sending dummy multicast frames with fake source MACs so the CAM tables in other switches update quickly.

UplinkFast is **not needed** in RSTP (802.1w) because RSTP includes this fast uplink transition natively as part of its role-based port behavior.

## What is BackboneFast?

BackboneFast is another Cisco proprietary enhancement to traditional STP (802.1D) that speeds up convergence when an indirect link failure occurs (i.e., a failure that isn’t directly connected to the detecting switch).

### How BackboneFast works

* When a switch receives an inferior BPDU (i.e., a BPDU that suggests a worse path to the root bridge), it suspects an indirect link failure.
* Normally, STP would wait the full MaxAge timer (20 seconds) before reacting.
* BackboneFast bypasses this delay by allowing the switch to ask the upstream switch if it still has a path to the root via a **Root*

## RSTP backup port role

The backup port role is a discarding port that receives a superior BPDU from another interface on the same switch. This only happens when two interfaces are connected to the same collision domain through a hub.
A hub will seldom be used in newer networks so it is not really relevant. Backup ports will switch to designated ports if the designated port goes down and is decided by the interface with the lower port ID.

### CLI commands

In Cisco iOS, to enable RSTP on a switch, you must run ```rapidpvst```. Note that RSTP is compatible with Standard STP, the interfaces connected to the STP-configured switch will adapt.

### RSTP Linktypes

There are three distinct linktypes in RSTP:
1. Edge: as we know this is portfast on the egress into an endpoint ideally, can be configured with BPDUGuard to protect unintended similar nodetypes being injected. ```spanning-tree portfast```
3. P2P/Point-to-point: a direct connection between two switches, usually on a trunk port. Usually default but you can ```spanning-tree link-type point-to-point```
4. Shared: connection to a hub, pretty much obsolete. Must operate in half-duplex mode. ```spanning-tree link-type shared```, although you will never see this.
