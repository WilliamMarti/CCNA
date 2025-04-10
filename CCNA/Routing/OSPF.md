
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

**Inter-Area Route** - Router to a destination in a different area

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

RB / IB

Examples:

For Fast Ethernet speed at 100.  100RB/100IB = Cost of 1

For Gig Ethernet speed of 1000, 100RB/1000IB = Cost 1 ?

For Ten Gig Ethernet speed of 10000, 100RB/10000IB = Cost of 1 ?

All values less than 1 (fractional / decimal), just equal 1

You can (and should) change the reference bandwidth with:

```
Router(config)# auto-cost reference-bandwidth {mbps} 
```

Should configure the same Reference Bandwidth for every Router

**OSPF Cost to a Destination** is the total cost of the outgoing/exit interfaces

```
Router(config-if)# ip ospf cost {1-65535}
```

^ will take precedence over auto-calculated costs

speed != bandwidth

```
Router(config-if)# bandwidth {kbps}
```

```
Router# show ip ospf brief
```

hello timer = 10s

Hello Multicast Address = 224.0.0.5

IP Header Protocol Field OSPF = **89**

##### **OSPF Neighbor States**

1. Down
2. Init State
	1. Hello Packet Received, but own Router ID is not in Hello Packet
3. 2-Way
	1. Neighbor sends Hello with BOTH Router IDs
	2. DR (Designated Router) and BDR (Backup Designated Router) will be selected at this point
		1. Highest Interface Priority
		2. Highest Router ID
4. Exstart
	1. Determine who is master/slave
		1. This is different than BR / BDR
		2. Higher Router ID (RID) will be the master and initiate the exchange of DBD's (Database Description)
5. Exchange
	1. Routers exchange DBD packets which contain a list of the LSA's in the LSDB
	2. Just basic info
6. Loading
	1. Routers send LSR (Link State Requests) to request LSA they don't have
7. Full
	1. Full OPSF adjacency and identical LSDBs



```
Router(config)# int g0/1
Router(config-if) ip ospf 1 area 0
```


##### **OSPF Message Types**

| Num | Name                               |
| --- | ---------------------------------- |
| 1   | Hello                              |
| 2   | Database Description               |
| 3   | Link State Reqeust (LSR)           |
| 4   | Link State Update (LSU)            |
| 5   | Link State Acknowledgement (LSACK) |

OSPF Network Types refer to the type of connection between OSPF neighbors

5 OFPS Network Types:

1. Broadcast
	1. Enabled by default on **Ethernet** and **FDDI** (FIber Distributed Data Interfaces)
2. Point-to-Point
	1. Enabled by default on PPP and HDLC (High-level Data Link Control) interfaces
3. Non-Broadcast
	1. Enabled by default on Frame-Relay and X.25 interfaces
4. Point-to-Multipoint Broadcast
5. Point-to-Multipoint Non-broadcast


###### **Broadcast** 

Dynamically discover neighbors by sending / listening to OSPF Hello Messages using multicast address 224..0.0.5

**DR** and **BDR** must be elected on each subnet.  Only DR if there are no OSPF neighbors

Routers that are not a DR or BDR are a DROTHER

###### **Point-to-Point**

Default for serial interfaces using PPP or HDLC encapsulation

DR and BDR are not elected.  Only 2 routers so no point
Form FULL adjacency with each other

###### **Nonbroadcast**

Nonbroadcast networks do not allow multicast, need manual configuration of OSPF neighbors with the `neighbor` command

`ip ospf network non-broadcast`

###### **Point-to-Multipoint Broadcast

Similar to point-to-point but have timers as:

Hello: 30s
Dead 120s

`ip ospf network point-to-multipoint`

###### **Point-to-Multipoint Non-Broadcast

Do not allow multicast, need manual configuration of OSPF neighbors with the `neighbor` command

`ip ospf network point-to-multipoint non-broadcast`
##### **DR/BDR election**

1. Highest OSPF interface priority
2. Highest OSPF Router ID

First place is DR
Second place is BDR

![[OSPF-BR-BDR.PNG]]

Default OSPF interface priority is 1 on all interfaces

DR/BDR election is "non-premptive", once the DR/BDR are selected they will keep the role until OSPF is reset, the interface fails, or is shutdown.

DROther **do not** exchange LSAs

Messages to DR/BDR routers are to multicast address **224.0.0.6**

DR/BDR for FULL adjacency with **ALL** routers
DROthers form FULL adjacney with the DR/BDR

```
Nbrs F/C F=Full adj C=Total Neighbor
2/3
```

#### **OSPF Neighbors**

1. Areas **must** match
2. Interfaces must be in the same area
3. OSPF process must not be shutdown
4. Router ID's must be unique
5. Hello/Dead timers must match
	1. Configured on interface

```
Router(config-if)# ip ospf hello-interval
Router(config-if)# ip ospf dead-interval
```

6. Auth settings must match

```
! enable ospf auth
Router(config-if)# ip ospf authentication
Router(config-if)# ip ospf authentication-key {xyz}
```

7. IP MTU settings must match
```
Router(config-if)# ip mtu <68-1500>
```
8. OSPF Network Types
	1. Warning: Routers can become neighbors but won't work properly


OSPF LSA Types:
1. Type 1 - Router LSAs
2. Type 2 - Network LSAs
3. Type 5 - AS External LSAs

**Type 1 (Router)**
Every Router generates this type
ID's Router using its **Router ID**
Lists networks attached to the Routers OSPF activated interfaces

**Type 2 (Network)**
Generated by the DR of each "multi-access" (broadcast)

**Type 5 (AS-External)**
Generated by ASBR (Autonomous System Border Router) to describe routes to destinations outside of the AS (OSPF Domain)




