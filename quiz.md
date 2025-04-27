# Quiz 25 #

---

### R1 & R2 both use RIP to share routes. R1 has a default route to the Internet that you want to advertise to R2. Which CLI command should you use? ###

#### POSSIBLE ANSWERS ####

* R1(config-router)# default-information originate
* R1(config-router)# network 203.0.113.0
* R2(config)# ip route 0.0.0.0 0.0.0.0 10.0.12.1
* R2(config-router)# default-information originate
 
##### MY ANSWER: a) R1 because it is the one with the default gateway that it wants to advertise and default-information originate does this. ######

### R1's G1/0 interface has an IP address of 172.20.20.17 and its G2/0 interface has an IP of 172.26.20.12. Which of the following commands will activate EIGRP on both interfaces?

#### POSSIBLE ANSWERS ####

* R1(config-router)# network 128.0.0.0 127.255.255.255
* R1(config-router)# network 172.16.0.0 0.0.255.255
* R1(config-router)# network 172.20.0.0 0.0.127.255
* R1(config-router)# network 172.20.0.0 0.3.255.255

##### MY ANSWER: a) the wildcard subnet mask in a is the only one that matches up with the IP that we want to advertise #####

### What is the correct order of priority when determing the EIGRP router ID? ###

#### POSSIBLE ANSWERS ####

* Highest possible loopback address, highest physical interface address, manual config
* Highest physical interface address, highest loopback interface address, manual config
* Manual config, highest physical interface address, highest loopback interface address
* Manual config, highest loopback interface address, highest physical interface address

##### MY ANSWER: d) manual config is first, loopback second, physical inter third #####

---
