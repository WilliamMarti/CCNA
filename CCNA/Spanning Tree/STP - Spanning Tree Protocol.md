'Classic Spanning Tree Protocol is IEEE 802.1D

STP prevents L2 loops by placing redundant ports in a blocking state, essential "disabling" the interface (not the interface is still up/up)

Above disabled interfaces can act as backups 

Interfaces in a blocking state only send to receive STP messages (called BPDUs = Bridge Protocol Data Units)

By selecting which ports are **Forwarding** and which ports are **Blocking**, STP creates a single path to/from each point in the network.  This prevents L2 loops

STP enabled switches send/receive **Hello BPDUs** out of all interfaces.  The default time is **2 seconds** (Hello BPDU sent every 2 seconds)

If a BPDU is received it knows that interfaces is connected to another switch

Routers/PCs **do not** send BPDU's

Switches use one field in the STP BPDU, the **Bridge ID** to elected the **root bridge** for the network

Lowest **Bridge ID** becomes the **root bridge**

Bridge ID
- Bridge Priority - 16 bits
	- Bridge Priority - 4 bits
	- Extended System ID (VLAN ID) - 12 bits
- MAC Address - 48 bits

Bridge Priority

| 32768 | 16384 | 8192 | 4096 |
| ----- | ----- | ---- | ---- |
| 1     | 0     | 0    | 0    |
Extended System ID (VLAN ID)

| 2048 | 1024 | 512 | 256 | 128 | 64  | 32  | 16  | 8   | 4   | 2   | 1   |
| ---- | ---- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0    | 0    | 0   | 0   | 0   | 0   | 0   | 0   | 0   | 0   | 0   | 1   |

In the Default VLAN 1, the default bridge priority is 32769 (32768+1)

STP Bridge Priority can only be changed in units of **4096**

ALL ports on the Root Bridge are **Designated**

When a Switch powers on it assumes it is the Root Bridge

Only gives up its position if it receives a superior (lower) BPDU

Only a topology has converged and all switches agree on a Root Bridge, only the Root Bridge sends BPDU's

Other switches will forward BPDU, but not generate their own

STP Steps

1. Switch with the lowest Bridge ID is elected as the Root Bridge.  All ports on the Root Bridge are Designated Ports (Forwarding State)
2. Each remaining switch will selected ONE of its interfaces to be its **root port**.  
	1. Root Port Selection
		1. The interfaces with the lowest root cost will be the root port.  Root Ports are also in a Forwarding State
		2. Lowest Neighbor ID
		3. Lowest Neighbor Port ID
3. Need to block some ports now
	1. Switch with Lowest Root Cost will make its port Designated
	2. If the Root Cost is the same, the switch with the lowest Bridge ID will make it port Designated
	3. The other switch will make its port non-designated (blocking)



| Speed    | STP Cost |
| -------- | -------- |
| 10 Mbps  | 100      |
| 100 Mbps | 19       |
| 1 Gbps   | 4        |
| 10 Gbps  | 2        |

**Port Roles**
- Root Port
- Designated Port
- Blocked (Non-Designated)

**Loopguard** - Protects the network from loops by disabling a port if it unexpectedly stops receiving BPDUs, ensuing it does not mistakenly enter Forwarding state
	Issue for unidirection links.  Detet unidirection and puts the port in a Broken state

```
Switch(config)# int g0/0
Switch(config-if)# spanning-tree guard loop
```

```
Switch(config)# spaning-tree loopguard default
```

Loopguard vs Rootguard are mutually exclusive.  Each will overwrite the other.    Specific will take effect.  

Root Cost - Total cost of outgoing interfaces to Root Bridge

Every collision domain has a single STP Designated Port

1. Lowest Root Cost makes its port Designated
2. If cost is the same, lowest Bridge ID
3. If there is 2 links to the same switch, lowest **neighbor** Port ID (G0/0 > G0/1 of other side)
4. Other switch will make its port non-designated (Blocked)