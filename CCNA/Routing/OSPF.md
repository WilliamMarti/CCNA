
**Link State**
- Every router creates a "connectivity map" of the network
- All routers share info of interfaces to all routers
- More CPU heavy
- Faster reacting to changes

3x Versions
1. v1 1989 - OLD and not used
2. v2 1998 - Used for IPv4
3. v3 2008 - IPv6

Routers store info about the network in **LSA: Link State Advertisements**

LSA are stored in a **LSDB: Link State Database**

Routers will flood LSAs until all routers in the OSPF area develop the same map of the network (LSDB)


| LSA  |                |
| ---- | -------------- |
| RID  | 4.4.4.4        |
| IP   | 192.168.4.0/24 |
| Cost | 1              |

| LSDB |     |
| ---- | --- |
| LSA  | LSA |
| LSA  | LSA |
| LSA  | LSA |
OSPF uses **areas** to divide the network

**Area** - set of routers and links that share the same LSDB

**Backbone Area (Area 0)** - Area all other areas must connect to

**Internal Routers** - Routers with interfaces in the same area

**Area Border Routers (ABR)** - Router with interfaces in multiple areas.  Recommended to connect to max of 2 areas.

**Intra-Area Route** - Route to a destination in the same OSPF area

Inter-Area Route - Router to a destination in a different area

OSPF areas should be *contiguous*, connected not divided up 


```
! process ID, locally significant
Router(config)# router ospf 1
! Activate OSPF on interfaces that match
Router(config)# network 10.0.10.0 0.0.0.3 area 0
Router(config)# network 10.0.13.0 0.0.0.3 area 0
! Stop sending OSPF "hello" messages out of the interfaces
! Will still tell the neighbors about this network
! always use on interface not running OSPF
Router(config)# passive-interface g2/0
! Need to reload router or clear OSPF process to change
Router(config)# router-id 1.1.1.1
```

OSPF Router ID Choice Order:
1. Configured
2. Highest Loopback
3. Highest IP

**Autonomous System Boundary Router (ASBR)** - OSPF Boundary router that connects the OSPF network to an external network

By using 

```
Router(config)# default-information originate
```

routers become and ASBR

```
Router(config)# maximum-paths <1-32>
! Administrative Distance
Router(config)# distance 85
```

OSPF Metric is **Cost**

Cost is automatically calculated based on bandwidth(speed) of the interface

Calculated by dividing the **Reference Bandwidth** by **Interface Bandwidth**.  **Reference Bandwidth** is 100mbps by Default.  

Examples:

For Fast Ethernet speed at 100.  100RB/100IB = Cost of 1

For Gig Ethernet speed of 1000, 100RB/1000IB = Cost 1 ?

For Ten Gig Ethernet speed of 10000, 100RB/10000IB = Cost of 1 ?

All values less than 1 (fractional / decimal), just equal 1

You can (and should) change the reference bandwidth with:

```
Router(config)# auto-cost reference-bandwidth {mbps} 
```

