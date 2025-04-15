# Interfaces & Cables

---

## Switch Interfaces ##

Switches tend to have loads of interfaces to connect end-hosts like PC's and servers to. The shape of the interfaces on a switch are RJ45 (Registered Jack 45)

#### What is Ethernet?
*Ethernet is a collection of network protocols & standards
*We will focus on types cabling as defined by Ethernet standards

#### Why we need Network Protocols
If two people are communicating, and one only speaks English and the other Japanese, there will be no understanding.
What they need is some agreed upon system of communication, like a common language between them. Network Protocols serve this purpose for network devices.

## Bits and Bytes

Connections in a network operate a set speed, measured at bits/s. A bit is a value represented by 0's and 1's, 0 representing the on/off state on a conductor.
A series of 8 bits is known commonly as an octet or a byte. 
*1 Kilobit = 1 000 Bits. 
*1 Megabit = 1 000 000 Bits.
*1 Gigabit = 1 000 000 000 Bits.
*1 Terrabit = 1 000 000 000 000 Bits.

## Ethernet Standards

Defined by in the IEEE 802.3 standard. Consult the table to see the specifications for each type of Ethernet copper cable.
I will ignore the parts speaking about UTP and STP and BASE-T standards because I already know this.
Full Duplex tranmission means that BOTH devices can send and receive data simultaneously, and no collisions will occur because they use seperate wires.
A Straight-Through cable works when the two node types are differing and their pins match for receiving and sending data on the same pins.
A Crossover cable exists when you'd like to conjoin the same node types, because the nodes transmit/receive pins are the same so we must flip them.
In 8P8C, all cables are bidirectional, meaning that they are all used for receiving and transmitting data. This is why the throughput is so heavily increased.

## Auto-MDIX

Previously, if two networking devices were connected with a straight-through cable, they would be unable to communicate.
However, MDIX allows devices to detect what pins their neighbor are transmitting data on and then adjust their pins automatically to receive correctly.

## Fiber optics

Larger networks need to travel far longer than 100m distance runs. On modern switches, we have SFP slots, which are then connected to a Fiber optic connector type.
The fiber optics used two cables, one for transmitting and one for receiving on both sides for full-duplex. They are light signals sent very quickly over a fiberglass 
core.

### Going to skip multimode and singlemode

Refer to the table specifying the standards for fiber optic cabling.

---
