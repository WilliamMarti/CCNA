
**DCE** - Data Communication Equipment.  Sets the clock rate
**DTE** - Data Terminal Equipment

Ethernet uses speed
Serial uses clock rate

Default encapsulation is HDLC (cHDLC for Cisco) or PPP

Encapsulation must match on both sides

```
Router# show controllers 0/0
```

```
Router(config)# int g0/0
Router(config-if)# ip ospf network <network-type>
```

Hello Timers


|             | Broadcast | P2P | Non-Broadcast |
| ----------- | --------- | --- | ------------- |
| Hello Timer | 10s       | 10s | 30s           |
| Dead        | 40s       | 40s | 120s          |




