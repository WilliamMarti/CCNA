
Benefits
- Human error reduced (typos)
- Network becomes more scalable.  Net deployments, network wide changes
- Network wide policy compliance (standard configs / software versions)
- Improved efficiency compliance (standard configs / software versions)
- Improved efficiency of network operations reduces the opex
	- Each task requires fewer man-hours

Tools
- SDN
- Ansible
- Puppet
- Python

**Data Plane** - All task involved in forwarding user data/traffic from one interface to another

**Control Plane** - Function that build ARP/MAC Tables to control traffic flow
	Controls what Data Plane does.  OSPF/STP don't control forwarding of data packets themselves

In traditional networking the data and control planes are *distributed* among each network device

**Management Plane** - Consists of protocols used to manage devices SSH/Telnet.  Doesn't directly affect forwarding of messages
	NTP/SNMP

Operations of Management and Control plane are usually managed by the CPU

CPU is typically slow(relatively)

ASIC (Application-Specific Integrated Circuit) is used for Data Plane

MAC Table is stored in TCAM (Ternary Content Addressable Memory) 
	aka CAM Table

##### Software Defined Networking

Approach to networking that centralized the control plane into an application called a Controller
	Like WLCs

Traditional Networking uses a distributed architecture
	Ex. OSPF running on each router

SDN Controller centralizes control plane functions like calculating routes

Controller can interact programmatically with the network devices using API(Application Programming Interface)

**SBI (South Bound Interface)** Used to communicate between controller and network devices it controls

Consists of communication protocol and an API

SBI Examples:
- OpenFlow
- Cisco OpFlex
- Cisco onePK (Open Network Environment Platform Kit)
- NETCONF

**NBI (Northbound Interface)** 

SBI gathers info from the devices
- Devices on the network
- Topology 
- Available interfaces
- Configurations
NBI allows us to interact with the **controller**

A REST API is used on the controller as an interface for apps to interact with it

REST = Representation State Transfer



