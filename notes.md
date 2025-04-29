# OSPF

---

## What is OSPF?

The OSPF (Open Shortest Path First) protocol uses the ShortestPathFirst algorithm by Esdger Dijkstra, hence why OSPF is sometimes referred to as Dijkstra's Algorithm.
There are three versions of OSPF
* OSPv1 (1989): old and obsolete
* OSPv2 (1998): used for IPv4
* OSPv3 (2008): developped for IPv6 (or IPv4)

--

OSPF-enabled routers store information about the network is LSAs (Link-State Advertisements), which are organized in a structure called the LSDB (Link-State Database).
Routers will flood LSA's until all routers in the OSPF area develop the same LSDB. Each LSA has an aging timer, which is 30 minutes by default.
Here is the process for sharing LSAs and building LSBDs in OSPF
* Step 1: Become neighbors with adjacent routers in the same segment.
* Step 2: Exchange LSA's with neighbor routers which will flood throughout the entire OSPF area.
* Step 3: Each router independently calculates it's best routes to each destination and inserts them into their routing-table.

## OSPF Areas

OSPF uses *areas* to divide up the network, however small networks can be single-area without effects on performance. Areas in larger networks can have negative effects such as:
* longer times for SPF to calculate routes
* exponentially more CPU power to make calculations
* each router sharing 1 giant LSDB takes up more memory on the routers
* rerunning of SPF through LSAs every single time a change is made on the network
  
An **Area** is a set of routers and links that share the same LSDB. The **backbone** is a special area that all other areas must converge to. Routers with all interfaces in one single area are called **internal routers**.

Routers with interfaces in multiple areas are called **ABR** (Area Border Routers) because they conjoin areas. ABR's maintain a seperate LSDB for every area they are connected to, so to prevent overburdening of the router it is recommended you have a ABR connected to only 2 areas concurrently.

**Interarea routes** are routes that use routers to access a destination in another OSPF area, and **Intraarea routes** are the opposite, routes that are within the same OSPF area.
OSPF areas should be contiguous otherwise OSPF will not function properly.

All OSPF areas should have one ABR connected to the backbone at all times, otherwise the network design will not work. OSPF interfaces in the same subnet should be in the same area.

## CLI Commands related to OSPF

* ```router ospf (process id)``` activates OSPF on a router.
* ```network (ip) (wildcard mask (area #)``` tells OSPF to look for any interfaces with an IP address contained in the range, activate OSPF dynamic routing on the specified area, and the router will then try to become OSPF neighbords with other OSPF enabled routers next to it.
* ```passive-interface (inter)``` stops sending OSPF hello's out of the interfaces but continues sending LSA's informing its neighbors about the subnets configured on that interface.
* ```ip route 0.0.0.0 0.0.0.0 (ip)``` adds the default gateway advertisement to all routers over dynamic routing through OSPF creating a new LSA and flooding it.

### ASBR (Autonomous System Boundary Router)

An ASBR is a OSPF router that connects the OSPF network to an external network. OSPF doesn't support unequal cost load-balancing but does support ECMP load-balancing.

---

## OSPF Cost

OSPF's metric is called cost, automatically calculated based on the bandwidth of the interface.

The OSPF cost is calculated by dividing a **reference bandwidth** value by the interface's bandwidth. The default reference is 100 Mb/s. 

This is why we change the reference bandwidth with this command ```auto-cost reference-bandwidth (megabits-per-second)```.
The OSPF cost to a destination is the total cost of all outgoing interfaces costs. Loopback interfaces have a cost of 1.

The `speed (kilobits)` command in OSPF is used to manually set the interface bandwidth in kilobits per second. This value affects OSPF's metric calculation, specifically the cost, which is inversely proportional to the bandwidth. By adjusting this value, you can influence OSPF's path selection.

---

## OSPF Neighbors

Making sure that routers become OSPF neighbors is the main task in OSPF. When OSPF is activated on an interface, the router starts sending OSPF hello's out of the interfaces at regular intervals determined by the hello timer which is 10 seconds by default.
Hello messages are multicast to 224.0.0.5 class d range address. OSPF messages are encapsulated in an IP Header with a value of 89 in the Protocol field to specify that it is an OSPF hello.

