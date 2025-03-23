
Power over Ethernet

**PSE** - Power Sourcing Equipment (switch)
**PD** - Powered Devices (IP Phone/AP)

Power Policing

```
S1(config)#int g0/0
S1(config-if)# power inline police
S1(config-if)# end
```

```
S1# show power inline police g0/0
```


| Name               | Standard Number | Watts | Powered Wires |
| ------------------ | --------------- | ----- | ------------- |
| Cisco Inline Power | N/A             | 7     | 2             |
| PoE (Type 1)       | 802.3af         | 15    | 2             |
| PoE+ (Type 2)      | 802.3at         | 30    | 2             |
| UPoE (Type 3)      | 802.3bt         | 60    | 4             |
| UPoE+ (Type 4)     | 802.3bt         | 100   | 4             |
