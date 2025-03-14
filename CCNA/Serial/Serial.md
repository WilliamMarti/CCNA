**DCE** - Data Communications Equipment.  Set clock rate
**DTE** - Data Terminal Equipment

Ethernet uses speed
Serial uses *clock rate* 

Default encapsulation is HDLC (cHDCL for Cisco)
Encapsulation must match on both ends

```
R1# show controllers 0/0
```

```
! Set OSPF Network Type
R1(config)# ip ospf network ?
```


|             | Broadcast | Point-to-Point | Non-Broadcast |
| ----------- | --------- | -------------- | ------------- |
| Hello Timer | 10s       | 10s            | 30s           |
| Dead Timer  | 40s       | 40s            | 120s          |