## OSPF Neighbor Formation and State Process

### 1. OSPF Activation
- You activate OSPF on an interface by entering router configuration mode (`router ospf <process-id>`) and using the `network` command to match the interface IP and area.
- This tells the router to start looking for OSPF neighbors on that interface.

### 2. Down State
- This is the initial state before any hello packets are heard from other routers.
- The router just waits.

### 3. Init State
- The router has received a Hello packet from another router.
- However, the receiving router has not yet seen itself listed in the neighbor’s Hello packet.
- It's a one-way communication at this point.

### 4. 2-Way State
- Routers see their own Router ID listed in the neighbor's Hello packet.
- They agree to form a neighbor relationship.
- If the network type is multi-access (like Ethernet), DR (Designated Router) and BDR (Backup Designated Router) election happens at this stage.

### 5. DR/BDR Election (if needed)
- In multi-access networks (like LANs), routers elect a DR and a BDR.
- DR manages LSAs for the segment to reduce OSPF overhead.
- BDR takes over if DR fails.

### 6. ExStart State
- After DR/BDR election, routers determine which one will start exchanging link-state information.
- The router with the higher Router ID becomes the master; the other is the slave.

### 7. Exchange State
- Routers exchange DBD (Database Description) packets containing summaries of their LSDB (Link-State Database).
- They figure out if they have any missing LSAs from each other.

### 8. Loading State
- Routers request any missing LSAs using LSR (Link-State Requests).
- They receive LSA updates until their LSDBs are fully synchronized.

### 9. Full State
- Neighbors have fully synchronized their LSDBs.
- Routing can now happen properly based on the complete topology.

---

### Loopback interfaces

A loopback interface is a virtual interface inside the router. It is always by default up/up unless you admin shutdown. It is not dependant on the hardware interfaces and is a permanent IP address associated with a router.

## OSPF Network Types

There are three main OSPF network types:
* Broadcast

Enabled by default on both Ethernet and FDDI (Fiber Distributed Data Interfaces) interfaces.

* P2P

 Enabled by default on both PPP (Point-to-Point Protocol) and HDLC (High Data Link Control) interfaces.
 
* Non-Broadcast

 Enabled by default on Frame Relay and X.25 interfaces.

## OSPF Network Broadcast Type

* Routers dynamically discover neighbors by sending and listening for OSPF hello messages using the multicast address 224.0.0.5
* A DR (designated router) and BDR (backup designated router) must be elected on each subnet
* Routers that aren't the DR or the BDR become the DROther

##### The DR/BDR election order of priority:
1. Highest OSPF interface
2. Highest OSPF router ID
(note, the interface priority is by default 1 on all interfaces)

So basically DR/BDR is by default just a arbitrary assignment in each subnet for which router will do the heavy lifting.

## OSPF Point-To-Point Network Type

* A DR and BDR are not elected and routers will still form adjacencies
* Routers dynamically discover neighbors by sending or listening for OSPF hellos over multicast address 224.0.0.5
* PPP or HDLC encapsulations are used for p2p connections. These encapsulations are ONLY used for serial connections between routers in networking infrastructure
* One side functions as the DCE and the other as the DTE. The DTE needs to know the clock speed so the DCE must specify the clock speed in bits per second

## OSPF Neighbor Requirements

* The area number must match
* The interfaces must be in the same subnet
* OSPF process must not be **shutdown**
* OSPF Router IDs/loopbacks must be unique
* Hello & Dead timers must match between routers
* Authentication settings/passwords must match
* IP MTU settings must match up
* OSPF configured network type must match

### OSPF LSA Types

There are in total 11 LSA types shared in OSPF depending on the setup. There are only 3 main important ones:

- Type 1 (Router LSA)

Every OSPF router generates this type of LSA, it identifies the router using it's router ID. It lists networks attached to the router's OSPF-activated interfaces.

- Type 2 (Network LSA)

Generated by the DR of each multi-access/broadcast network. Lists the overarching routrs all linked back to the DR.

- Type 3 (AS-external LSA)

Advertises and propagates default gateway, generated by ASBR to describe the way out to an external router.











