**FTP** - File Transfer Protocol
**TFT** - Trivial File Transfer Protocol

Industry Standard protocols for transferring files over a network.

client-server model
	to/from server

##### **TFTP** 

Standardized in 1981

Only allows a copy to or from a server

Released *after* FTP, more lightweight

No authentication

No encryption

UDP port 69
UDP connectionless, no reliability

TFTP has built in feature within the protocol itself

Every TFTP data message is acknowledged
If client is transferring to server, server acks
If server sending to client, client acks

Timers are used if an expected message isn't received in time.

TFTP 
- Client sends read request
- Server sends data
- Client sends ACK

Local Step communication - Client and server send a message and wait for a reply

3x Phases
- **Connection** - TFTP Client sends a request to the server.  Server responds back, initializing the connection.
- **Data Transfer** - Client and server exchange TFTP messages.  One sends data and the other acks
- **Connection Termination** - After last data message a final ACK is sent to terminate the connection.


##### FTP

Standardized 1971

TCP port 20 and 21

Has authentication, but plain text

For greater security FTPS(FTP over SSL/TLS).  Upgrade to FTP.

SSH File Transfer Protcol (SFTP) for greater security

FTP is more complex than TFTP.  Can navigate directories, add/remove directories, list files, etc

Client sends FTP command to the server to perform function

FTP uses 2x Connections:
1. **FTP Control** (21) - Used to send FTP commands and replies
2. **FTP Data(20)** - Used to send the actual data

2x Modes of Data Connection
- **Active** - Server initiates the TCP connection for Data
- **Passive** - Client activates the TCP connection for data.  Required if there is a Firewall that would block data from the server

FTP
- TCP Ports 20/21
- Use commands for various actions
- Username/pw auth

TFTP
- UDP 69
- Client can copy files to/from a server
- No auth

 









