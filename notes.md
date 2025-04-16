# Ethernet switching

---

## Ethernet frames 

We have a packet encapsulated within a layer 2 Ethernet header and trailer, making an Ethernet frame. There are 5 fields within the Ethernet frame header.
* The Preamble and SFD (Startframe Delimiter) which are used for synchronization and for the device to be prepared to receive the data in the frame.
* The Destination, the layer 2 MAC address to which the frame is being sent.
* The Source, the layer 2 MAC address of the device that sent the frame.
* The Type, which indicates the L3 protocol used in the encapsulated packet, which is almost always IPv4 or IPv6. However, sometimes this is a length field.

The Ethernet trailer has only 1 field: the FCS (Framecheck Sequence) which is used by the receiving device to see if any errors have occured during transmission.
Here are the first 2 fields, the preamble and SFD, which are typically grouped together:
**Preamble** is 7 bytes or 8x7=56 bits, and is a series of alternating 1's and 0's, 10101010. The purpose of this is for the device to synchronize the receivers clock.
**SFD** is 1 byte or 1x8=8 bits, it's bit pattern is 10101011. It indicates the end of the preamble and the rest of the frame.
Now are the next two fields, the destination and source fields:
**Destination** says to whom the frame is being sent based on their 6 byte MAC address
**Source** says who is sending the frame and their associated 6 byte MAC address 

**Type/length** is 2 bytes long, used to represent the type of the encapsulated packet or it's length. When the binary adds up to something under 1500 in decimal, it suggests that it is specifying the length. When it is surpasses this 1536 it is suggesting that it is specifiying the IPv4 or IPv6 type.

**FCS** is the framecheck sequence and is 4 bytes in length. It's purpose is to detect corrupted data using CRC.
This means that the total size of an Ethernet frame header and trailer is 24 bytes.

## MAC addresses

A 6-byte/48-bit physical address assigned to the device when it is made. The MAC address may be referred to as a BIA (Burned-in address). The MAC address is globally unique.
The first 3 bytes are the OUI (Organizationally Unique Identifier) which specifies the manufacturer's brand. The last 3 bytes are unique to the device itself. 
Mac addresses are written as a series of 12 hexadecimal characters.

### Decimal System ###

The **decimal system** is the standard number system used in everyday life.  
It is **base 10**, meaning it uses **10 digits**:  
`0, 1, 2, 3, 4, 5, 6, 7, 8, 9`  

Each place value is a power of 10:
- 345 = (3 × 100) + (4 × 10) + (5 × 1)

### Hexadecimal System ###

The **hexadecimal system** is **base 16**, often used in computing and networking.  
It uses **16 digits**:  
`0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F`

- Letters `A–F` represent values `10–15`
- Each hex digit represents 4 binary bits (a nibble)
- Often written with a prefix like `0x` (e.g. `0x2F`)

Example:  
`0x1A` in decimal is `(1 × 16) + (10) = 26`

## Dynamic MAC

On Cisco switches, dynamic MAC addresses are removed from the table after 5 minutes of traffic inactivity.

## Aging ##

Aging in networking refers to the process by which a network device, like a switch, removes or updates entries in its MAC address table after a certain period of inactivity. When a MAC address is no longer seen for a specified period, it is "aged out" and removed from the table to free up space for new addresses.

## Flooding ##

Flooding is the process by which a switch sends a network packet to all ports when it doesn't have an entry for the destination MAC address in its MAC address table. It typically happens when the switch does not know where the destination device is located in the network, forcing it to broadcast the packet to all ports except the one it came from.

---

