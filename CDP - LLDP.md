Timers

|      | Message | Holdtime | Reinitialization |
| ---- | ------- | -------- | ---------------- |
| CDP  | 60      | 180      | N/A              |
| LLDP | 30      | 120      | 2                |

### **CDP**

Muticast  MAC Address: 0100.0CCCC.CCCC

****
### **LLDP**

Muticast  MAC Address: 0180.C200.000E
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
! set llde[p message timer
R1(config)# lldp timer <seconds>
! set lldp holdtime
R1(config)# lldp holdtime <seconds>
! set lldp reinitialization time
R1(config)# lldp reinit <seconds>
```