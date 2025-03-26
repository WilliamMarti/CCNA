
Virtual Routing and Forwarding

VRF divides a single router into multiple virtual routers.
	Similar to how VLANs are used to divide a single switch (LAN) into multiple switches (VLANs)

Separate routing tables
- Interfaces and Routes are configured to be in a specific VRF
- Router Interfaces, SVI, and routed ports on multilayer switch can be configured in a VRF
- Traffic in one VRF cannot be forwarded out of an interface in another VRF
- VRF is commonly used to facilitate MPLS
	- Kind we are talking about here is VRF-LIte (VRF without MPLS)

VRF commonly used by service providers to allow one device to carry traffic from multiple customers
- Each customers traffic is isolated from the others
- Customer IP addresses can overlap without issues

##### Config

```
! Create VRF
R1(config)# ip vrf CUSTOMER1
R1(config-vrf)# ip vrf CUSTOMER2
```

```
! Create VRF
R1(config)# int g0/0
R1(config-if)# ip vrf forwarding CUSTOMER1
! removes IP address from int, need to reapply
R1(config-if)# ip address 192.168.1.1 255.255.255.0
```

```
R1# show ip route vrf CUSTOMER1
```

```
R1# ping vrf CUSTOMER1 1.1.1.1
```

