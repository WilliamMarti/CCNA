
1. **HSRP** - Hot Standby Router Protocol
2. **VRRP** - Virtual Router Redundancy Protocol
3. **GLBP** - Gateway Load Balancing Protocol
4. **GARP** - Gratuitous ARP.  ARO replies sent without request.  Broadcast to ffff.ffff.ffff

FHRP's are not pre-emptive.  Meaning the current active router will not give up its role.  Even if former active router comes back online

A Virtual IP is created on both routers and a virtual MAC Address is generated for the Virtual IP

Active and Standby routers are elected

End Hosts use the Virtual IP for the Default Gateway

Active Router replies to ARP requests using the Virtual MAC so traffic destined for other networks will be sent to the it.

If Active Route fails, Standby Router takes over as the new Active.  New Router uses GARP to advertise new MAC Address.

If old router comes back online it wont take back its role as Active, will be Standby


## HSRP

Cisco Proprietary

Active + Standby are elected

2x Versions
- v1 - Original
- v2 - Adds IPv6 support and additional number of groups. 
Can configure a different active router  to load balance **per subnet**
##### Configure HSRP
###### **Router 1**
```
Router(config)# int g0/0
Router(config-if)# standby version 2
Router(config-if)# standby 1 ip 172.16.0.254
! priority is a value of <0-200>
Router(config-if)# standby 1 priority 200
Router(config-if)# standby 1 preempt
```

###### **Router 2**
```
Router(config)# int g0/0
Router(config-if)# standby version 2
Router(config-if)# standby 1 ip 172.16.0.254
! priority is a value of <0-200>
Router(config-if)# standby 1 priority 50
! preempt on a standby router does nothing
! just makes for consistent configurations
Router(config-if)# standby 1 preempt
```


| Version | Virtual MAC Address | Multicast Address |
| ------- | ------------------- | ----------------- |
| v1      | 0000.0c07.acXX      | 224.0.0.2         |
| v2      | 000.0c9f.fXXX       | 224.0.0.102       |
|         |                     |                   |
