
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


 
