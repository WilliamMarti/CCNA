3x Versions:
- v1
- v2
- v3

Max hop count = 15

2x Message Types:
- Request
- Response

##### **RIPv1**

Only advertises Classful address space (A/B/C)
No VLSM/CIDR

Messages broadcast to 255.255.255.255

##### **RIPv2**

Supports VSLM/CIDR

Includes subnet mask info

Message are multicast from 224.0.0.9

**Broadcast** - All devices on the local network
**Multicast** - Messages are delivered only to device that have joined that multicast group

```
R1(config)# router rip
R1(config)# version 2
R1(config)# no auto-summary
! assumed to be 10.0.0.0/8
! looks for interfaces that fall in the 10.0.0.0/8 range
! OSPF and EIGRP are similar
R1(config)# network 10.0.0.0
R1(config)# network 172.16.0.0
```

network 10.0.0.0 tells the router which interfaces to activate RIP on.  DOES NOT tell which networks to advertise. 

```
R1(config)# default-information originate
R1(config)# distance {number}
R1(config)# maximum-paths {number}
```

