D-> O -> R -> A

**Discover** 
src: UDP 68 Client Broadcast
dst: UDP 67 Server

**Offer**
src: UDP 67 Server Broadcast/Unicast
dst: UDP 68 Client

**Request**
src: UDP 68 Client Broadcast
dst: UDP 67 Server

**Ack**
src: UDP 67 Server Broadcast/Unicast
dst: UDP 68 Client

**DHCP Relay Agent** - Router will forward client's broadcast messages to a remote DHCP server as a unicast message

```
! excluded range
R1(config)# ip dhcp excluded-address 192.168.1.1 192.168.1.10 
! create dhcp pool
R1(config)# ip dhcp pool LAB_POOL
R1(dhcp-config)# network 192.168.1.0/25
R1(dhcp-config)# dns-server 8.8.8.8
R1(dhcp-config)# domain-name test.com
R1(dhcp-config)# default-router 192.168.1.1
! {days} {hours} {minutes}
R1(dhcp-config)# lease 0 5 30
```

```
R1# show dhcp bindings
```

```
! DHCP Relay
R1(config)# int g0/1
R1(config-if)# ip helper-address 192.168.10.10
```

```
! DHCP Client
R1(config)# int g0/1
R1(config)# ip address dhcp
```

```
! Windows 
# ipconfig /release
# ipconfig /renew
```

