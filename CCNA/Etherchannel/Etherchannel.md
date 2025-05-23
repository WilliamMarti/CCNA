```
! Show load balance method
Switch# show etherchannel load-balance
```

```
Switch(config)# int po1
Switch(config-if)# port-channel load-balance
dst-ip
src-ip
src-dst-ip
dst-mac
src-mac
src-dst-mac
```


## Methods

##### PaGP

Port Aggregation Protocol
Cisco Proprietary
Dynamic Negotiation creation/maintenance of the Etherchannel (DTP for trunks)

##### LACP

Link Aggregation Protocol
Industry Standard 802.3ad
Dynamic Negotiation creation/maintenance of the Etherchannel

##### Static Etherchannel

No protocol
Interfaces are statically configured to form Etherchannel

Up to 8 interfaces in a single Etherchannel
16 for LACP (8 active / 8 standby mode)

##### PaGP Config

```
Switch(config)# int range g0/0-3
Switch(config-if)# channel-group 1 mode desirable [auto]
```

auto+auto = NO Etherchannel
desirable + auto = Etherchannel 
desirable + desirable = Etherchannel

##### LACP Config

```
Switch(config)# int range g0/0-3
Switch(config-if)# channel-group 1 mode active [passive]
```

passive+passive = NO Etherchannel
active + active = Etherchannel
active + passive = Etherchannel

##### Static Etherchannel

```
Switch(config)# int range g0/0-3
Switch(config-if)# channel-group 1 mode on [passive]
```

on + on = Etherchannel

##### Manually Configure the Negotiation Protocol

```
Switch(config)# int range g0/0-3
Switch(config-if)# channel-protocol ?
lacp
pagp
```

Not really a need to use this when using active / on / desirable / auto

