Binary - Base 2 - 0b

Decimal - Base 10 - 0d

Hexadecimal - Base 16 - 0x

"10" = binary, decimal, or hex?

##### **Binary to Hex**
________


0b11011011 = 219 Decimal

0b1101 -> 0d13 -> 0xD

0b1011 -> d11 -> 0xB

== 0xDB (Hex)

_____________

0b00101111

0b0010 -> 0d2 -> 0x2

0b1111 -> 0d15 -> 0xF

== 0x2F

_______________

0b10000001

0b1000 -> 0d8 -> 0x8

0b0001 -> 0d1 -> 0x1

== 0x81

##### **Hex to Binary** 
___________
0x2B = 0b ??

0x2 -> 0d2 -> 0b0010

0xB -> 11 -> 0b1011

== 0b00101011

---------------------

0xD7 = 0b ??

0xD -> 0x13 -> 0b1101

0x7 -> 0x7 -> 0b0111

== 0b11010111

IPv4 Addresses are controller by IANA (internet Assigned Number Authority)

IANA distributes IPv4 address space to various RIRs (Regional Internet Registries), which then assign them to companies

IPv6 is **128** bits
IPv4 is **32** bits

##### Shortening IPv6

Leading 0's can be removed

2001:0DB8:000A:001B:20A1:0020:0080:34BD ->
2001:DB8:A:1B:20A1:20:80:34BD

Consequitive quartets of all 0's can be replaced with double colon

2001:0DB8:0000:0000:0000:0000:0080:34BD ->
2001:0DB8::0080:34BD

Typically an Enterprise will get a /48 block

IPv6 subnets use /64 prefix length

Enterprise has 16 bits to use to make subnets

Remaining 64 bits can be used for hosts

2001:0DB8:8B00:0001:0000:0000:0000:0001/64

2001:0DB8:8B00 - 48 bit global routing prefix assign by the ISP

0001 - 16 bit subnet identifier used by enterprise to make various subnets

0000:0000:0000:0001 64-bit "interface ID" the host portion of the address

##### Configuring IPV6

```
R1(config)# ipv6 unicast-routing
R1(config)# int g0/0
R1(config-if)# ipv6 address 2001:db8:0:0::1/64
R1(config-if)# no shut
```

```
R1# show ipv6 brief
```

Interface will automatically have "link-local" address

##### EUI-64

Extended Unique Identifier

(Modified) EUI-64 is a method of converting a MAC Address (48 bits) into a 64-bit interface ID

This interface ID can then become the "host portion" of a /64 IPv6 address

Convert MAC --
1. Divide MAC Addresses in half
	1. 12:34:56:78:90:AB -> 123456    7890AB
2. Insert FFFEE in the middle
	2. 123456    7890AB -> 1234 56FF FE78 90AB
3. Invert 7th bit (the 2 below)
	1. 1***2***34 56FF FE78 90AB
	2. 2 = 0010 -> 0000 = 0x0
	3. 1034 566FF FE78 90AB <- Final answer


##### Configure EUI-64

```
R1(config)# int g0/0
R1(config)# no shut
R1(config)# ipv6 address 2001:db8::/64 eui-64
```

2001:db8 Prefix + EUI-64 id to generate address for this interface

##### Global Unicast

Public
Must Register to use them globally unique

Originally defined as the 2000::/3 block

2001:0DB8:8B00:0001:0000:0000:0001/64

2001:0DB8:8B00 = 48 bit "global routing prefix" assigned by ISP
0001 = 16 bit subnet identifies the Enterprise to make various subnets
0000:0000:0001 = 64-bit interface identifier the host portion of the address

3 Parts -
1. Global Routing Prefix
2. Subnet Identifier
3. Interface Identifier

**Unique Local**
1. Private addresses, cannot be used over the Internet
2. Don't need to be globally unique (should be)
3. Uses block FC00::/7
4. Later update required 8th bit set to 1, so first 2x digits must be **FD**

FD45:93AC:8A8F:0001:0000:0000:0001/64

