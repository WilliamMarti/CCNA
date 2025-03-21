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



