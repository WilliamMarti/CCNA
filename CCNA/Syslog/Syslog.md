Industry standard for logging messages 

Interface Status
OSPF Neighbor Status
System Restarts

{seq} {timestap} {%facility}-{severity} - MNEMONIC description

seq - Sequence Number
timestamp - time of log message
facility - which process generated message
severity - number of the severity (1-8)
MNEMONIC - Shot code for the message
description - detail of the event

##### Syslog Levels

| Number | Name          | Detail                          | Acronym   |
| ------ | ------------- | ------------------------------- | --------- |
| 0      | Emergency     | System is unusable              | Every     |
| 1      | Alert         | Action must be taken immediatly | Awesome   |
| 2      | Critical      | Critical condition              | Cisco     |
| 3      | Error         | Error conditions                | Engineer  |
| 4      | Warning       | Warning conditions              | Will      |
| 5      | Notice        | Normal but significat           | Need      |
| 6      | Informational | Informational messages          | Ice Cream |
| 7      | Debugging     | Debug-level messages            | Daily     |
**RFC5424** - Severities are subjective.  A relay/collector should not assume all originators have the same definition of severity.  Cisco vs Juniper 

##### Logging Locations

**Console Line** - Syslog messages will be display in the CLI for anyone connected bia the console.  By default all syslog messages (0-7) are displayed

**VTY Lines** - Syslog will be displayed when connected via Telnet/SSH.  Disabled by default.

**Buffer** - Syslog saved to RAM.  Default all message are displayed

```
R1# show logging
```

**External Server** - Can send syslog to an external server.  Syslog server will listen on UDP 514

##### Config

```
! 6 = info and higher
! config logging to console line
R1(config)# logging console 6 
R1(config)#
```

```
! config logging to vty lines
R1(config)# logging monitor informational
```

```
! config logging to the buffer (in bytes)
R1(config)# logging buffered 8192
```

```
R1(config)# logging 192.168.1.100
R1(config)# logging host 192.168.1.100
R1(config)# logging trap debugging 
```

```
! display logging in vty 
R1# terminal monitoring
```

```
R1(config)# line console 0
! commands will be printed on a new line when a log comes in
R1(config)# logging syncronous
```

```
R1(config)# service timestamp log datetime
R1(config)# service sequence-numbers
```
