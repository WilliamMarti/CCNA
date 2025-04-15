IPv4 running out of space

3x Solutions
1. CIDR
2. Private IPv4 addresses
3. NAT

RFC1918 (Private Address Space)
- 10.0.0.0/8 10.0.0.0 - 10.255.255.255 Class A
- 172.16.0.0/12 172.16.0.0 - 172.31.255.255 Class B
- 192.168.0.0 192.168.0.0 - 192.168.255.255 Class C

Private IP CANNOT be used over the Internet

NAT is used to modify the source and/or destination of packets

##### Source NAT

![[source-nat.PNG]]

Static NAT involves configuring one-to-one mappings of private IPs addresses to public IP address

**Inside Local** - IP address mapped to an Inside Global IP.  Inside host from the perspective of the local network.  Usually Private IP

**Inside Global** - IP Address of the Inside Host from the perspective of outside hosts
	IP Address of the inside Host AFTER NAT, usually public IP

```
R1(config)# int g0/1
R1(config-if)# ip nat inside
R1(config-if)# int g0/0
R1(config-if)# ip nat outside
R1(config-if)# exit
R1(config)# ip nat inside source static 192.168.0.167 100.0.0.1
R1(config)# ip nat inside source static 192.168.0.168 100.0.0.2
```

```
R1# show ip nat translations
```

**Outside Local** - IP of the outside host, from the perspective of the local network

**Outside Global** - IP of the outside host, from the perspective of the outside network

```
R1# clear ip nat translations *
```

Static NAT entries never go away

```
R1# show ip nat statistics
```

##### Dynamic NAT

Router dynamically maps inside local addresses to inside global addresses as needed

An ACL is used to identify which traffic should be translated.  If source IP is permitted by the ACL the source IP will be translated
If Source IP is denied traffic will NOT be translated
	Traffic isn't dropped

A **NAT Pool** is used to define the available inside global addresses that can be used

Although dynamically assigned mappings are still one-to-one
	One IL per IG

If there aren't enough IG IPs available, its called **NAT Pool Exhaustion**

If none available, router will drop the packet.  Host will be unable to access outside networks

Dynamic NAT entries will timeout, or can clear them manually. 

```
R1(config)# int g0/1
R1(config-if)# ip nat inside
R1(config-if)# int g0/0
R1(config-if)# ip nat outside
R1(config-if)# exit
R1(config)# access-list 1 permit 192.168.0.0 0.0.0.255
R1(config)# ip nat pool POOL1 100.0.0.0 100.0.0.255 prefix-length 24
R1(config)# ip nat inside source list 1 pool POOL1
```

##### PAT

Port Address Translations (aka NAT Overload)

Translates both the IP Address and the port numbers (if necessary)

By using a unique port number for each communication flow, a single Public IP Address can be used by many different internal hosts (port numbers are 16 bits = over 65,000 available port numbers)

![[PAT.PNG]]

Source Port kept for PC1

Source Port Translated for PC2

 ##### Configure PAT

```
R1(config)# int g0/1
R1(config-if)# ip nat inside
R1(config-if)# int g0/0
R1(config-if)# ip nat outside
R1(config-if)# exit
R1(config)# access-list 1 permit 192.168.0.0 0.0.0.255
R1(config)# ip nat pool POOL1 100.0.0.0 100.0.0.255 prefix-length 24
!
R1(config)# ip nat inside source list 1 pool POOL1 overload
! OR 
R1(config)# ip nat inside source list 1 interface g0/0 overload
```


##### **PAT NAT Config Steps**

1. Assign Inside Interface
2. Assign Outside Interface
3. Create ACL for Inside Local Address space
4. Create NAT POOL for Inside Global
5. Add NAT config tying together ACL and NAT POOL with overload
