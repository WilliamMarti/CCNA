
[Chapter: Understanding and Configuring Dynamic ARP Inspection](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst4500/12-2/25ew/configuration/guide/conf/dynarp.html)




DAI (Dynamic ARP Inspection) - Security feature of switches that is used to filter ARP messages received on untrusted ports

DAI only filters ARP messages.  Non-ARP messages aren't affected.

All ports are untrusted by default

Typically ports connected to other network devices (router/switches) should be *trusted*.  Interfaces connected to end hosts should remain *untrusted*

##### ARP Poisoning

Involved an attack manipulating targets ARP tables so traffic is sent to the attacker

Attacker can send gratuitous ARP messages using another devices IP Address

DAI inspects the *senders MAC* and *sender IP* fields of ARP messages received on untrusted ports and checks that there is a matching entry in the DHCP Snooping Binding Table
	If Match -> Forward

DAI doesn't inspect messages received on trusted ports.  They forward as normal

ARP ACLs can be manually configured to map IP/MAC addresses for DAI to check
	For hosts not using DHCP

DAI Can be configured to perform more in-depth checks also but they are optional

DAI also supports rate-limiting
- DHCP Snooping and DAI both require work from CPU
- Even if the attackers messages are blocked, they can overload the switch with ARP messages

```
S1(config)# ip arp inspection vlan 1
S1(config)# int g0/0
S1(config-if)# ip arp inspection trust
```

```
S1# show ip arp inspection interfaces
```

```
S1(config)# int g0/0
! 25 - Default is 15, in pps
! 2 - Default is 1 (burst in seconds)
! Burst (Optional) For burst interval seconds, specify the consecutive interval in seconds, over which the interface is monitored for a high rate of ARP packets. The range is 1 to 15.
S1(config-if)# ip arp inspection limit rate 25 burst interval 2
S1(config-if)# int g0/1
S1(config-if)# ip arp inspection limit rate 10
```

Interfaces get put into err-disable
- `shut` / `no shut`
- `errdisable recovery cause arp-inspecton`


##### DAI Option Checks

```
! options will overwrite each other
S1(config)# ip arp inspection validate {x}
dst-mac
ip
src-mac
S1(config)# ip arp inspection validate dst-mac ip src-mac
```








