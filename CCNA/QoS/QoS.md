
Quality of Service

Phones have an internal 3-port switch:
- Uplink to switch
- Downlink to PC
- Internal to the phone itself

PC and Phone share a single switchport

PC - Phone - Switch

Recommended to separate "voice" traffic and "data" traffic to different vlans

**Audio Quality**


| Type   | Limits        |
| ------ | ------------- |
| Delay  | 130ms or less |
| Jitter | 30ms or less  |
| Loss   | 1% or less    |
```
S1(config)# int g0/0
S1(config-if)# switchport mode access
S1(config-if)# switchport mode access vlan 10
S1(config-if)# switchport mode voice vlan 11
```

QoS is used to manage the following characteristics of network traffic:
1. Bandwidth
2. Delay
	1. src to dest: one way delay
	2. src to dest to return two-way delay
3. Jitter
	1. Variation in one way delay between packets sent by the same application
	2. IP Phones have a jitter buffer to provide a fixed audio delay to audio packets
4. Loss
	1. Percent of packets that dont reach destination
	2. Faulty cables
	3. Can also be caused when devices packet queues get full and discard packets

IF a network device receives messages faster than it can forward them out of the appropriate interface, they messages are placed in a queue.   

![[QOS Queue.PNG]]

**Tail Drop** - Newly arrived packets are dropped when a queue is at max capacity

Tail Drop is bad because it can lead to a TCP Global Synchronization

Creates "waves" of congestion

1. Network congestion 
2. Tail Drop
3. Global TCP Window Size Decrease
4. Network underutilized
5. Global TCP window size increase
6. Go to 1

Solution to Tail Drop: RED - Random Early Detection

When the amount of traffic in the queue reaches a certain threshold, device starts randomly dropping packets from TCP flows

Only those specifically TCP Flow affected, avoid Global TCP Sync

In standard RED, all kinds of traffic are treated the same

**WRED**  - Weighted Random Early Detection, allow control over which packets are dropped depending on the traffic classes.

**Classification** - Organizes network traffic (packets) into traffic classes (categories)
	Fundamental to QoS

Methods to classify Traffic:
1. ACLs - Traffic permitted by ACL will be given certain treatment, others will not
2. NBAR - Network Based Application Recognition.  Performs Deep Packet Inspection, looking beyond the L3 and L4info up to L7 to id the specific traffic
3. PCP - Priority Code Point field if a 802.1Q tag (CoS) can be used to identify high/low priority traffic only when there is a dot1q
4. DSCP - Differentiate Service Code Point.  Field of the IP header


| PCP Value | Traffic Types         | Notes                                |
| --------- | --------------------- | ------------------------------------ |
| 0*        | Best Effort (default) | No guarantee will be delivered       |
| 1         | Background            |                                      |
| 2         | Excellent Effort      |                                      |
| 3*        | Critical Applications | IP Phone mark call signaling as PCP3 |
| 4*        | Video                 |                                      |
| 5*        | Voice                 | Mark actual Voice traffic as PCP5    |
| 6         | Internetwork Control  |                                      |
| 7         | Network Control       |                                      |


PCP is in a dot1q header so it can only be used over the following connections
- Trunk Links
- Access Link with Voice VLANs

#### DSCP

ToS Byte - Type of Service

DSCP+ECN

##### DF(Default Forwarding)
Best Effort
Mark = 0

000000

##### EF (Expedited Forwarding)
Requires low latency /jitter
Mark 46
101110

##### AF (Assured Forwarding)
All packets in a class have the same priority.  Within each class, there are levels of *drop precedence*

Higher Drop Precedence = more likely to drop during congestion

 0/1 0/1 0/1 0/1 0/1
| class x       | drop y |
AFXY

Formula to convert from AF to decimal DSCP:

AFXY -> 8x + 2Y

##### CS (Class Selector)

Defines eight DSCP values for backwards compatibility with IPP

There's bits that were added for DSCP are set to 0 and originally IPP bits are used to make 8 values

CH# -> DSCP = CS# x 8
CS1 = DSCP 8
CS2 = DSCP 16
CS3 = DSCP 24

#### RFC4954

Developed with Cisco to bring all these values together and standardize their use


| Traffic Class      |      |
| ------------------ | ---- |
| Voice Traffic      | EF   |
| Interactive Video  | AF4X |
| Streaming Video    | AF3X |
| High Priority Data | AF2X |
| Best Effort        | DF   |
