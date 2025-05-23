
CDP/LLDP share info with and discover info about neighboring devices

L2 Discovery BUT they can share L3 info

CDP = Cisco proprietary

LLDP = industry standard 8021.ab

Could be considered a security risk due to sharing info about the network


Timers

|      | Message | Holdtime | Reinitialization |
| ---- | ------- | -------- | ---------------- |
| CDP  | 60      | 180      | N/A              |
| LLDP | 30      | 120      | 2                |

### **CDP**

Enabled by default

CDP messages are periodically sent to multicast:
MAC Address: 0100.0CCCC.CCCC

When a device, receives a CDP message it process and discard the message.   Does NOT forward the message

Sent once every 60 seconds

Hold time is 180 seconds if a message isn't received in that time neighbor is removed from the table

CDPv2 messages are sent by default

```
R1# show cdp
R1# show cdp traffic
R1# show cdp interfaces
```

CDP is on by default

###### CDP Config

```
! enable globally
R1(config)# cdp run
! CDP timer
R1(config)# cdp time <seconds>
! Enable CDPv2
R1(config)# [no] cdp advertise-v2
```

****
### **LLDP**

Industry standard: 802.1ab

Disabled on Cisco devices by default

Device can run both CDP and LLDP 

LLDP messages are sent to multicast address:
MAC Address: 0180.C200.000E

When a device receives a LLDP message it processes it and discards it.  It DOES NOT forward it

LLDP has an additional "re-initialization delay"  If LLDP is enabled globally or on an interface.  This timer will delay the initialization of LLDP 2 seconds by default.

LLDP is disabled by default globally and on an interface
###### **LLDP Config**
```
! enable
R1(config)# lldp run
```

```
! transmit lldp on an interface
R1(config-if)# lldp transmit
! recieve lldp on an interface
R1(config-if)# lldp recieve
```

```
! set lldp message timer
R1(config)# lldp timer <seconds>
! set lldp holdtime
R1(config)# lldp holdtime <seconds>
! set lldp reinitialization time
R1(config)# lldp reinit <seconds>
```


##### Enable / Disable

**CDP**
run = global
enable = interface