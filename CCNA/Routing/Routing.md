**Network Route** - Route to a network/subnet

**Host Route** - Route to a specific Host or Address /32

**IGP** - Interior Gateway Protocol. Within an AS (Autonomous System)

**EGP** - Exterior Gateway Protocol.  Between AS's.  Path Vector -> BGP

**Distance Vector** - 
RIP - Routing Information Protocol
EIGRP - Enhanced Interior Gateway Routing Protocol

**Link State** -
OSFP - Open Shortest Path First
IS-IS - Intermediate System to Intermediate System

##### Distance Vector Protocols 

Were invented first

Send
1. Known destination networks
2. metric to reach their known destination networks

Calling "Routing by Rumor"

Route only knows the info neighbor tells them

Distance -> Metric
Vector -> Direction / Next Hop


| IGP   | Metric          |                                                                                                                                                                             |
| ----- | --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| RIP   | Hop Count       | Each router in the path counts as one 'hop'.  The total  metric is the total number of hops to the destination.  Links of all speeds are equal                              |
| EIGRP | Bandwidth/Delay | Complex forumula that can take into account many values.  By default, the bandwidth of the slowest link in the route and the total delay of all links in the route are used |
| OSPF  | Cost            | Cost of link is based on bandwidth.  The total metric is the total cost of each link in the route                                                                           |
| IS-IS | Cost            | The total metric is the total cost of each link in the route.  The cost of each link is not automatically calculated by default.  All links have a cost of 10 by default.   |





