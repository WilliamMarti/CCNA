
| Preamble | SFD | Destination | Source | 802.1Q(Inserted) | Type/Length |
| -------- | --- | ----------- | ------ | ---------------- | ----------- |
802.1Q - 16 **bytes**


802.1Q Tag has 2x fields:
1. TPID - Tag protocol identifier
	1. 16 bits
	2. Always 0x8100 
		1. Indicate the frame is 801.Q tagged
2. TCI - Tag control information
	1. PCP - Priority Code Point
		1. 3 bits
		2. CoS - Class of Service
	3. DEI - Drop eligible indicator
		1. 1 bit
	4. VID - VLAN identifier
		1. 12 bits

[[802.1Q Header Structure.canvas|802.1Q Header Structure]]

Normal Vlans: 1-1005
Extended Vlans: 1006-4094

0 - Reserved
1002-1005 Reserved (Token Ring/FDDI)
4096 - Reserved

Native Vlan = 1
Untagged frames on a trunk port it assumes the frame belongs to the native vlan

###### **Configuring a Trunk port**
```
Switch(config)# int g0/0
Switch(config-if)# switchport trunk encapsulation dot1q
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 10,30
Switch(config-if)# switchport trunk native vlan 1001
```

Sub-interface number SHOULD match the vlan

**ROAD** - Router on a Stick

**SVI** - Switched Virtual Interface

###### **Enable routing on a L3 Switch**
```
Switch(config)# ip routing
```

###### Allow port to act as a L3 interface
```
Switch(config)# int g0/0
Switch(config-if)# no switchport
```

Creating SVI will **not** auto create a L2 Vlan

L3 Switch must have at least 1 access port in the vlan  in an up/up state AND/OR one trunk port that allows the vlan that is in an up/up state

SVI must not be shutdown


