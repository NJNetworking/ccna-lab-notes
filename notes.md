# Basic VLANs

---

## LAN (Local Area Network)

A **LAN** is a broadcast domain — a logical grouping of devices that can all receive broadcast frames from each other without going through a router. By default, all devices connected to the same switch are in the same LAN and can hear each other's broadcasts.

## VLAN (Virtual LAN)

A **VLAN** is a virtual LAN, or a **logical segmentation** of a physical switch. It allows the creation of multiple broadcast domains on a single switch. Devices in different VLANs cannot communicate with each other without a Layer 3 device (router or Layer 3 switch).

- VLANs are used to improve security, reduce broadcast traffic, and logically separate departments (like HR, Finance, Sales) even on the same physical infrastructure.

Example:  
- VLAN 10: HR  
- VLAN 20: Sales  
Even if HR and Sales machines are on the same switch, traffic won’t cross VLAN boundaries without routing.

## Purpose of VLANs

- **Segmentation**: Divide networks into smaller broadcast domains.  
- **Security**: Isolate sensitive traffic (e.g. accounting) from general users.  
- **Organization**: Group users by function or department regardless of physical location.  
- **Efficiency**: Reduce unnecessary traffic across the network.

## Access Ports

An **access port** is a switch port assigned to carry traffic for **one VLAN only**.

- It does **not use VLAN tags** — traffic is untagged.  
- Typically used for end devices like PCs or printers.

## Cisco IOS VLAN Commands

### View VLANs  
`show vlan brief`

### Create VLAN  
`vlan 10`

### Enter VLAN Configuration Mode  
`vlan 10`  
`name HR`

### Assign a Port to a VLAN (Access Mode)  
`interface FastEthernet0/1`  
`switchport mode access`  
`switchport access vlan 10`

---
