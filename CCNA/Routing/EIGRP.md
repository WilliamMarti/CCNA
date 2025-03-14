Sends messages using multicast address 224.0.0.10

Only IGP that can do unequal cost load balancing
	By Default it does ECMP over 4 paths

```
R1(config)# router eigrp
R1(config)# no auto-summary
R1(config)# no passive-interface g0/0
R1(config)# network 10.0.0.0
R1(config)# network 172.16.0.0 0.0.0.15 ! wildcard mask
```

Wildcard mask -> Inverted Subnet mask

255.255.255.128 -> 0.0.0.127
255.252.0.0 -> 0.3.255.255

| K Value | Desc        |
| ------- | ----------- |
| K1      | Bandwidth   |
| K2      | Load        |
| K3      | Delay       |
| K4      | Reliability |
| K5      | MTU         |
**Router ID**
1. Manual Config
2. Highest IP Address on Loopback
3. Highest IP on Physical Interface

EIGRP "D" in RIB (show ip route)

**Feasible Distance** - This router's metric value to the router destination

**Reported Distance** - Neighbors metric value to the router destination

![[EIGRP-FD-RD.PNG]]

**Successor** - Route with the lowest metric to the destination (the best)

**Feasible Successor** - Alternate route to the destination (not the best) which meets the *feasibility condition*

**Feasibility Condition** - A route is considered a feasible successor if its reported distance is lower than the successors routes feasible distance.
	Loop prevention mechanism

```
via 10.0.12.2 (28672/28416) ! 28672 = FD
via 10.0.13.2 (30976/28416) ! 28416 = RD
```

##### Unequal Cost Load Balancing

**Variance = 1** - Only ECMP load-balancing will be performed 
**Variable = 2** - Feasible Successor routes with a Feasible Distance up to 2x the successor routes Feasible Distance can be used to load-balance

ONLY for Feasible Successor routes.  If a route doesn't meet the Feasibility Condition it will NEVER be selected, regardless of variance.  