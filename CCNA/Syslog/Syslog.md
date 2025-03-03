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
**RFC5424** - Severeities are subjective.  A relay/collector should not assume all originators have the same definition of severity.  Cisco vs Juniper 