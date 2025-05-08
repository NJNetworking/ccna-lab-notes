# ACL (Access Control Lists)

## What are ACL?

ACL have multiple usecases, in their most basic security form simply control which devices have access to another part of the network.
This is the main purpose of ACL, but not the only purpose however it is the security perspective we will focus on.

ACL function as packet filters, instructing the router to either permit or discard specific traffic. ACL can filter traffic based on src/dst IP addresses, src/dst L4 ports, etc...

## How ACL function

Building ACL are configured specifically to satisfy a requirement. Let's say endpoints in 192.168.1.0/24 should ONLY be able to access the 10.0.1.0/24 network.
However, hosts in the 192.168.2.0/24 should not be able to access 10.0.1.0/24. How can we achieve this using ACL?

Firstly, ACL are configured on the router in global config mode. ACL are made up of an ordered series of ACE (Access Control Entries). For example, we could have 3 ACEs in ACL 1 to satisfy our requirements.
One would be permit, then deny, then the any clause ACE. However, configuring an ACL with ACE in global config mode on the router WILL not apply it. We must first create it, then add it to an interface in question.
The ***order*** in the ACL is ***PARAMOUNT***, because the ACEs are processed logically from top of the list to the bottom. The most restrictive and specific rules should generally be put first for that reason.

A maximum of 1 ACL can be applied to one interface in both directions, meaning 1 inbound ACL and 1 outbound ACL on each interface is allowed. If you apply a new one it will overwrite the previous.
Standard ACL should be applied on the interface closest to the destination as possible.

### Inbound and Outbound ACL ###

Inbound ACLs filter traffic as it enters an interface, before it's routed — useful for blocking unwanted access before it reaches the network. 
Outbound ACLs filter traffic after routing decisions are made — useful for controlling what leaves the network, such as restricting certain outbound services or destinations.

## Implicit Deny

The implicit deny is the rule always applied as an ACE by defualt at the end of a ACL that tells the router to deny all traffic that doesn't implicitly match any of the rules configured in the ACL.

## ACL Types

There are two main types of ACL with two different subtypes:

1: Standard ACL, match based on source tcp/IP only
---
- Standard Numbered ACL
- Standard Named ACL

2: Extended ACL, match based on source/dest TCP/IP, src/dst port, MAC address, etc...
---
- Extended Numbered ACL
- Extended Named ACL

### Standard ACL

Standard ACL match traffic through ACE based only on the source IP of the traffic, so they are rudimentary.
Numbered ACL are identified with a number, named ACL are identified with a name. This is because you can configure MANY ACL on a single router.

The CiscoOS CLI command to config an Standard Numbered ACL is ```access-list number deny/permit ip wildcard-mask```.

Additional tags are ```host``` (to specify /32 subnet mask), ```any``` (to allow all traffic) & ```remark ##___##``` to add a note to the ACL entry.

The CiscoOS CLI command to push the ACL onto an interface is interface config ```ip access-group # in/out```.

#### Standard NAMED ACL

Standard named ACL are still standard ACL but they are actually good in the sense you can name them logically instead of sifting through random numbers and their associated ACEs.
To configure CiscoOS CLI command is ```ip access-list standard (acl-name)```. You now add the ACEs like this ```entry-number deny/permit ip wildcard-mask```.
