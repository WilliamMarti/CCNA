Simple Network Management Protocol

SNMPv1
RFC 1065 - Structure and identification of management information
RFC 1066 - Management information base
RFC 1067 -

Monitor Status and make config changes

Two main devices:
1. Managed Devices
	1. Routers/Switches
2. Network Management System (NMS)

SNMP Object ID are organized in a hierarchy structure 

.1.3.6.1.2.1.1.5

1 - iso
3 - identified organization 
6 - dod
1 - Internet
2 - mgmt
1 - mib-2
1 - system
5 - sysname

**SNMPv1** - Original Version
**SNMPv2c** - Allow NMS to retrieve large amounts of info in a single request.  "c" refers to "community strings" used as passwords.  Removed from v2 and added back on 2c
**SNMPv3** - Secure.  Supports **encryption** and **authentication**


| Message Class | Description                                            | Message                  |
| ------------- | ------------------------------------------------------ | ------------------------ |
| Read          | Sent by NMS to read info from managed device           | Get / GetNext / Get Bulk |
| Write         | Sent by NMS to change info on the managed device       | Set                      |
| Notification  | Sent by managed device o alert NMS                     | Trap / Inform            |
| Response      | Message sent in response to a previous message/request | Reponse                  |
SNMP used **UDP**

Traps area "unreliable", no response is sent from NMS

Inform a message, response is sent

SNMP agent 161 UDP
SNMP manager 162 UDP

```
R1(config)# snmp-server contact user@test.com
R1(config)# snmo-server location Chicago
R1(config)# snmp-server community xya ro
R1(config)# snmp-server community abc rw
R1(config)# snmp-server host 192.168.1.1 version 2c xyz
R1(config)# snmp-server enable traps snmp linkdown linkup
R1(config)# snmp-server enable traps config
```



