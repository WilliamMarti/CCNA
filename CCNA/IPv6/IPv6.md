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


