Secure Shell

By default no password is needed to access a cisco IOS device via the console port

Can configure a password via the command line

```
! only a single console line, 1 user at a time
R1(config)# line console 0
R1(config)# password ccna
! require a user to enter the configured password
R1(config)# login
R1(config)# end
```

Can configure the console line to require users to log in using a username on the device

```
R1(config)# username ben secret ccna
R1(config)# line console 0
R1(config-line)# login local
```

login local > password

```
! 3 = minutes
! 30 = seconds
R1(config)# exec-timeout 3 30
```

Layer 2 switch can have a SVI to allow remote connections (telnet/ssh)

```
R1(config)# int vlan1
R1(config-if)# ip address 192.168.1.253 255.255.255.0
R1(config-if)# no shut
R1(config-if)# exit
R1(config)# ip default-gateway 192.168.1.254
```

##### Telnet

Teletype Network

Used to remotely access the CLI of a remote host

Developed in 1969

Replaced with SSH

Sends data in plaintext

TCP port 23

##### Telnet Config

```
R1(config)# enable secret
R1(config)# username ben secret ccna
R1(config)# access-list 1 permit host 192.168.2.1
! 16 available, 16 users, 0-15
R1(config)# line vty 0 15
R1(config)# login local
R1(config)# exec-timeout 5 0
R1(config)# transport input telnet
R1(config)# access-list 1 in
```


##### SSH

Secure Shell

Developed in 1995

Shell is a program that exposes an OS's services to a user with a CLI or GUI.  "Shell" being the outermost layer of the OS

SSHv2 came out in 2006, major revision.

If a device supports both v1 and v2, it runs "v1.99"

SSH provides data encryption and authentication

TCP 22

IOS SSH support = K9  image

```
R1# show ip ssh
```

MUST generate RSA keys

```
! FQDN used to name RSA keys
R1(config)# ip domain name ben.com
R1(config)# crypto key generate rsa <2048>
```

SSHv2 requires a length of at least 768 bit

##### Configure SSH

```
R1(config)# enable secret ccna
R1(config)# username ben secret ccna
R1(config)# access-list 1 permit host 192.168.2.1
! option, but recommended
R1(config)# ip ssh version 2
R1(config)# line vty 0 15
R1(config-line)# login local
R1(config-line)# exec-timeout 5 0
R1(config-line)# transport input ssh
R1(config-line)# access-class 1 in
```

```
! Cannot be default 'Router'
R1(config)# hostname TEST1
```


SSH Config Steps:
1. Configure Hostname
2. Configure DNS domain name
3. Generate RSA key pair
4. Enable password, username/password
5. SSHv2
6. VTY lines

Linux

```
# ssh ben@hostname
! or
# ssh -l ben hostname
```



