# Lab 29 – HSRP and Redundancy Failover #

## Summary ##

In this HSRP-focused lab, I set up **redundant routing with failover** between two routers using **HSRPv2**. The goal was to ensure that PC1 and PC2 could still reach the external server (8.8.8.8) through a shared virtual gateway, even if the primary router went offline. The 8.8.8.8 address was actually just a loopback on the external router, but it simulated an internet-facing IP.

---

## What I Did ##

- **Initial Test**:
  - Pinged **8.8.8.8** from PC1/PC2 — verified reachability using current default gateway settings.
  
- **HSRP Configuration**:
  - Configured **HSRPv2** on the interior `G0/0` interfaces of both **R1** and **R2**.
  - Set the **virtual IP (VIP)** to act as the shared default gateway between them.
  - Raised **R1’s priority** (above default) to make it the **active router**.
  - Lowered **R2’s priority** (below default) to make it **standby**.
  - Enabled **preemption** so that **R1 can regain active status** if it comes back online after a failure.

- **Client-Side Fix**:
  - Updated the **default gateway on PC1 and PC2** to point to the new **VIP** instead of a physical IP.
  - Verified ARP tables on the PCs — confirmed the MAC address mapped to the VIP was coming from **R1**.

- **Failover Simulation**:
  - Ran `copy running-config startup-config` on both routers.
  - Simulated a failure by manually powering down **R1** in Packet Tracer.
  - Re-tested connectivity in simulation mode — traffic now passed through **R2**, which became the new active router.

- **Restoration Test**:
  - Turned **R1** back on and waited a bit.
  - Because preemption was enabled, **R1** reclaimed its role as the **active HSRP router**.
  - Pings to 8.8.8.8 resumed flowing through R1 as expected.

---

## Network Overview ##

This lab used **Hot Standby Router Protocol version 2** to implement **gateway redundancy** on a LAN segment:

- Both **R1 and R2** shared a **VIP** used by internal clients.
- **R1 served as the active router**, while **R2 remained on standby**, ready to take over instantly on failure.
- Failover was smooth — **no reconfiguration needed on the clients**.
- Once R1 returned, it resumed control thanks to **preemptive priority** settings.

This setup keeps internal traffic flowing to external networks without interruption, even during router outages.

---

## Screenshots ##

![Lab Screenshot 1](lab27-1.png)  
![Lab Screenshot 2](lab27-2.png)

---

## Wrap-up ##

This was a great introduction to **HSRP failover and redundancy concepts**. I liked how simple it was to swap control between routers without touching the PCs at all — just config the routers once and let the protocol do its job. Simulating hardware failure and verifying traffic paths showed exactly why HSRP matters in real-world networks.
