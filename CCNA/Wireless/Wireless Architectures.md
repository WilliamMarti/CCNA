
802.11 Frame Format

**Frame Control** - Provides information such as the message type and subtype

**Duration/ID** - Depending on the message type, this field can indicate
- The time in microseconds the channel will be dedicated for transmission of the frame
- and identifier for the association(connection)

**Addresses** - Up to 4 addresses can be present on a 802.11 frame which are present depends onthe message type
- Destination Address (DA) Final recipient of the frame
- Source Address (SA) Original sender of the frame
- Receiver Address (RA) Immediate recipient of the frame
- Transmitter Address (TA) Immediate sender of the frame

**Sequence Control** - Used to reassemble fragment and eliminate duplicate frames. 

**QoS Control** - Used in QoS to prioritize certain traffic.

**HT(High Throughput) Control** - Added in 802.11n to enable High Throughput operations
- 802.11n is also known a "HT" wifi
- 802.11ac is also known as "Very HI" Wifi

**FCS (Frame Check Sequence)** - Same as iin an Ethernet frame used to check for errors

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

