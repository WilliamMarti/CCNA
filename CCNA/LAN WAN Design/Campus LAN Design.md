
2-Tier LAN Design

- Access Layer 
- Distribution Layer

Also called a "Collapsed Core", omits the "Core Layer"

**Access Layer** - Layer that end hosts connect to (PCs, Printers, Cameras)

- Access Layer Switches have lots of ports for end hosts
- QoS marking is done here
- Security services like port-security, DAI, are done here
- Switchports might be PoE-enabled for wireless APs, IP Phones, etc

**Distribution Layer**

- Aggregator connections from the Access Layer Switches
- Typically border between Layer 2 and Layer 3
- Connects to service such as Internet, WAN, etc

![[Campus LAN.PNG]]

Collapsed core design the Distribution Layer is sometimes called the Core-Distribution Layer

Cisco recommends adding a Core Layer if there are more than 3 Distribution Layers in a single location

Sometimes called Aggregation Layer

##### 3-Tier Campus LAN Design

- Access Layer
- Distribution Layer
- Core Layer

**Core Layer**

- Connects Distribution Layer together in Large LAN Networks
- Focus is speed ("Fast Transport")
- CPU intensive operations such as Security, QoS Markings should be avoided at this layer
- Connects all Layer 3, no spanning tree!
- Should maintain connectivity throughout the LAN even if devices fail


![[3 tier.PNG]]

##### Spine-Leaf Architecture

aka **Clos** -> Charles Clos Formalized

Data Centers are dedicated spaces/building used to store computer system such as servers and network devices

Traditional DC designs used 3-Tier architecture.  Access-Distribution-Core like we covered

Worked well when most traffic was North-South

With the precedence of virtual server, applications are often deployed in a distributed manner (across multiple physical servers), which increases the amount of East-West traffic in the Data Center

Traditional 3-Tier architectures led to bottle necks in bandwidth as well as variability in the server-to-server latency depending on the path the traffic flows

To solve this, **Spine-Leaf** architecture (Also called Clos architecture) has become prominent in Data Centers.

![[Spine-Leaf.PNG]]

##### Spine-Leaf Architecture Rules

- Every Leaf is connected to every Spine
- Every Spine is connected to every Leaf
- Leaf switches do NOT connect to other Leaf Switches
- Spines don't connect to other Spines
- End hosts (Servers) only connect to Leafs

Path taken by traffic is randomly chosen to balance the traffic load among the Spine Switches

##### SOHO Networks

Small Office / Home Office

Don't have complex needs, so all networking functions are typically provided by a single device,  often called a "home router" or "wireless router"

This one deivce can serve as a:
- Router
- Switch
- Firewall
- Wireless Access Point
- Modem


