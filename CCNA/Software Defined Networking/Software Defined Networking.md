
3x Layers:
- **Application Layer** - Scripts/Apps that tell the SDN controllers what network behaviors are desired
- **Control Layer** - SDN Controllers that receive and process instructions from the application layer
- **Infrastructure Layer** - Network devices that are responsible for forwarding messages across the network


**Cisco SD-Access** - SDN of LANs

**Cisco DNA(Digital Network Architecture)** - Controllers for SD-Access

**Underlay** - Underlying physical network of devices and connections (including wired and wireless) which provide IP connectivity

**Overlay** - Virtual network built on top of the physical underlay network
	SD-Access uses VXLAN (Virtual Extensible LAN) to build tunnels

**Fabric** - Combination of the overlay and underlay Physical+Virtual as a whole

##### SD-Access Underlay

Underlay supports VXLAN tunnels of the overlay

3x Roles:
1. Edge Nodes - Connect to end hosts
2. Border Nodes - Connect to devices outside of the SD-Access domain (WAN Routers)
3. Control Nodes - Use LISP (Locator ID Separation Protocol) to perform various control plane functions

You can add SD-Access on top of existing network (brownfield)

New deployments (greenfield) will be configured by DNA Center to use optimal SD-Access underlay

- All switches are Layer 3 and use IS-IS as their routing protocol
- All Links between switches are routed ports.  No more STP
- Edge nodes (access switches) act as default gateway of end hosts

##### SD-Access Overlay

LISP provides the control plane of SD-Access
- A list of mappings  of EID (Endpoint Identifiers) to RLOCs (routing locators) is kept)
- EIDs identify end hosts connected to edge switches, and RLOCs identify the edge switch which can be used to reach the end host

Cisco TrustSec(CTS) provides prolicy control (QoS, security)

VxLAN provides the data plane of SD-Access

##### Cisco DNA Center

SDN Controller

Network Manage in a traditional network

On Cisco UCS Hardware

Enables "Intent Based Networking"