FD = Unique local address
45:93AC:8A8F = 40-bit global ID should be **random**
0001 = 16-bit subnet identifier
0000:0000:0001 = 64-bit interface identifier

**Link Local Address**

Automatically generated on IPv6 Interfaces

```
R1(config)# int g0/0
! create ipv6 ip on a interface
R1(config)# ipv6 enable
```

Uses address block FE80::/10

ONLY FE80

Interface ID uses EUI-64 rules

Link-Local means that these address are used for communication within a single link (subnet)  Routers will not route packets with a link-local destination IPv6 address

Uses: 
* Routing Peers
* Next-hop address for static routes
* Neighbor Discovery (NDP, IPv6's replacement for ARP)

**Multicast**

Uncast: one-to-one
Broadcast: One source to all destinations
Multicast: One source to multiple destinations (that have joined the multicast group)

IPv6 use FF00::/8

IPv6 **does not** Broadcast

IPv6 defines multicast "scopes" which indicate how far the packet should be forwarded

Link Local (FF02) which stay in the local subnet

##### IPv6 Multicast Scope

**Interface-Local (FF01)** - Packet doesn't leave device. Can be used to send traffic to a service within the device

**Link-Local (FF02)** - Packet remain in the local subnet.  Routers will not route the packet between subnets

**Site-Local (FF05)** - Packet can be forwared by routers.  Should be limited to a single physical location (not forwarded over WAN)

**Organization-Local (FF08)** - Winder in scope than Site-Local.  Can be entire Company/Organization.

**Global (FF0E)** - No boundaries.  Possible to be routed over the Internet

##### Anycast

New feature of IPv6

one-to-one-of-many

Multiple routers are configured with the same IPv6 address

Use Routing protocol to advertise that address.  Routers will forward to nearest router with configured IP

No specific address range

```
R1(config)# int g0/0
R1(config-if)# ipv6 address 2001:db8:1:1::99/128 anycast
```

```
! unspecified IPv6 address
! For device thtat doesn't yet know its v6 address
::
```

IPv6 default routes are configured to ::/0
Same as 0.0.0.0/0

```
! Loopback
! Test protocol stack on local device
::1
```

Messages to Loopback are processed within the local device, but not sent to other devices.

IPv4 equivalent to 127.0.0.1/8

##### RFC - Request for Comment

RFC5952 - A recommendation for IPv6 Address Text Representation
Before this IPv6 was more flexible
* Could remove leading 0's OR leave them
* Replace all 0's with :: or leave them
* Upper OR lower case

RFC5952

* Leading MUST be removed
* :: MUST be used to shorten the longest string of all-0 quartets 
	* (if only 1x all-0, leave it as is)
* If 2x equal-length choices for the ::, use :: to shorten the one to the left
* Hexidecial chars MUST be lower case

###### IPV6 Header

* Length - 4 bits
* Indicates the version of ID that is used
* Fixed value of 6(0b0110)

##### Traffic Class

* Length - 8 bits
* Used for QoS

##### Flow Label

* Length - 20 bits
* Used to identify traffic "flows" (communication between a specific sources and destinations)

##### Payload Length

* Length 16 bits
* Indicates the length of the payload
* Length of the IPv6 Header itself isn't included

##### Next Header

* Length - 8 bits
* Indicates the type of the "next header"
	* TCP or UDP
* Same function as the IPv4 "Protocol" field

###### Hop Limit Header

- Length 8 bits
- Value is decremented by 1 by each router that forwards it.  If it reaches 0, the packet is discarded
- Same function as the Ipv4 header 'TTL' field

##### Source / Destination Header

- Length - 128 bits EACH
- Contain IPv6 address of a packets source and a packets destination

##### Solicited-Node Multicast Address

An IPv6 solicited-node multicast address is calculated from a unicast address

ff02:0000:0000:0000:0000:0001 + last 6 hex digits of unicast address

unicast address = 2001:0db8:0000:0001:0f2a:4ffff:fca3:00b1

== ff02::1:ffa3:b1

##### NDP - Neighbor Discovery Protocol

Various function, one of which is to replace ARP.
	ARP no longer used in IPv6

ARP-like function of NDP uses ICMPv6 and solicited-node multicast addresses to learn the MAC address of other hosts
	ARP uses Broadcast in v4

2x Message Types

1. Neighbor Solicitation (NS) = ICMPv6 Type 135
2. Neighbor Advertisement (NA) = ICMPv6 Type 136

IPv4 ARP Table = IPv6 Neighbor Table

```
R1# show ipv6 neighbor
```

Another function of NDP allows Hosts to discover routers on the local network

2x Messages

1. Router Solicitation (RS) = ICMPv6 Type 133
	1. Sent to multicast address FF02::2 (all routers)
	2. Asks all routers on the local link to identify themselves
	3. Sent when an interface is enabled/host is connected to the network
2. Router Advertisement (RA) = ICMPv6 Type 134
	1. Sent to multicast FF02::1 (all nodes)
	2. Router announces its presence, as well as other info about the link
	3. Those messages are sent in response to RS messages
	4. Also sent periodically, even if the router hasn't received an RS

##### SLAAC - Stateless Address Auto-Configuration

- Hosts use the RS/RA message to learn the IPv6 prefix of the local link (2001:db8::/64) and the automatically 
- When using the #ipv6 address prefix/prefix-length eui-64 command you need to manually enter the prefix
- With the "#ipv6 address auto config" command, you don't need the prefix.  The device used NDP to learn the prefix on the local link
- Device will use EUI-64 to generate the interface ID or it will be randomly generated (depending on the device/maker)


##### DAD - Duplicate Address Detection

- Check if other devices are using the same v6 address
- Happens any time a device is initialized as a v6 address is configured 
- Uses NS and NA
- Host will send NS to its own address.  If it doesn't get a reply it knows its unique

##### IPv6 Static Routing

Works same as IPv4

v4 and v6 processes are separate on the router.  2x different routing tables.  

v4 routing is enabled by default.
v6 routing is disabled by default

enable v6 with

```
R1(config)# ipv6 unicast-routing
```

If v6 is disabled, router will be able to send/receive v6 traffic, but not route v6 traffic.  

Connected network route is automatically added for each connected network

Local host route is automatically added for ac

Router for link-local addresses are not added to the routing table

```
R1(config)# ipv6 route dest/prefix-length {next-hop|exit  interface [next-hop]} [ad]
```

##### Directly Attached Static Route
Only exit interface is specified

```
R1(config)# ip6 route 2001:db8:0:3::/64 g0/0
```

##### Recursive Static Route

Only next hop is specified

```
R1(config)# ip6 route 2001:db8:0:3::/64 2001:db8:0:12:2
```

Recursive because of 2x loopups
1. 1 for dest network
2. 1 for next-hop IP

##### Fully specified Static Route

Both exit interface and next hop are specified 

```
R1(config)# ip6 route 2001:db8:0:3::/64 g0/0 2001:db8:0:12:2
```


##### Routes

**Network Route**

```
R1(config)# ipv6 route 2001:db8:0:3::/64 2001:db8:0:12::2
```

**Host Route**

```
R1(config)# ipv6 route 2001:db8:0:1::100/64 2001:db8:0:12::1
R1(config)# ipv6 route 2001:db8:0:3::100/64 2001:db8:0:12::2
```

**Default Route**

```
R1(config)# ipv6 route ::/0 2001:db8:0:12::1
```

**Floating Static Route**

Higher AD than the primary route

Link-local next hop MUST have next-hop and exit interface specified


##### IPv6 Address Blocks

https://www.ripe.net/media/documents/ipv6-address-types.pdf

**Non-Routable**
FE80::/10 0 link-local unicast addresses
FF02::/16  link-local multicast addresses

FF = Multicast

**Globally Routable**
2000::/3 - 2000 - 3FFF

**Unique Local Unicast Addresses**
FC00::/7 --
FC00::/8
FD00::/8

Not globally routable, but routable within an organization


**Node-Local Multicast Addresses**
FF01::/16



