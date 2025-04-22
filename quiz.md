
# Quiz 19 #

---

### SW1 and SW2 are connected, are both new switches and the connected interfaces are operating as access ports. However, SW2 power supply fails, so you replace SW2 with an old spare switch. You reset the config before connecting it to SW1, but when you connect it you realise that a trunk is formed between the two switches. What could be the cause? ###

#### POSSIBLE ANSWERS ####

* Interfaces default to ```switchport mode trunk```
* Interfaces on old switches default to ```switchport mode dynamic desireable```
* Access ports are a feature of newer switches

##### MY ANSWER: b) interfaces on old switches default to desireable  ######

### SW1 is connected to SW2, and SW2 to SW3. You want SW2 to forward SW1's VLAN database info to SW3 but you do not want SW2 to sync its database to SW1. Which command should you use on SW2? ###

#### POSSIBLE ANSWERS ####

* ```vtp mode transparent```
* ```vtp transparent mode```
* ```vlan mode transparent```
* ```vtp mode client```

##### MY ANSWER: a) ```vtp mode transparent``` #####

### What are two methods to reset a switches revision VTP number to 0? ###

#### POSSIBLE ANSWERS ####

* Change the VTP domain name
* Change the SW to vtp server mode
* Change the SW to vtp transparent mode
* Use the ```vtp reset``` command
  
##### MY ANSWER: a) & c) #####

---
