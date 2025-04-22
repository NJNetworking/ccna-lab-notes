# DTP/VTP

---

## What is DTP?

DTP (Dynamic Trunking Protocol) is a Cisco protocol that allows switches to dynamically determine their interface status (access or trunk) without manual configuration.
Two Cisco switches connected together can form a trunk otherwise the interface will automatically be an access port. DTP is enabled by default on all Cisco switches.
For security reasons, manual config is recommended as DTP can be exploited by attackers and should be disabled.

### DTP auto vs desirable

```switchport mode dynamic (DTP) desireable``` will actively try to form a trunk with other Cisco switches, if connected to another switchport in the following modes: trunk, auto, desireable.
```switchport mode dynamic (DTP) auto``` is far more passive, it will only form trunks if requested by a trunk port or from desireable DTP. Otherwise it will stay as accessport.
Static access ---> means an access port that belongs to a single VLAN that doesn't change, unless you configure a different VLAN. There are also dynamic access ports automatically assigns the VLAN depending on the MAC of the connecting device.
DTP will not form a trunk with another nodetype automatically. The switchport remains in access mode until manually configured as trunk.

## Disable DTP

```switchport nonegotiate``` is the command to disable DTP and make it so you must configure trunks if you want inter-VLAN traffic.

## What is VTP?

VTP (VLAN Trunking Protocol) allows you to configure VLANs on a central server switch and other switches called VTP clients will synchronize their VLAN database to the server.
It is designed for large networks with many VLANs so you do not have to configure VLANs on every single switch. It is NOT recommended for security purposes like DTP.

### VTP Modes

* Server mode: Server mode can add, modify and delete VLANs. Cisco switches operate in VTP servermode by default. They store the VLAN database in NVRAM (Nonvolatile Random Access Memory).
  VTP servers will increase the **revision number** every time a VLAN is added modified or deleted. This number is important as it is what VTP uses to determine the newest VLAN database and synchronise the clients with it.
  VTP servers will advertise the latest version of the VLAN database on trunk interfaces and the clients will sync their databases to it.

* Client mode: clients CANNOT add, modify or delete VLANs. If you try to in the CLI the command will be rejected. VTP clients do not store the vlan database in NVRAM (except in VTP3).
  VTP clients will sync their VLAN database to the server with the highest revision number in their VTP domain.
  ```show vtp status``` is the Cisco IOS CLI-command to obtain real time information about the VTP status of a switch.

* Transparent mode: Switches in VTP transparent mode do NOT participate in the VTP domain, they do not sync the VLAN database with the VTP server.
  It can add, modify, and delete VLANs in NVRAM but will not be advertised to other switches. It will however forward/pass-on VTP advertisements over its trunk ports if the advertisement server is in the same domain.

  ## VTP versions

  ```vtp version (1,2,3)``` is the command to change the VTP version, it will update the revision number and new advertisements with the version will be sent and other servers/clients will sync.
  VTPv2 is no different from v1, except the introduction of Tokenring VLANs. Tokenring is obsolete so there is really no reason to use V2.
  As for version 3, there is many new features but not exactly relevant.

  ---
  

  
