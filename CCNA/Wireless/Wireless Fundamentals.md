
Standards for wi-fi is 802.11 IEEE

All devices within range receive all frames like a Hub

- Privacy within the LAN is a greater concern
- CSMA/CA (Carrier Sense Multiple Access with Collision Avoidance) is used to facilitate half-duplex communications.  

**CSMA/CD** - Wired networks detect and recover from collisions
**CSMA/CA** - Wireless networks to avoid collisions

Using CSMA/CA a device will wait for other devices to stop transmitting before it transmits itself

Wireless Communication are governed by various international bodies

Wireless Signal Coverage must be considered
- Signal Range
- Signal:
	- Absorption
		- Wireless Signal passes through a material and is converted into heat, weakening the original signal.  
	- Reflection
		- When a signal bounces off a material.  Ex Metal
	- Refraction
		- When a wave is bent when entering a medium where signal travels at a different speed
	- Diffraction
		- When a wave encounters an obstacle and travels around it
	- Scattering
		- When a material causes a signal to scatter in all directions
			- dust/smog/uneven surfaces

Other devices using the same channels can cause *interference*

##### Radio Frequency

To send wireless signal, sender applies an alternating current to an antenna
	This creates electro magnetic fields which propagates out as waves

EM waves can be measured in multiple was, **Amplitude** and **Frequency**

**Amplitude** - is the maximum strength of the electric and magnetic fields

**Frequency** - Number of up/down cycles per a given unit of time

Most common measurement of frequency is hertz(Hz) = cycles per seconds

**Period** - Amount of time per cycles

Visible Frequency range is about 400THz to 780Thz

##### Wifi Bands

2x Wifi bands:
- 2.4Ghz
	- 2.400Ghz to 2.4835Ghz
- 5Ghz
	- 5.150Ghz to 5.825Ghz

2.4 provides further reach in open space and better penetration of obstacles such as walls. 
- However, more devices tend to use the 2.4Ghz band so interference can be a bigger problem compared to the 5Ghz band.

Wifi 6(802.11ax) expanded the spectrum range to include a band in the 6Ghz range

Each "band" is divided into multiple "channels"
- Devices are configured to transmit and receive traffic on one (or more) of these channels

2.4 is divided into several channels, each with a 22Mhz range

In small wireless LANs with only a single AP, you can use any channel.

In Large WANs with multiple APs its important that adjacent APs, don't use overlapping channels to avoid interference

In 2.4Ghz it is recommended to use channels 1, 6, 11

| Standard | Frequency | Max Data Rate | Alt Name |
| -------- | --------- | ------------- | -------- |
| 802.11   | 2.4       | 2M            |          |
| 802.11b  | 2.4       | 11M           |          |
| 802.11a  | 5         | 54M           |          |
| 802.11g  | 2.4       | 54M           |          |
| 802.11n  | 2.4/5     | 600M          | Wifi 4   |
| 802.11ac | 5         | 6.93G         | Wifi 5   |
| 802.11ax | 2.4/5/6   | 4*802.11ac    | Wifi 6   |
802.11 defines different kinds of service **sets** which are groups of wireless network devices.

3x Main Types:
1. Independent
2. Infrastructure
3. Mesh

All Devices in a service set share the same SSID(Service Set Identifier) 

SSID is a human readable name which identifies the service set

SSID does not have to be unique

**IBSS** - Independent Basic Service Set.  Wireless network in which two or more wireless devices connect directly without using an AP(Access Point)
- ad hoc (air drop)

**BSS** - Basic Service Set - Kind of Infrastructure Service Set in which clients connect to each other via an AP, but not directly to each other

**BSSID** (Basic Service Set ID) - is used to uniquely identify the AP
- Other APs can use the same SSID but not the same BSSID
- BSSID is the MAC address of the APs radio

Wireless devices associate with the BSS

Wireless devices that have associated with the BSS are called 'clients' or 'stations'

**BSA** - Basic Service Area - Area around the AP

BSS = Group of devices
BSA = Physical Area

**ESS** - Extended Service Set - APs with their own BSSs are connected by a wired network.  
- Each BSS uses same SSID

**Roaming** - Clients can pass between APs, without having to reconnect, providing a seamless Wifi experience when moving between APs.  

BSAs should overlap 10-15%

**MBSS** - Mesh Basic Service Set - Mesh APs use 2 radios: 
- One to provide a BSS to wireless clients
- One to form a "backhaul network" which is used to bridge traffic from AP to AP

At least one AP is connected to  the wired network and it is called the RAP (Root Access Point)

In 802.11 the upstream wired network is called the   DS(Distributed System)

Each BSS or ESS is mapped to a VLAN

It is possible for an AP to provide multiple wireless LANs, each with a unique SSID

##### AP Operation Modes

**Repeater Mode** - Extend the range of a BSS

Repeater will retransmit and signal it receives from the AP 

A repeater with a single radio must operate on the same channel or the AP, butr this can drastically reduce the overall throughput on the channel

**Workgroup Bridge(WGB)** - Operates as a wireless client of another AP and can be used to connect wired devices to the wireless network.  

![[WGB.PNG]]

**Outdoor Bridge** - used to connect networks over long distances without physical cable connecting them

APs used specialized antennas that focus most signal power in one direction, which allows the wireless connection to be made over long distances.  

Connection can be point-to-point or point-to-multipoint

##### Wireless Frame

![[80211-frame.PNG]]