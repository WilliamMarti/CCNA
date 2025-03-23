
Transport Protocols

Provide transparent transport of data between hosts

Can provide (or not):
1. Reliable Data Transfer
2. Error Recovery
3. Data Sequencing
4. Flow Control

Layer 4  Addressing = **Port Numbers**
- ID the App Layer Protocol 
- Provide session multiplexing

## **TCP**

| Port Purpose              | Port Numbers |
| ------------------------- | ------------ |
| Well Known                | 0-1023       |
| Registered                | 1024-49151   |
| Ephemeral/Private/Dynamic | 49152-65535  |

TCP is connection oriented
Two Hosts communicate to establish a connection before data transfer

TCP provides a reliable communication
Destination host must acknowledge it received each TCP sequence
If a sequence isn't Acknowledged it is sent again

TCP provides sequencing
Sequence Numbers allow Destination host to put segments in the correct order even if they arrive out of order

TCP provides Flow Control
Destination Host can tell the source host to increase or decrease the rate that data is sent

Source Port: 16 bits
Destination Ports : 16 bits

TCP Forward Acknowledgment

![[TCP-Forward-ACK.PNG]]


TCP Retransmission
Source Host has a timeout waiting for a ACK

TCP Window Size
Allow more data to be sent before an ACK is required

**TCP Sliding Window** - Increases or decreases the rate at which at which the send traffic as needed
- When a packet is dropped it will be retransmitted
- When a drop occurs, sender will reduce the rate it sends traffic.
- Gradually increases rate again
## **UDP**

UDP is NOT connection oriented
Data is simply sent

UDP does NOT provide reliable communication
NO ACKs for data
Segments are sent "best effort"

UDP does NOT provide sequencing
UDP will not put out of order segments back in order

UDP does NOT provide Flow Control
No window size

TCP provides more features, but at the cost of **overhead**

For apps that require reliable communication (downloading a file), TCP is preferred

For real-time voice/video, UDP is preferred

**Common TCP Ports**

| TCP Service | Port Number | UDP Service  | Port Number | TCP&UDP Service | Port Number |
| ----------- | ----------- | ------------ | ----------- | --------------- | ----------- |
| FTP Data    | 20          | DHCP server  | 67          | DNS             | 53          |
| FTP Control | 21          | DHCP client  | 68          |                 |             |
| SSH         | 22          | TFTP         | 69          |                 |             |
| Telnet      | 23          | SNMP agent   | 161         |                 |             |
| SMTP        | 25          | SNMP manager | 162         |                 |             |
| HTTP        | 80          | Syslog       | 514         |                 |             |
| POP3        | 110         |              |             |                 |             |
| HTTPS       | 443         |              |             |                 |             |
|             |             |              |             |                 |             |








