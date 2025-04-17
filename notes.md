# IPv4 Header

---

## IPv4 Packets

An IPv4 packet sits at Layer 3 in the OSI model and gets encapsulated inside an Ethernet frame. Inside the packet is an IPv4 header, which contains information that routers use to move data from the source to the destination.

Just like how Ethernet has fields like destination MAC and type, the IPv4 header has a bunch of fields of its own. Each field has a specific size and job, and they’re always in a fixed order.

---

## Version (4 bits)

This field is only 4 bits and tells you what version of IP is being used. Since we’re working with IPv4, the value here is always **4**.

---

## IHL – Internet Header Length (4 bits)

Also 4 bits, this field says how long the IPv4 header is. It’s measured in 32-bit chunks (4 bytes). The minimum is 5, which means the header is 5 × 4 = **20 bytes** long.  
If there are options added (which is rare), the IHL will be more than 5.

---

## DSCP (6 bits) and ECN (2 bits)

These two fields sit right next to each other.

**DSCP** stands for Differentiated Services Code Point. It’s 6 bits and is used to mark the packet for priority handling (used in QoS – Quality of Service).  
**ECN** is 2 bits and works with DSCP to signal network congestion without dropping packets. Not always used.

Together, they take up 1 full byte (8 bits).

---

## Total Length (2 bytes)

This is a 16-bit field that shows the total size of the entire IPv4 packet, including both the header and the actual data (payload).  
Maximum value here is **65,535 bytes** (because that’s the max of 16 bits).

---

## Identification (2 bytes)

This field helps when a packet gets **fragmented**. If a large packet is broken into smaller chunks, this ID is the same for all of them, so the receiving device knows how to put them back together.

---

## Flags (3 bits)

There are only 3 bits here, but they do important things.

One bit is reserved.  
The second bit is the **DF** bit (Don’t Fragment). If this is set, routers aren’t allowed to chop up the packet.  
The third is the **MF** bit (More Fragments). If this is set, it means there are still more pieces of the packet after this one.

---

## Fragment Offset (13 bits)

Used **only when fragmentation happens**. This 13-bit field tells the receiver where this fragment belongs in the original packet, measured in 8-byte blocks.  
If a packet isn’t fragmented, this will just be 0.

---

## TTL – Time To Live (1 byte)

This field prevents packets from looping endlessly around the network. It’s 8 bits long (1 byte).  
Each time the packet hits a router, the TTL is reduced by 1. If it hits 0, the packet is dropped.

---

## Protocol (1 byte)

This tells you what Layer 4 protocol is inside the packet. Some common values:

* **6** = TCP  
* **17** = UDP  
* **1** = ICMP  

It’s just a single byte (8 bits), but it’s critical for the receiving host to know how to handle the payload.

---

## Header Checksum (2 bytes)

This is a **checksum** only for the header itself. It’s used by routers and devices to check if the IPv4 header was damaged in transit.  
It doesn’t check the payload — just the header.

---

## Source IP Address (4 bytes)

This is where the packet is coming from. A full 32-bit (4-byte) IPv4 address, like `192.168.1.10`.

---

## Destination IP Address (4 bytes)

This is where the packet is going. Same as source — 32 bits or 4 bytes long.

---

## Options (Variable length, optional)

This field only appears if the IHL is greater than 5. It’s rarely used, but it can carry things like security labels, timestamps, or record route data.  
If options are included, **padding** is used to make sure the header still ends on a 32-bit boundary.

---
