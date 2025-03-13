https://www.cisco.com/c/en/us/support/docs/lan-switching/spanning-tree-protocol/24062-146.html

| Name                   | Protocol | IEEE   |
| ---------------------- | -------- | ------ |
| Spanning Tree          | STP      | 802.1d |
| Rapid Spanning Tree    | RSTP     | 802.1w |
| Multiple Spanning Tree | MSTP     | 801.1s |

## **PVST+**

Cisco upgrade  to RSTP(802.1d)
Each VLAN has own STP instance
Can load balance by blocking different ports in each VLAN

## **RPVST+**

Cisco's upgrade to 802.1w
Each VLAN has own STP instance

Each VLAN has its own VLAN instance

STP needs 50s to respond to change

RPVST+ can load balance

RSTP is NOT time based, it is bridge to bridge handshake based

RPVST+ has the same rules for Root Bridge and Root Ports and Designated Ports. 

| Speed    | RSTP Cost | STP Cost |
| -------- | --------- | -------- |
| 10 Mbps  | 2,000,000 | 100      |
| 100 Mbps | 200,000   | 19       |
| 1 Gbps   | 20,000    | 4        |
| 10 Gbps  | 2,000     | 2        |
| 100G     | 200       | X        |
| 1T       | 20        | X        |


###### **STP Port States**

| State          | Send / Receive BPDUs | Frame Forwarding | MAC Learning | Stable/Transitive |
| -------------- | -------------------- | ---------------- | ------------ | ----------------- |
| Blocking       | No / Yes             | No               | No           | Stable            |
| Listening      | Yes / Yes            | No               | No           | Transitive        |
| **Learning**   | Yes / Yes            | No               | Yes          | Transitive        |
| **Forwarding** | Yes / Yes            | Yes              | Yes          | Stable            |
| Disabled       | No / No              | No               | No           | Stable            |
###### **RPVST+ Port States**

| State          | Send / Receive BPDUs | Frame Forwarding | MAC Learning | Stable/Transitive |
| -------------- | -------------------- | ---------------- | ------------ | ----------------- |
| Discarding     | No / Yes             | No               | No           | Stable            |
| **Learning**   | Yes / Yes            | No               | Yes          | Transitive        |
| **Forwarding** | Yes / Yes            | No               | Yes          | Transitive        |
Shutdown = Discarding
Enabled but blocking = Discarding

**Port Roles**
- Root Port
- Designated Port
- Alternate Port
	- Was Non-Designated Port in STP
- Backup Port
	- Was Non-Designated Port in STP

Alternate is a backup to the Root Port

Backbone Fast / Uplink Fast STP config -> Built into RSTP

**Backbone Port Role** - Discarding port that receives a superior BPDU **from another switch on the same interface** 
	Only happens when 2 switch interfaces are connected to the same collision domain (Hub)

RSTP version number = 2
STP version number = 0

Classic BPDU  uses 2 bits, 1 and 8th
RSTP uses all 8 bits

Classic STP, only the Root Bridge originates BPDUs
RSTP ALL switches originate and send BPDUs from Designated Ports (2 seconds)

Classic lost switch = 10 interfaces @ 2 sec per = 20 seconds
RSTP lost switch = 3 BPDUs @ 2 sec per = 6 seconds
	Flush / Delete all interfaces

**Link Types**
1. Edge = Connected to end host
2. Point-to-Point = Connected between 2 switches
3. Shared = Connection to a Hub, half-duplex


```
Switch(config)# spanning-tree mode rapid-pvst
```

```
Switch(config)# int g0/0
Switch(config)# spanning-tree link-type point-to-point
```


802.1w -> RSTP -> Rapid PVST+
802.1s -> STP
802.1s -> MSTP (Multiple STP)
802.1d -> PVST+ (Cisco)

**RSTP Port Roles**
- Root
- Designated 
- Alternate
- Backup

**Link Types**
- Edge
- Point-to-point
- Shared

**STP**
* Discarding
* Listening
* Learning
* Forwarding
* Disabled  