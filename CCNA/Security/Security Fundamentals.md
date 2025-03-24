
CIA Triad
* **Confidentiality** - Only authorized users can access data
* **Integrity** - Data cannot be tampered with.  Correct and authentic
* **Availability** - Network systems should be operational and accessible to users

Attackers can threaten the Confidentiality, Integrity, and Availability of systems.  

**Vulnerability** - Potential weak that can compromise the CIA of a system.

**Exploit** - Something used to exploit the vulnerability

**Threat** - Potential of a vulnerability to be exploited 

**Mitigation Technique** - Something used to protect against threats

##### Common Attacks

DoS (Denial of Service) Attacks

Spoofing Attacks

Reflection / Amplification Attacks

Man-in-the-middle Attacks

Malware

Social Engineering Attacks

Password-Related Attacks


##### DoS

Threated Availability of a system

One common attack si the TCP SYN flood

DDoS  - Distributed Denial of Service
(botnet)

##### Spoofing Attacks

Uses a fake source address(IP or MAC)

Many attacks use this, not a single type of attack

Ex. DHCP Exhaustion
- Attacker uses spoofed MAC Addresses to flood DHCP Discover Messages
- Target server DHCP pool becomes full, resulting in a DoS to other devices

##### Reflection / Amplification Attack

Attackers sends traffic to a *reflector* and spoofs the source address of its packets using the targets IP Address

The reflector(DNS Server) sends the reply to the targets IP address

Amount of traffic can result in a DoS

Reflection attack becomes an amplification attack when the amount of traffic sent by attack is small but triggers a large amount of traffic to be sent from the reflector to the target

> Cloudflare DNS Attack


##### Man-in-the-Middle

Attackers places himself between the source and destinations to eavesdrop on communication, or to modify traffic before it reaches the destination.

Ex. ARP Spoofing aka ARP Poisoning 

Host sends ARP Request asking for MAC of another device

Target Send ARP reply

Attack waits and send another ARP reply after legit replies

If attacker ARP replies last it will overwrite the legit ARP entry

Compromises the Confidentiality and Integrity

##### Reconnaissance Attacks

Aren't attacks themselves, but need used to gather info about a target

Publically available info

nslookup / whois

##### Malware 

Malicious software refers to a variaty of harmful programs that can infect a computer

* **Viruses** - Infect other software.  Viruses spreads as the software is shared by users.  Typically they corrupt or modify files on the target computer
* **Worms** - Standalone malware and able to spread on their own.  Spread of worms can congest the network but the payload of a worm can cause additional harm to the target devices
* **Trojan Horse** - Harmful software disguised as legit software spread throughout users interaction such as opening email attachments or downloading a file from the Internet

##### Social Engineering

Attach most vulnerable part of any system, **people**

**Phishing** - Emails from a "legit" website.  Contain links to a fraudulent website. 

**Spear Phishing** - Targeted form of phishing.  Aimed at a certain employee of a company

**Whaling** - Targeted a high profile person

**Vishing** - Voice Phishing.  Phishing done over the phone

**Smishing** - (SMS Phishing) Phising over text messages

**Watering Hole** - Compromise site the victim frequently visits.  If a malicious link is placed on a website the target trusts, they might not hesitate to click it.

**Tailgating** - Entering a restricted, secured area by simply walking in behind an authorized person as they enter

##### Personal Related Attacks

Most systems use a username/password combination to authenticate users

Username is easy to guess, strength and secrecy of the password is relied on to provide necessary security.  

Attacker can learn a users password via multiple methods
1. Guessing
2. Dictionary Attack
	1. Common words/passwords
3. Brute Force
	1. Program tries every password

Strong Passwords contain
- At least 8 characters
- Uppercase and Lowercase letters
- mix of letters and number
- one or more special characters
- changed regularly

##### Multi-Factor Authentication 

More than a username+password

- Something you KNOW
	- username/password
- Something you HAVE
	- Notification on a phone/Badge
- Something you ARE

##### Digital Certificate 

Prove Identity of holder

Used for websites to verify that the website is legitimate

Prove Identity by sending a CSR(Certificate Signing Request)to a CA (Certificate Authority), which will generate and sign the certificate

##### AAA

Authentication / Authorization / Accounting

Authentication - Process of verifying a users identity

Authorization - Process of granting the user the appropriate access and permissions

Accounting - Process of recording a users activities on a system

Use AAA server to provide AAA services

Ex. ISE - Cisco Identity Services Engine

Use the following 2 Protocols

1. RADIUS - Open Standards
	1. UDP ports 1812 nad 1813
2. TACACS - Cisco Proprietary
	1. TCP port 49


##### Security Program Elements

**User Awareness** - Program designed to make employee aware of potential threats and risks
	Ex. Phising emails

**User Training** - More formal than user awareness

**Physical Access Control** - Protect equipment and data by only allowing authorized users to protect areas such as network closets or data center floors




