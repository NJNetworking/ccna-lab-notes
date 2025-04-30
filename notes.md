# IPv6 Notes

## Intro to IPv6

IPv6 (Internet Protocol version 6) replaces IPv4 to address its limitations, especially address exhaustion. It uses 128-bit addresses, allowing for 2^128 (about 3.4×10^38) unique IP addresses. This removes the need for NAT in most use cases and enables direct end-to-end communication.

Benefits include:
- Vastly larger address space
- Simplified packet headers
- Built-in support for IPsec
- No need for broadcast (uses multicast)
- Native support for autoconfiguration (SLAAC)
- More efficient routing and better mobility features

## Hexadecimal Review

IPv6 addresses are written in hexadecimal (base 16). Hex digits range from 0–9 and A–F (A = 10, F = 15). Each IPv6 address consists of 8 groups (called hextets) of 4 hex digits separated by colons.

Example:  
2001:0db8:0000:0000:0000:ff00:0042:8329

Each hextet is 16 bits, so the full address is 128 bits total.

## IPv6 Condensing

IPv6 addresses can be shortened using the following rules:

1. Remove leading zeroes in each hextet.  
   Example: 0db8 becomes db8  
2. Replace a single contiguous sequence of all-zero hextets with a double colon ::  
   Example: 0000:0000:0000 becomes ::  
   You can only use :: once per address

Example:  
Original: 2001:0db8:0000:0000:0000:ff00:0042:8329  
Condensed: 2001:db8::ff00:42:8329

## Identifying the IPv6 Prefix

Just like subnet masks in IPv4, IPv6 uses prefix lengths to define networks. A /64 prefix means the first 64 bits are the network portion, and the remaining 64 bits are used for interface identifiers.

Example:  
2001:db8:acad:1::/64

Prefix lengths can vary:
- /64 is common for subnets assigned to hosts
- /48 or /56 are often used for ISP allocations

## Configuring IPv6 in Cisco IOS CLI

Enable IPv6 globally:
ipv6 unicast-routing

Configure an interface with a global unicast address:
interface g0/0  
ipv6 address 2001:db8:acad:1::1/64  
no shutdown

Configure link-local manually (optional):
ipv6 address fe80::1 link-local

Verify:
show ipv6 interface brief

## EUI-64 and EUI CLI Config

EUI-64 is a method of automatically generating the interface ID portion of an IPv6 address using the MAC address of the interface.

Enable IPv6 using EUI-64:
interface g0/0  
ipv6 address 2001:db8:acad:1::/64 eui-64

This will automatically generate the last 64 bits based on the MAC address.

## IPv6 Address Types

- Global Unicast: Publicly routable addresses, starts with 2000::/3
- Link-Local: Used on the local link only, always starts with fe80::
- Unique Local: Private, non-routable, similar to IPv4’s 192.168.x.x; starts with fc00::/7
- Multicast: Sent to multiple devices at once, starts with ff00::/8
- Anycast: Multiple devices share the same address; packet is routed to the nearest one
- Loopback: ::1, equivalent to 127.0.0.1 in IPv4

## IPv6 Header Components

IPv6 headers are simplified compared to IPv4. The base IPv6 header is 40 bytes and includes:

- Version (4 bits)
- Traffic Class (8 bits)
- Flow Label (20 bits)
- Payload Length (16 bits)
- Next Header (8 bits)
- Hop Limit (8 bits)
- Source Address (128 bits)
- Destination Address (128 bits)

There is no header checksum (removed for performance), and fragmentation is handled by the sending host, not routers.

## Solicited-Node Multicast Address

This is a special multicast address that ends in the last 24 bits of a device’s IPv6 address. It’s used for Neighbor Discovery Protocol (NDP) to resolve link-layer (MAC) addresses.

Format: ff02::1:ffXX:XXXX  
Example: For address ending in 42:8329, the solicited-node multicast is ff02::1:ff42:8329

## NDP - Neighbor Discovery Protocol (NS & NA)

NDP is the IPv6 equivalent of ARP in IPv4. It uses ICMPv6 messages to discover neighbors, resolve MAC addresses, and detect duplicate addresses.

Key message types:
- NS (Neighbor Solicitation): "Who has this IP?"
- NA (Neighbor Advertisement): "I have this IP"

## SLAAC - Stateless Address Autoconfiguration

SLAAC allows hosts to configure their own IPv6 addresses without DHCP. The host listens for Router Advertisements (RAs) and combines the advertised prefix with a generated interface ID (often using EUI-64).

## DAD - Duplicate Address Detection

Before a host assigns an IPv6 address to itself (e.g. via SLAAC), it runs DAD to make sure no other device is already using that address. It sends an NS for its own address. If no NA is received in response, the address is considered safe to use.

## Static Routing in IPv6 CLI

Configure a static route:
ipv6 route <destination-prefix> <next-hop>

Example:
ipv6 route 2001:db8:acad:2::/64 2001:db8:acad:1::2

If using link-local as next hop (common in IPv6), you must specify the outgoing interface:
ipv6 route 2001:db8:acad:2::/64 fe80::2 g0/0

Verify:
show ipv6 route

