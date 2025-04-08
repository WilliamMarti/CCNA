
802.11 Frame Format

**Frame Control** - Provides information such as the message type and subtype

**Duration/ID** - Depending on the message type, this field can indicate
- The time in microseconds the channel will be dedicated for transmission of the frame
- and identifier for the association(connection)

**Addresses** - Up to 4 addresses can be present on a 802.11 frame which are present depends on the message type
- Destination Address (DA) Final recipient of the frame
- Source Address (SA) Original sender of the frame
- Receiver Address (RA) Immediate recipient of the frame
- Transmitter Address (TA) Immediate sender of the frame

**Sequence Control** - Used to reassemble fragment and eliminate duplicate frames. 

**QoS Control** - Used in QoS to prioritize certain traffic.

**HT(High Throughput) Control** - Added in 802.11n to enable High Throughput operations
- 802.11n is also known a "HT" Wi-Fi
- 802.11ac is also known as "Very HT" Wi-Fi

**FCS (Frame Check Sequence)** - Same as in an Ethernet frame used to check for errors

##### Association Process

APs bridge traffic between wireless stations and other devices

3x 802.11 connected states:
1. Not authenticated, not associated
2. Authenticated, no associated
3. Authenticated, and associated

A station must be authenticated and associated with the AP to send traffic.  

![[association-request.PNG]]

2x ways for a station to scan for a BSS:
- **Active** - Station sends probe requests and listens for a probe response from an AP
- **Passive** - Station listens for a beacon message from an AP

Beacons are send periodically by APs to advertise the BSS

##### 802.11 Message Types

**Management** - Used to manage BSS
- Beacon
- Probe request, probe response
- Authentication
- Associate request, association response

**Control** - Used to control access to the medium (radio frequency).  Assists with delivery of management and data frames
- RTS (Requests to Send)
- CTS (Clear to Send)
- ACK

**Data** - Used to send actual data packets

##### Wireless AP Deployments

3 Types:
1. Autonomous
2. Lightweight
3. Cloud-Based

**Autonomous**  - Configured individually
- Configured via console, telnet/ssh, or HTTPS
- All parameters configured individually

Connect to the wired network with a trunk port

**Lightweight APs** - Handles "real-time" operation like transmitting/receiving RF traffic, encryption/decryption of traffic, sending beacons/probes.

**WLC** - Wireless Lan Controller.  Handles RF management, security/QoS, client auth, client association/roaming, etc

Called *split-mac architecture*

WLC centrally configures lightweight APs

WLC can be in same or different VLANs

WLC and LWAP auth each other using digital certificate installed on each device (X.509 standard certs)

##### CAPWAP

Control and provisioning of Access Points.

Protocol used to communicate between LWAP and WLC.  Based on an older protocol, LWAPP(Lightweight Access Point Protocol)

Two tunnels are created between each AP and the WLC
- **Control Tunnel (UDP port 55246)** - Tunnel used to configure the APs and control/manage the operations.  All traffic in this tunnel is encrypted by default
- **Data Tunnel (UDP port 5247)** - All traffic from wireles clients is sent through this tunnel to the WLC.  Does *not* go directly to the wired network
	- Traffic in this tunnel is not encrypted by default but you can configure it to be encrypted with DTLS (Datagram Transport Layer Security)

Lightweight Benefits
- Scalability
- Dynamic Channel Assignment
- Transmit Power Optimization
- Self-Healing Coverage
- Seamless Roaming
- Client Load Balancing
- Security/QoS Management

##### Lightweight AP Modes

**Local** - Default mode where the AP offers a BSS(s) for clients to associate with

**Flex Connect** - Allows the AP to locally switch traffic between the wired and wireless network if the tunnels to the WLC go down

**Sniffer** - AP does *not* offer a BSS for clients.  Captures 802.11 frames to send to a sniffer like wireshark

**Monitor** - AP does *not* offer a BSS.  Dedicated to receiving 802.11 frames to detect rogue devices

**Rogue Detectors** - AP does not use its radio.  Listens to **wired** traffic.  Receives a list of suspected rogue clients from WLC correlates ARP messages to info from WLC.

**SE-Connect (Spectrum Expert Connect)** - AP does not offer BSS.  Used for Spectrum Analysis

**Bridge/Mesh** - Can be bridge between sites over long distances.  Or a mesh between APs.

**Flex+Bridge** - FlexConnect + Bridge, locally forward traffic even if WLC is lost.  

##### Cloud Based AP

Between Autonomous and split MAC architectures

Cisco Meraki popular cloud based solution

Meraki Dashboard can be used to configure APs, monitor, reports

Traffic is *not* sent to the cloud, sent directly to wired network like when using autonomous APs.
	Only management traffic is sent to the Cloud

##### 4 WLC Deployment Models

1. Unified - Hardware Appliance in a central location in the network
	1. 6000 APs
2. Cloud Based - WLC is a VM running in a private cloud or data center.  Not a Meraki style
	1. 3000 APs
3. Embedded - WLC on a switch
	1. 2000 APs
4. Mobility Express - WLC on a AP
	1. 100 APs


