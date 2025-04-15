
```
R1# show clock
```

Default timezone is UTC

Hardware calendar is the default time source
	Means NOT authoritative

Internal clock will drift over time

Most important reason (for CCNA) to have accurate time is for **logging**

```
R1# show logging
```

```
R1(config)# clock set hh:mm:ss <1-31> <month> <year>
```

```
R1# show clock internal
```

Manually convert

```
R1# calendar set hh:mm:ss <1-31> <month> <year>
```

You want to sync *time* and *calendar*

clock = software clock
calendar = hardware clock

```
! Sync calendar to clock time
R1# clock update-calendar
```

```
! Sync clock to calendar time
R1# clock read-calendar
```

```
R1# clock summer-time recurring <name> <start> <end> [offset]
```

Reference clocks are stratum 0

NTP servers directly connected to reference clocks are stratum 1

Stratum 15 is the max, anything above that is considered unreliable

3x Modes of NTP:
1. Server 
2. Client
3. Symmetric active Mode

**Primary Servers** - NTP servers who get their time from reference clocks

**Secondary Servers** - Get time from primary servers.  Act as both client and servers

```
R1(config)# ntp server 216.239.35.4
```

``` 
R1# show ntp associations
```

```
R1# show ntp status
```

```
R1(config)# ntp source loopback0
```

```
R1(config)# ntp authenticate
R1(config)# ntp authentication-key <key-number> md5 <key>
R1(config)# ntp trusted-key <key-number>
R1(config)# ntp server <ip-address> key <key-number>
R1(config)# ntp peer 10.0.23.1 key <key-number>
```



##### NTP Master

Router becomes an authoritative name server

Listen on all interfaces