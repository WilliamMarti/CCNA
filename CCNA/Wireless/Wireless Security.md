 ##### Integrity

Ensure a message is *not* modified in transit

A MIC (Message Integrity Check) is added to help protect their integrity

Process:
1. Sender calculate a MIC for the message and attaches it to the message
2. Sender encrypts the message and MIC and sends the frame
3. The receipt decrypts the message
4. The receipt independently calculate a MIC for the message (using the same protocol or the sender)
5. If the two MICs are the same the recipient assumes the message wasn't tampered with

##### Authentication Methods
1. Open Authentication
2. WEP (Wired Equivalent Privacy)
3. EAP (Extensible Authentication Protocol)
4. LEAP (Lightweight EAP)
5. EAP-Fast (EAP Flexible Authentication via Secure Tunneling)
6. PEAP (Protected EAP)
7. EAP-TLS (EAP Transport Layer Security)

Original 802.11 standard included 2 options for Auth

##### Open Authentication

- All accepted
- Not secure
- After client is authed and associated with AP it is possible to require the user to authenticate via other methods before access to the network is granted (Starbucks Wifi)

##### WEP (Wired Equivalent Privacy)

- Provides both auth and encryptions 
- Used RC4 algorithm
- "Shared-Key" protocols.  Sender and receiver are required to have the same key
- Keys can be 40 bits or 104 bits in length
- Above keys are combined with a 24-bit "IV" (Initialization Vector) to bring the total length to 64 bits or 128 bits
- NOT secure, can be easily cracked
- Process
	- AP sends "challenge phrase"
	- Client encrypts challenge phrase using WEP key and sends it back
	- AP compares clients encrypted challenge phrase with APs encrypted challenge phrase.  

##### EAP (Extensible Authentication Protocol)

- Auth Framework
- Defines a standard set of functions that are used by the various EAP Method
	- LEAP/EAP-FAST/PEAP/EAP-TLS
- Integrated with 802.1x, provider port based access control

##### 802.1x

Used to limit network access for clients connected to a LAN or WLAN unit they authenticate

- **Supplicant**  - Device that wants to connect to the network
- **Authenticator** - Device that provides access to the network (Access Point/WLC/Switch)
- **Authentication Server(AS)** - The device that receives credentials and permits/denies access

##### LEAP (Lightweight EAP)

- Developed by Cisco
- Client must provide username and password
- Mutual Authentication is provided by both the client and server send a challenge phrase to each other
- Dynamic WEP keys are used, meaning they are changed frequently
- Like WEP, LEAP is considered vulnerable and should not be used.

##### EAP-Fast

EAP Flexible Authentication via Server Tunnel

Developed by Cisco

3x Phases:
1. A PAC (Protected Access Credential) is generated and passed from the server to client
2. A secure TLS tunnel is established between the client and authentication server
3. Inside the service (encrypted) TLS tunnel, the client and server communicate further to authenticate/authorize the client

##### PEAP (Protected EAP)

- Like EAP-Fast, PEAP involves establishing a secure TLS tunnel between the client and server
- Instead of PAC, the server has a digital certificate
- Certificate is used to establish a TLS tunnel
- Because the server only provides a certificate for authentication, the client must still be authed within the secure tunnel, for example using MS-CHAP (Microsoft Challenge-Handshake Protocol)

##### EAP-TLS (EAP-Transport Layer Security)

- Where PEAP only required the AS to have a cert, EAP-TLS requires a certificate on the AS and on every single client
- Considered the most secure, more difficult because every client needs a certificate.
- Because client and server authenticate each other with digital certs, these is no need to auth the client within the TLS tunnel
- TLS tunnel is still used to exchange encryption key info

##### Encryption and Integrity Methods

- TKIP (Temporal Key Integrity Protocol)
- CCMP (Counter / CBC-MAC Protocol)
- GCMP (Galois / Counter Mode Protocol)

##### TKIP

- Temp solution to fix vulnerabilities with WEP
- Security Features
	- Uses MIC
	- Key mixing algorithm to create unique WEP key for every frame
	- Initialization Vector is double in length from 24 bits to 48 bits, making brute-force attacks much more difficult
	- MIC includes the sender MAC address to identify the frames sender
	- Timestamp is added to prevent replay attack
	- TKIP sequence number is used to keep track of frames sent from each source MAC address to prevent replay attacks.
