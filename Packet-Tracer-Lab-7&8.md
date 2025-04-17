# Packet Tracer Lab 7/8 — Router and PC Configuration

---

## Summary ##

In this lab, I configured Router 1 (R1) and connected workstations to test IP addressing and connectivity. I changed the hostname of R1, assigned IP addresses to the router's interfaces, enabled them, and configured interface descriptions. After configuring the IP addresses on the PCs (PC1, PC2, and PC3), I tested connectivity by pinging between the endpoints. I ran into an issue with connectivity between PC1 and other PCs, which I resolved by configuring the default gateway on PC1, allowing successful communication through the router.

---

## What I Did ##

1. **Configured the hostname on Router 1**:
   - Entered global configuration mode on R1 and changed the hostname to `R1`.
   - Command used:  
     `hostname R1`

2. **Configured IP addresses and enabled interfaces on R1**:
   - Used the `show ip interface brief` command to display a list of R1's interfaces, their IP addresses, and their status.
   - Configured IP addresses for R1’s interfaces and enabled them.
     - Command used:  
       `interface FastEthernet0/0`  
       `ip address [IP_ADDRESS] [SUBNET_MASK]`  
       `no shutdown`
     - Added descriptions for the interfaces to help with identification.
     - Command used:  
       `description Link to PC1`

3. **Verified configuration on R1**:
   - Used `show ip interface brief` again to confirm the changes.
   - Command used:  
     `show ip interface brief`

4. **Configured the IP addresses on PC1, PC2, and PC3**:
   - Configured the IP address and subnet mask for each PC according to the CIDR provided in the lab.
   - Example for PC1:  
     `IP Address: [PC1_IP]`  
     `Subnet Mask: [PC1_SUBNET_MASK]`  
     I repeated this step for PC2 and PC3 with their respective IPs.

5. **Pinged between PCs**:
   - Tried to ping from PC1 to PC2 and PC3 to test connectivity.
   - PC1 could not ping other PCs, so I investigated the issue.

6. **Troubleshooting**:
   - I noticed that the issue was with the default gateway configuration on PC1, which was missing.
   - Added the default gateway on PC1.
     - Command used on PC1:  
       `Default Gateway: [DEFAULT_GATEWAY]`
   - After this change, I successfully pinged PC2 and PC3 from PC1.

7. **Saved the configuration**:
   - Used the `copy running-config startup-config` command to save the configuration on R1.
     - Command used:  
       `copy running-config startup-config`

---

## Network Overview ##

The lab setup included:

- **Router R1** with two interfaces configured (FastEthernet0/0 and FastEthernet0/1).
- **Three PCs** (PC1, PC2, and PC3) configured with IP addresses, subnet masks, and default gateways.
- **Connectivity** between the PCs was tested using the `ping` command, which initially failed from PC1 to others due to the missing default gateway.

The goal of the lab was to configure IP addresses on devices, enable interfaces on the router, and troubleshoot connectivity issues. The key learning was identifying the missing default gateway on PC1 as the root cause of the connectivity failure.

---

## Screenshots ##

![Lab Screenshot 1](lab7-1.png)  
![Lab Screenshot 2](lab7-2.png)  
![Lab Screenshot 3](lab7-3.png)  
![Lab Screenshot 4](lab7-4.png)  
![Lab Screenshot 5](lab7-5.png)  

---

## Wrap-up ##

In this lab, I configured the router and PCs to establish network connectivity. I learned how to assign IP addresses, enable interfaces, and troubleshoot network issues. The experience of resolving the default gateway issue on PC1 was valuable in understanding the critical role of proper network configuration.
