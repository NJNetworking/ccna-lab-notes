# IP Addressing & Interface Configuration

---

## IPv4 Addressing ##

IPv4 is a **32-bit** address format divided into **4 octets** (8 bits each), written in **dotted decimal** notation.

Example: 192.168.1.1

Each octet ranges from 0 to 255.  
The address includes:
- A **network portion** (identifies the network)
- A **host portion** (identifies the specific device)

### CIDR Notation ###

CIDR (Classless Inter-Domain Routing) represents the subnet mask with a slash.

Examples:
- /8 → 255.0.0.0
- /16 → 255.255.0.0
- /24 → 255.255.255.0

So 10.1.1.1/24 means the first 24 bits are the network portion, and the last 8 are for hosts.

---

## Interface Configuration ##

---

### show ip interface brief ###

This command gives a short summary of interface info like IP, status, and protocol.

Example:

Interface              IP-Address      OK? Method Status                Protocol  
FastEthernet0/0        10.0.0.1        YES manual up                    up  
FastEthernet0/1        unassigned      YES unset  administratively down down  

Key columns:
- **Interface**: The interface name (e.g. FastEthernet0/1)
- **IP-Address**: IP assigned to the interface, or “unassigned”
- **OK?**: Whether the IP config is valid
- **Method**: How the IP was set (manual, DHCP, unset)
- **Status**: Layer 1 (physical) — up/down/administratively down
- **Protocol**: Layer 2 (data link) — up or down

---

### Interface Configuration Commands ###

To enter interface config mode:

conf t  
interface FastEthernet0/1  

To assign an IP address:

ip address 192.168.1.1 255.255.255.0  

To activate the interface:

no shutdown  

To shut down an interface manually:

shutdown  

To apply a description:

description Link to SW2  

To configure a range of interfaces:

interface range FastEthernet0/1 - 24  
