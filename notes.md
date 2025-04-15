# Network Devices #

---

## Definitions ##
Nodes: networking infrastructure devices, routers, switches, firewalls, servers, workstations/clients. 
Clients and servers may be referred to as end hosts, or end-points

## Building a network ##

Let's build a network and examine each nodes role within it. We have 2 PC's, PC 1 on the left and PC 2 on the right. This is not a network, but if we connect them with cables, it makes a simple network.

## Clients & Servers ##

Simple definition of a client: A device that accesses a service made available by a server. 
So... what's a server? Simple defintion of a server: A device that provides functions or services for clients.
Let's think of our small network, the two linked PC's. PC1 asks for the image.jpg file from PC2, PC2 responds and sends the image file. PC1 is therefore the client and PC2 the server.
Let's look at another example of a client-server relationship. On the left is your client, on the right is the Youtube Servers which contains the video. The blue cloud represents the internet.

## Switches ##

Alrighty, we now know what a client and a server is. Let us now build out the network further and show the next part of the connection between end-hosts and the internet.
However, we don't typically link endpoints to each other directly, we use an aggregator called a switch, with many Ethernet interfaces.
Switches are used to forward traffic within a LAN or VLAN segmentation. PC1 and PC2 and any other devices connected to switch 1 are on the same intranet and can communicate with each other, but not to the internet yet.

### Switch types within Cisco ###

Let's talk more about switches, on the left we have the CISCO Catalyst 9200 model swtich, on the right is a CISCO Catalyst 3650 model switch. Catalyst switches are CISCO's enterprise-grade switches.
Switches usually have many network interfaces for endpoints to connect to, typically 24 or more. Switches provide connectivity to hosts within the same LAN.

## Routers ##

The device that lets us bridge switches to the internet is the router. When endhosts in one subnet want to speak to another, the traffic is forwarded over the router.

### Router types within Cisco ###

A few examples of Cisco routers: ISR-1000, ISR-4000 have their network interfaces on the back. The ICR-900 has the network interfaces on the front.
Routers... have fewer network interfaces than switches. Routers are used to provide connectivity between LANs. Because of this, routers are used to send data over the internet.

## Firewalls ##

Firewalls should be used to protect our networks, which are specialty network infrastructure security devices. They control data coming into the ingress and exiting the egress points of your network.
What is important is that they protect the endpoints inside the LAN. Firewalls must be configured with security rules to determine which traffic should be allowed and denied.

### Firewall types within Cisco ###

On the left is a ASA5550-X hardware firewall. The ASA (Adaptive Security Appliance) is CISCO's classic firewall. Modern ASA contain capabilities of NGFW's including things like IPS, IDS, etc...
On the right is a Firepower 2100 hardware firewall. This is a NGFW as well.
Firewalls monitor and control network traffic based on specific rules. Firewalls can filter traffic before it goes through the router, or after it has passed through the router.

---
