#### Standard ACLs (Access Control Lists)

Multiple uses

Functions as a packet filter, permit or discard traffic

Can filter on:

- Source IP
- Destination IP
- Source L4 Port
- Destination L4 Port

ACLs are configured globally (global config mode)

Ordered sequnce of ACEs(Access Control Entries)

ACL must be applied to an interface to take effect.  Applied **INBOUND** and **OUTBOUND**

Process ACE, in order, from top to bottom

If a packet match 1 ACE, router takes the action and stop processing the ACL.  All below will be ignored

Max of 1x ACL *per direction*

**Implicit Deny** - "Hidden" deny-all at end of ACL

**Standard ACLs** - Match on Source IP only
- Standard Numbered ACLs
- Standard Named ACLs

**Extended ACLs** - Match on source/destination IP, source/destination port 
- Extended Numbered ACLs
- Extended Named ACLs

#### Standard ACLs

Traffic match based on Source IP **only**

Numbered are identified by a number (ACL 1, ACL 2)

Standard ACLs can use numbers

- 1-99 (original)
- 1300-1999 (added later)

```
R1(config)# access-list number {deny|permit} ip wildcard-mask
R1(config)# access-list 1 deny 1.1.1.1 0.0.0.0
! OR
R1(config)# access-list 1 deny 1.1.1.1
! OR
R1(config)# access-list 1 deny host 1.1.1.1
```

```
R1(config)# access-list 1 permit any
! OR
R1(config)# access-list 1 permit 0.0.0.0 255.255.255.255
```

```
R1(config)# access-list 1 remark # TEST REMARK #
```

```
R1# show access-lists
!
R1# show ip access-lists
!
R1(config)# do show run | i access-list
```

Apply to Interface

```
R1(config)# ip access-group 1 {in|out}
```

**Standard ACLs** Should be applied as **close** to the **destination** as possible.  

**Named ACLs** are identified with a name, Ex: BLOCK_BOB

```
R1(config)# ip access-list standard BLOCK_BOB
R1(config)# 1 permit 10.10.10.0 0.0.0.255
R1(config)# 2 permit any
R1(config)# remark EXAMPLE COMMENT
```


```
R1(config)# int g0/0
R1(config-if)# ip access-group BLOCK_BOB in
```

In modern IOS you can configure numbered ACLs in the exact same way as named ACLs

```
R1(config)# ip access-list standard BOB
R1(config)# deny 192.168.1.1
R1(config)# permiy any
```

OR

```
R1(config)# ip access-list standard 1
R1(config)# deny 192.168.1.1
R1(config)# permiy any
```

```
! 1 = Access list numner
! 10 = Change the sequence num of the first entry
! 10 = Add 10 for every entry after 10
R1(config)# ip access-list resequence 1 10 10
```


##### Extended Numbered ACLs

- 100-199
- 2000-2699

```
R1(config)# access-list number [permit|deny] protocol src-ip dest-ip
```

IP Protocol Numbers:
- 1 = ICMP
- 6 = TCP
- 17 = UDP
- 88 = EIGRP
- 89 = OSPF

```
! Allow all traffic
R1(config)# permit ip any any
```

```
! Prevent 10.0.0.0/8 from sending UDP traffic to 192.168.1.1/32
R1(config)# deny udp 10.0.0.0 0.255.255.255 host 192.168.1.1
```

```
! Prevent 172.168.1.1/32 from pinging hosts in 192.168.0.0/24
R1(config)# deny icmp host 172.16.1.1 192.168.0.0. 0.0.0.255
```

eq = equals
gt = greater
lt = less than
neq = Not

range 80-100 = from 80 to port 100

TCP

ack = match TCP ACK flag
fin = match TCP FIN flag
syn = match TCP SYN flag
ttl = match specific TTL value
dscp = match specific DSCP value

Closest to the source as possible

