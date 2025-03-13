

###### **Port Config**
```
!
interface FastEthernet0/3
switchport mode access
switchport port-security
switchport port-security violation restrict
switchport port-security aging time 60
!
```

###### **Port-Security Status**
```
SW1#show port-security int f0/3
Port Security : Enabled
Port Status : Secure-up
Violation Mode : Restrict
Aging Time : 60 mins
Aging Type : Absolute
SecureStatic Address Aging : Disabled
Maximum MAC Addresses : 1
Total MAC Addresses : 1
Configured MAC Addresses : 0
Sticky MAC Addresses : 0
Last Source Address:Vlan : 000D.BD75.1814:1
Security Violation Count : 2
```