- Used in WPA 1

##### CCMP (Counter / CBC-MAC Protocol)

- Developed after TKIP and is more secure
- Used in WPA2
- Must be supported by devices hardware
- Old hardware built only for WEP/TKIP can't CCMP
- CCMP consists of 2x algorithms
	- AES (Advanced Encryption Standard) counter mode for encryption
	- CBC-MAC (Cipher Block Chaining Message Authentication Code) is used as a MIC to ensure integrity

##### GCMP (Galois / Counter Mode Protocol)

- More secure than CCMP
- Its increased efficiency allows higher data throughput than CCMP
- It is used in WPA3
- 2 x Algorithms
	- AES (Advanced Encryption Standard) counter mode for encryption
	- GMAC (Galois Message Authentication Code) used as a MIC for integrity


##### Wi-Fi Protected Access

Wi-Fi Alliance developed 3x WPA certification for wireless devices
- WPA
- WPA2
- WPA3
Devices must be tested in labs to be certified

All of the above support 2 authentication methods

1. Personal Mode - A pre-shared key (PSK) is used for authentication
	1. PSK isn't sent over the air.  4-way handshake is used for auth and the PSKs used to generate encryption keys
	2. Enterprise Mode - 802.1x is used with an Authentication Server (RADIUS).  No specific EAP method is specified so all are support (PEAP, EAP-TLS)


##### WPA

Certification was developed after WEP was proven to be vulnerable.  Includes:
- TKIP for encryption/MIOS
- 802.1x authentication.  Enterprise or Personal

##### WPA2

- Released in 2004
- CCMP provides encryption/MIC
- 802.1x authentication.  Enterprise or Personal

##### WPA3

- Release in 2018
- GCMP for encryption/MIC
- 802.1x authentication.  Enterprise or Persona;
- Additional security features
	- PMF(Protected Management Frames) protecting 802.11 management frame from eavesdropping/forging
	- SAE (Simultaneous Authentication of Equals) protects the four-way handshake when using personal mode authentication.
	- Forward Secrecy prevents data from being decrypted after its been transmitted

DHCP Option 43 can be used to tell APs the IP address of their WLC

WLC **port** are the physical ports that cables connect to

WLC Interfaces are  the logical interfaces within the WLC(SVI on a switch)

**Service Port**  - Dedicated management port.  Used for out-of-band management.  Most connect to switch access port, only supports one vlan.  Used to connect while WLC is booting/system recovery

**Distribution Port** - Standard network port to connect to the "distribution network".  Usually a trunk.  Can be a LAG

**Console** - Standard RJ45 or USB Console port

**Redundancy Port** - Used or USB console port

##### WLC Interfaces

**Management** - Management traffic such as telnet/SSH/HTTPS/RADIUS/CAPWAP tunnel are also formed to/from the management interface. 

**Redundancy Management** - Where 2 WLCs are connected by RP ports one is "active" and the other is "standby".  These interfaces can be used to manage the "standby" WLC

**Virtual Interfaces** - Used when communicating with wireless clients to relay DHCP requests, perform client web authentication

**Service Port Interfaces** - If service port is used.  This interface is bound to it and used for out-of-band management

**Dynamic Interface**  - Interfaces used to map a WLAN to a VLAN.  For example traffic from the internal WLAN will be sent to the wired network from the WLCs "Internal" dynamic Interface

**Web Authentication** - After client gets an IP and tries to access a web page, they will have to enter a username/password

**Web Passthrough** - Similar to above, but no username/password are required.  Warning of statement is displayed and the client has to agree to gain access to the Internet

**Conditional** and **Splash Page**  - web redirect options are similar but additional require 802.1x L2 auth

**CPU ACLS** - Are used to limit traffic to the CPU of the WLC, such as telnet/SSH/HTTPS traffic to management NETO data plane traffic

WLC QOS:
- Platinum (Voice)
- Gold (Gold)
- Silver (Silver)
- Bronze (Bronze)

WLC *passwords* can be in ASCII or HEX

ASCII must be at least 8 characters long