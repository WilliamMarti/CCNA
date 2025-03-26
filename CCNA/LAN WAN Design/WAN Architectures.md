
**WAN** - Wide Area Network

WAN is a network that extends over a large geographic area

WANs are used to connect geographically separate LANs

Although the Internet can be considered a WAN, the term WAN is usually used to refer to a Enterprise's private connection that connect their offices, data center, and other sites together

Over Public/Shared networks, VPNs, can be used to create private WAN connections

##### Leased Line

Dedicated physical link, typically connectivity 2 sites

Use serial connections (PPP or HDLC encapsulation)

Various standards that provide different speeds and different standards are available in different countries

| US  | EU  | Speed       |
| --- | --- | ----------- |
| T1  | E1  | 1.544 Mbps  |
| T2  | E2  | 6.312 Mbps  |
| T3  | E3  | 44.736 Mbps |
Leased Lines have a higher cost, install time, and slower speeds vs Ethernet

**MPLS** - Multi-Protocol Label Switching

Similar to Internet, service provider MPLS networks are sshared infrastructure because many customer Enterprises connect and share the same infrastructure

Label Switch in the name of MPLS allows VPNs to be created over the MPLS infrastructure through the use of labels

Label separate the traffic of customers

CE Router = Customer Edge
PE Router = Provider Edge
P Router = Provider Core

![[MPLS.PNG]]

When the PE ROuter receives frames from CE routers they add a label to the frame.

The **labels** are used to make forwarding decisions with the service provider network.  *not the destination IP*

CE Routers do not use MPLS, only the PE/P routers

When using a Layer 3 MPLS VPN, the CE and PE routers peer using OSPF(or BGP), for example, to share routing information

Layer 2 MPLS VPN, CE and PE routers do not form peerings

Service providers network in entirely transparent to the CE routers

In effect 2 CE routers are directly connected WAN interfaces in same subnet

In routing protocol is used, the two CE routers all peer directly with each other

Many different technologies can be used to connect to a MPLS network
- Ethernet(Fiber)
- 4G/5G
- CATV(Cable TV)
- Serial

##### Internet Connections

Many ways to connect to Internet

Private WAN and Leased Lines can be used to connect to service provider Internet Infrastructure

CATV or DSL usually used by consumers can also be used by Enterprises

Fiber Optic Ethernet is growing in popularity

##### DSL

Digital Subscriber Line

Provide Internet connectivity to customers over phone lines and can share the same phone line that is already install at most homes


![[DSL.PNG]]

A DSL modem (modulator-demodulator) is required to convert data into a format suitable to be sent over the phone lines
	Modem might be a separate device, or it might be incorporate in to the "home router"

##### Cable Internet

Provider Internet Access via the same CATV lines used for TV Service

##### Redundant Internet Connections

- 1 Connection to 1 ISP = Single Homed
- 2 Connections to 1 ISP = Dual Homed
- 1 Connection to each of 2 ISP = Multi-Homed
- 2 Connections to each of 2 ISP = Dual Multi-Homed

##### Internet VPNs

Private WAN services such as leased lines or MPLS provide security via MPLS tags or separate physical connections

No built in security with Internet

VPNs are used to provide security

##### Site-to-Site VPN

VPN between two devices to connect 2 sites together

VPN tunnel is created between two devices encapsulating the original IP packet with a VPN header and a new IP header

When using IPSEC, original packet is encrypted before encapsulated with the new header

| encrypted data | VPN Header | IP Header |

Process
1. Sending Device combining original packet and session key (encryption key) and runs them through encrypt formula
2. Sending device encaps the encrypted packet with a VPN header and new IP
3. Sending devices sends the new packet to the device on the other side of the tunnel
4. Receiving device decrypted the data to get the original packet and then forwards the original packet to its destination

In a site-to-site VPN a tunnel is formed only between two tunnel endpoints (for example, the two routers connected to the Internet)

Other devices don't create tunnels, send unencrypted data to their sites router, which will encrypt and forward it in a the tunnel as described above.  

##### IPSEC Limitations

1. No broadcast or multicast traffic, only unicast means routing protocols such as OSPF cannot be used
	1. Can be solved with GRE over IPSEC
2. Full Mesh of tunnel between many sites is a labor-intensive task
	1. Can be solved with DMVPN

##### GRE over IPSEC-Generic Routing Encapsulation

Creates tunnels like IPSEC.  Does not encrypt original packet, so not secure

Has advantage of being able to encapsulate a wide variety of L3 protocol, as well as broadcast and multicast messages

Original packet will be encapsulated by a GRE header and a new IP header, and then the GRE packet will be encrypted and encapsulated within an IPSEC VPN header and a new IP header

##### DMVPN

Dynamic Multipoint VPN

Allows Routers to dynamically create a full mesh of IPSEC tunnels without having to manually config every single tunnel

![[DMVPN.PNG]]

Provide config simplicity of Hub  and Spoke and the efficiency of direct spoke-to-spoke communication.

##### Remote-Access VPNs

Used for end devices (PC, Phones) to access the company's internal resources securely over the Internet

Remote-Access VPNs typically use TLS (Transport Layer Security)

VPN client software (for example Cisco AnyConnect) is installed on end devices


| Site-to-Site                    | Remote Access |
| ------------------------------- | ------------- |
| IPsec                           | TLS           |
| Provide service to many devices | End Devices   |
| Permanent connect two devices   | On-Demand     |


