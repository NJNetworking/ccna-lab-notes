# Cisco CLI commands

---

### What is a CLI? ###

We already know this. Cisco IOS however has different syntax than xterm and windowsOS CLI.

### How do we connect to a hardware dedicated networking infrastructure device? 

We use a cable and go to the infrastructure device itself and plug it into our PC and speak to the device through the CLI on the laptop.
To connect to the device through the console connection, we typically use a RJ45 into the switch and a DB9 into the laptop. This cable is called a rollover cable.
Our laptops do not have DB-9 serial connectors anymore, so we have to use a USB-A adapter into DB-9 male.

## What is PuTTY?

PuTTY is a **terminal emulator** used to establish command-line access over a serial connection.  
When connected from a laptop to a switch's **console port** using a **rollover cable**, PuTTY allows direct access to the device's **CLI** for initial configuration — even without the switch being on the network.

## The CLI

When you first enter CLI, you will by default be in User EXEC mode, indicated by the greater than sign next to the hostname of the device.
User EXEC mode is a very limited role in scope, they can look at things but not make many configurations.
If you enter the command ```enable``` from user mode, you will be placed in priviledged exec mode. A pound sign is displayed. You would not make modifications in this mode, only save current ones.
The command ```?``` is enough for help in Cisco CLI, you don't need ```man``` or ```help```. The tab key autofills as is commonplace in most CLI's.
Global configuration mode is the mode where you would make actual changes to network infrastructure. The command to enter GCM is ```configure terminal```.
When in the highest priviledge mode GCM, (config)# is inserted after the hostname.
Auth should be setup for protecting pExec and GCM. This is done with the command ```enable password```. Passwords are case-sensitive in CiscoIOS.
Cancelling commands can be done with the ```no``` prefix.

## Running-config & startup-config

There are two config files stored on any Cisco device kept seperately.
The running-config is the current, active configuration file on the device. As you enter commands in the CLI, you edit the active config.
The startup-config is the config file that will be loaded upon restart of the device.
Use the command ```show running-config/startup-config``` in the CLI to see what is contained with the config files, using pExec.
Let's save the running config to the startup config. In pExec use ```write```, ```write memory``` & ```copy running-config startup-config```
```service password-encryption``` adds type 7 Cisco proprietary XOR to the plaintext contained in the startup-config. This is very bad and very easily reversable however.
```enable secret``` adds type 5 encryption which is MD5 which is very easily cracked.
Use ```enable algorithm-type sha256``` to enable SHA256bit which is uncrackeable for the foreseeable future, salting not allowed on Cisco though.

---
