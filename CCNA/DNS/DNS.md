
UDP port 53 TCP for message greater than 512 bytes

```
! enable DNS server
R1(config)# ip dns server
! list of entries
R1(config)# ip host test 192.168.0.1
! default DNS server to query
R1(config)# name-server 8.8.8.8
! Eanble R1 to perform DNS
R1(config)# ip domain lookup
R1(config)# ip domain name test.com
```

