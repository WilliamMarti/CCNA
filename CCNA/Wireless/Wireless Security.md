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
