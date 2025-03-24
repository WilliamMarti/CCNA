
Allows you to control source MAC Address that are allowed to enter a switchport

If unauthorized source MAC is received, an action is taken 
	Default action is to put the interface in a *err-disabled* state

Default is to allow 1 MAC Address
- Can configure the allowed MAC Address
- Otherwise Switch will allow the first source MAC that enters interfaces

Can change the max number of allowed MACs
	Useful for PC+Phone

Allows Net Admins to control devices that are allow to access the network

Not a perfect solution, MAC spoofing is easy

Port Security's  ability to control the number of MACs on an interface is more useful
	Protect against DHCP starvation

Switchport must be in *access mode*

```
S1(config)# int g0/0
S1(config-if)# swtichport mode access
S1(config-if)# switchport port-security
```

##### Err-Disable Recovery

```
S1# show errdisable recovery
```

By default *all* are disabled
300 seconds is the default time

Disconnect Unauthorized Device

```
S1(config)# int g0/0
S1(config-if)# shut
S1(config-if)# no shut
```


```
S1(config)# errdisable recovery cause psecure-violation
S1(config)# errdisable recovery interval 180
```

##### Violation Modes

**Shutdown**  - Effectively shuts down the port by placing it in an err-disabled state
- Generates syslog
- Violations counter is set to 1
**Restrict** - Switch Discards traffic from unauthorized MACs.
- Interface is NOT disabled
- Generates syslog/SNMP message for each unauthorized MAC
- Violation counter is incremented by 1 for each violation
**Protect** - Switch discards traffci from unauthorized MAC.
- Interface is *not* disabled
- Does NOT generate syslog/SNMP messages


```
S1(config-if)# switchport port-security violation restrict
S1(config-if)# switchport port-security violation protect
```

##### Secure MAC Aging

Secure MACs will not age out
Aging Timing: 0 minutes

```
S1(config-if)# switchport port-security aging timing <minutes>
```

Aging Types:
- **Absolute** - After a secure MAC is received, time runs and the MAc is removed after the time expires.  Even if the switch continues receiveing frames from that source MAC
- **Inactivity** - After a secure MAC is learned the aging timer starts but is reset every time a frame is received from that sources secure MAC

```
S1(config-if)# switchport port-security aging type {absoulte|inactivity}
```

**Secure Static** - MAC Aging is disabled by default

```
S1(config-if)# switchport port-security aging static
```

##### Sticky Secure MAC Address

```
S1(config-if)# switchport port-security mac-address sticky
```

When enabled, dynamically learned MAC addresses will be added to the running config like 

```
swithcport port-security mac-address sticky <mac-address>
```

Sticky secure MAC addresses will never age out

Need to save running config to startup config

When issues al currently dynamically-learned MAC will be converted to sticky secure

If you issues "no" all sticky secure will be converted to regular dynamically learned secure MACs

Secure MACs are added to the MAC table as normal

Will have a type of STATIC

Dynamically learned MAC will have a type of DYNAMIC

```
S1# show mac address-table secure
```

