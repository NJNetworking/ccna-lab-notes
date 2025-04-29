# FHRP's

---

## What is a FHRP?

A virtual IP is configured on two routers, and a VMAC is generated for the VIP.

An active router and a standby router are elected, the terms for these may vary but they accomplish the same functions.

Endpoints in the network are configured to use the VIP as their default gateway.

The active router replies to ARP requests by using the VMAC address, so traffic destined for other networks will be sent to it.

If the active router fails, the standby becomes the next active router. The new active router will send gratuitous ARP messages so that the switches will update their MAC address table. It will now function like the default gateway.

If the old router comes back online it will, by default, not take back its active role. It will become the new standby router. This can be changed however.

### Major FHRP types

1. HSRP (Hot Standby Router Protocol)

   The HSRP is a Cisco proprietary FHRP application protocol. In HSRP, an active and standby router are elected. There are two versions, version two adds IPv6 support and supports more groups.
   * Multicast IPv4 address: v1 = 224.0.0.2, v2 = 224.0.0.102
   * Virtual MAC address: v1 = 0000.0c07.acXX (XX = HSRP group number), v2 = 0000.0c9f.fXXX (XXX = HSRP group number)

2. VRRP (Virtual Router Redundancy Protocol)

   The VRRP is a Open standard runnable by Cisco. They are almost identical with a few differences. Instead of active and standby, a master and backup router are elected, just the names are altered however, its the same.
   * Multicast IPv4 address: 224.0.0.18
   * VMAC address: 0000.5e00.01XX (XX = VRRP group number)

3. GLBP (Gateway Load Balancing Protocol)

   GLBP is again Cisco proprietary FHRP application. It load balances among multiple routers in a *single subnet*.

   In GLBP, a single AVG (Active Virtual Gateway) is elected for the subnet, then up to 4 AVFs (Active Virtual Forwarders) are assigned by the AVG.

   Each AVF acts as the default gateway for a portion of the hosts in the subnet.

   * Multicast IPv4 Address: 224.0.0.102
   * VMAC format: 0007.b400.XXYY (XX = GLBP group number, YY = AVF number)

## CLI commands for HSRP Configuration

- `standby [group] ip [virtual-ip]`  
  Sets the virtual IP address for the HSRP group. All routers in the group share this IP (e.g., `standby 1 ip 192.168.1.1`).

- `standby [group] priority [value]`  
  Sets the priority for the router (default is 100). Higher priority = more likely to be active router.

- `standby [group] preempt`  
  Allows the router to take over as active if it has higher priority and rejoins the network.

- `standby [group] authentication [string]`  
  Optional password to authenticate HSRP messages between routers.

- `standby [group] timers [hello] [hold]`  
  Sets how often hello packets are sent and how long to wait before declaring the active router is down.
