# Quiz 26 #

---

### Which of the following statements about OSPF are *not true*? (select two) ###

#### POSSIBLE ANSWERS ####

* In multi-area OSPF networks, all non-backbone areas must have an ABR connected to area 0
* Single-area OSPF must all use area 0
* Two OSPF routers with different process ID's can become OSPF neighbors
* The OSPF area must be specified in the network command
* An ASBR connects the internal OSPF networks to networks outside of the OSPF domain
* The OSPF process ID must match the area number
 
##### MY ANSWER: b) & f) ######

### You want to activate OSPF on R1 G0/1 and G0/2 interfaces with a single command. G0/1 IP: 10.0.12.1/28, G0/2 IP: 10.0.13.1/26. Which of the following commands should you use on R1?

#### POSSIBLE ANSWERS ####

* R1(config-router)# network 10.0.12.0 0.0.0.255 area 0
* R1(config-router)# network 10.0.12.0 0.0.0.254 area 0
* R1(config-router)# network 10.0.12.0 0.0.1.255 area 0
* R1(config-router)# network 10.0.8.0 0.0.3.255 area 0

##### MY ANSWER: c) #####

### Answer the following questions about the OPSF network below ###

##### MY ANSWER: There is 4 backbone routers, 1 ASBR and 3 ABRs #####

### Which of the following CLI commands will make R1 an OSPF ASBR? ###

#### POSSIBLE ANSWERS ####

* R1(config-router)# network 10.0.0.0 0.0.0.255 area 0, R1(config-router)# network 10.0.1.0 0.0.0.255 area 0
* R1(config)# ip route 0.0.0.0 0.0.0.0 203.0.113.2, R1(config)# router ospf 1, R1(config-router)# default-information originate
* R1(config-router)# network 0.0.0.0 255.255.255.255 area 0
 
##### MY ANSWER: b) ######

### Which command can be used to manually configure the OSPF router ID?

#### POSSIBLE ANSWERS ####

* R1(config-router)# router-id 1.1.1.1
* R1(config-router)# ospf router-id 1.1.1.1
* R1(config)# interface l0, R1(config-if)# ip add 1.1.1.1 255.255.255.255
* R1(config-router)# ospf router id 1.1.1.1

##### MY ANSWER: a) #####

---

# Quiz 28 #

---

### Which option states a characteristic of the OSPF p2p network type that is different than broadcast?  ###

#### POSSIBLE ANSWERS ####

* DR/BDR elections are held
* DR/BDR elections are not held
* Neighbors are dynamically discovered
* Neighbors are not dynamically discovered
 
##### MY ANSWER: b) ######

### There is an OSPF broadcast network with 5 connected routers. R1 is the DR on its G0/0 interface. How many FULL OSPF adjacencies does R1 have on the interface?

#### POSSIBLE ANSWERS ####

* 1, with the BDR
* 2, with the DR and BDR
* 4, with the all neighbors
* 5, with the routers connected to the segment
  
##### MY ANSWER: c) 4 #####

### Which of the following are requirements for routers to become OSPF neighbors (select two) ###

#### POSSIBLE ANSWERS ####

* Hello and Dead timers must match
* OSPF process IDs must match
* OSPF router IDs must match
* Interfaces must be in the same area
* Interfaces must be in different areas
* Interfaces must be in different subnets

##### MY ANSWER: a) & d) #####

### Which of the following LSA types is generated only in broadcast mode by the DR? ###

#### POSSIBLE ANSWERS ####

* Type 1
* Type 2
* Type 4
* Type 5

##### MY ANSWER: b) type 2 (network) #####


### R1 is connected to an OSPF broadcast network on its g0/0 interface. R4 is the DR of the segment and R3 is the BDR. All routers on the segment have the default OSPF priority. You issue `ip ospf priority 100` on R1's g0/0 to make it the DR. Which of the following statements are true about the network after you issue this command? (select two) ###

#### POSSIBLE ANSWERS ####

* R1 is the DR
* R1 is the BDR
* R1 is still a DROther
* If you issue `clear ip ospf processes` on R4, R1 will become BDR
* If you issue `clear ip ospf processes` on R4, R1 will become DR
* The DR and BDR are unchanged

##### MY ANSWER: d) & f) #####

---


