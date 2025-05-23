[Cisco Wireless LAN Controller Configuration Guide, Release 7.3](https://www.cisco.com/c/en/us/td/docs/wireless/controller/7-3/configuration/guide/b_cg73/b_wlc-cg_chapter_011.html)
##### AAA Override

The AAA Override option of a WLAN enables you to configure the WLAN for identity networking. It enables you to apply VLAN tagging, Quality of Service (QoS), and Access Control Lists (ACLs) to individual clients based on the returned RADIUS attributes from the AAA server.

[AAA Override](https://www.cisco.com/c/en/us/td/docs/wireless/controller/7-4/configuration/guides/consolidated/b_cg74_CONSOLIDATED/m_configuring_aaa_override.pdf)


On the controller, enable the **Allow AAA Override** configuration parameter using the GUI or CLI





##### Configure

```
! Enable HTTP(S) web client
WLC1# config network secureweb enable
```


##### Management Interface

Default interface for in-band management of the controller and connectivity to Enterprise Service such as AAA servers.  

Used for communication between the controller and access points

Only consistent "pingable" in-band interface to control all controller-to-access point communications


##### AP-Manager

Optional on 5500 WLCs
	Management interface acts as the AP-Manager interface

Handles L3 communication between Controller and Lightweight APs after the access points have joined the controller

##### Virtual Interface

Supports:
- Mobility management
- Dynamic Host Configuration Protocol (DHCP) relay
- Embedded Layer 3 security such as 
	- Guest Web Authentication
	- VPN termination

The virtual interface IP address is used only in communications between the controller and wireless clients. It never appears as the source or destination address of a packet that goes out a distribution system port and onto the switched network. For the system to operate correctly, the virtual interface IP address must be set (it cannot be 0.0.0.0), and no other device on the network can have the same address as the virtual interface. Therefore, the virtual interface must be configured with an unassigned and unused gateway IP address. The virtual interface IP address is not pingable and should not exist in any routing table in your network. In addition, the virtual interface cannot be mapped to a physical port.


##### Service Port

Reserved out out-of-band management.

Cannot carry 802.1q tags

##### Dynamic Interfaces

Created by users, analogous to VLANs for wireless LAN clients

All Dynamic Interfaces must be on different VLAN or IP subnets from all other interfaces configured on the port

![[Pasted image 20250407191300.png]]


##### Link Aggregation

LAG requires the EtherChannel to be configured for 'mode on' on both the controller and the Catalyst switch.
	LACP and PAgP are not supported

Only 1 LAG group supported


##### Layer 2 Security 

PSK - Can accept ASCII or HEX values from 8 to 63 characters long
CCKM - Cisco Centralized Key Management
802.1X - Used with RADIUS/EAP





**Layer 2 Security:**

**None** - Disable Layer 2 security and allow open authentication to the WLAN
WPA+WPA2 - Enable Layer 2 security by using WPA or WPA2
8021.1X - Enable Layer 2 security by using EAP authentication combined with dynamic  WEP key
Static WEP - Enable Layer 2 security using a staic WEP key
Static WEP + 802.1X - Layer 2 security by using either a static WEP key or EAP authentication
CKIP - which enable layer 2 security by using the Cisco Key Integrity Protocol (CKIP)

**Layer 3 Security:**

None - Disable Layer 3 security no matter which Layer 2 security option is configured and regardless of whether you are configuring a WLAN or Guest LAN
IPSec - Enable Layer 3 security for WLANS by using IPSec
VPN Pass-Through - Layer 3 security for WALNs by allowing a client to establish a connection with a specific virtual private network server
Web Authentication - Layer 3 security for GUEST LANs by prompting for a user name and password when a client connects to the network
Web Passthrough - Direct access to the network for GEUST LANs without prompting for a user name and password