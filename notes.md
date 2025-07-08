# Syslog

## What is Syslog?

Syslog is an industry standard protocol for message logging. When speaking about network devices, Syslog typically logs events regarding dynamic routing protocol status, interface status, system restarts, etc...

The messages can be displayed in the CLI of the device, saved in the devices RAM or ideally sent to an external dedicated syslog server.
Logs are essential for troubleshooting devices and to see what happened and at what time.

## Syslog Message Formatting

The syslog message formatting in CiscoOS is as follows

---

seq:time_stamp:%facility-severity-MNEMONIC:description
Where seq means the sequence in which the event happened, it's relation to other events in the timeline
Timestamp displays the moment in time in which the message was saved to Syslog relevant to the NTP sync of the device.
%Facility refers to the process or protocol on the device generated the message.
Severity refers to the importance of the message, some messages are simply informational, others indicating a serious and immediate problem.
MNEMONIC is just a short relevant description to indicate what has happened.
Description is an in-depth description of the error or event that occured and is displayed last within the Syslog message.

## Syslog Severity Levels

Level 0 - EMERGENCY - System is unusable, shutdown imminent

Level 1 - ALERT - Action must be taken immediately

Level 2 - CRITICAL - Critical conditions

Level 3 - ERROR - Error conditions

Level 4 - WARNING - Warning conditions

Level 5 - NOTIFICATION - Normal but significant condition

Level 6 - INFORMATIONAL - Info message

Level 7 - DEBUGGING - Debug message

### Syslog Save Areas

Console line: Syslog messages will be displayed in the CLI when connected directly through console port on the physical hardware.
VTY lines: Syslog messages will be displayed in the CLI when connected to the device via Telnet or obviously SSH/Putty.
Buffer: The syslog messages will be saved to RAM and viewed with *do show login* command.
Centralized server: network management is easier and all syslog message are sent to a server. Syslog uses port UDP514. 

## Difference between SNMP & Syslog

Syslog and SNMP are both used for monitoring and troubleshooting devices. Syslog is used for message logging, categorized by facility and severity and are logged inside and externally.
The main difference between the two is that SNMP allows you to queryt devices and to get additional information. Syslog simply relays information to another server in which you cannot query additional info beyond the logs.
