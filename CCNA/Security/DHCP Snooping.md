Security feature of switches that is used to filter DHCP messages received by untrusted ports

Only filters DHCP messages

All ports are *untrusted* by default 

- **Uplink** are configured as trusted
- **Downlink** remain as untrusted

CHADDR - Client Hardware Address

When filters messages, it differentiates between DHCP server and DHCP client messages

| Server | Client                      |
| ------ | --------------------------- |
| OFFER  | DISCOVER                    |
| ACK    | REQUEST                     |
| NAK    | RELEASE (no longer need IP) |
|        | DECLINE(refuse IP offered)  |
##### DHCP Snooping Operations

If a DHCP message is received on a *trusted* port, forward as normal

If a DHCP message is received on a *untrusted* port, inspect as follows:
* If its a DHCP server(OFFER,ACK, or NAK) message, **Discard** it.
* IF message is a **Client**, perform the following checks
	* DISCOVER/REQUEST: Check if frame source/MAC and DHCP message CHADDR fields match
		* match = forward, mismatch = disccard
	* RELEASE/DECLINE: Check if the packets source IP address and the receiving interface match the entry in the DHCP Snooping Binding Table.
		* match = forward, mismatch = discard

When a client successfully lease an IP Address from a server, create a new entry in the DHCP Snooping Binding Table

```
S1(config)# ip dhcp snooping
S1(config)# ip dhcp snooping vlan 1
! remove Opt 82 info
S1(config)# no ip dhcp snooping information option
! uplink to router
S1(config)# int g0/0
S1(config-if)# ip dhcp snopping trust 
```

##### DHCP Snooping Rate-Limiting

DHCP Snooping can limit the rate at which DHCP messages care allowed to enter an interface

If the rate of DHCP message crosses to configured limit the interface is err-disabled

Similar to port-security, the interface can be manually re-enabled or automatically re-enabled with the errdisable recovery

```
S1(config)# int g0/0
S1(config-if)# ip dhcp snooping limit rate 1
S1(config)# errdisable recovery cause dhcp-rate-limit
```

Rate limiting can be useful to protect against DHCP exhaustion attacks

##### DHCP Option 82

AKA DHCP relay against information option

Provide additional info about which DHCP relay agent received the clients message, on which interface, in which vlan.

DHCP relay agents can add Option 82 to messages they forward to the remote DHCP server

With DHCP snooping enabled, by default Cisco Switches will add Option 82 to DHCP messages they receive from clinets
	Even if the switch isnt acting as a DHCP relay agent

By Default Cisco switch will drop DHCP message with Option 82 that are received on an untrusted port.



