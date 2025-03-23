
```
R1# show file systems
```

**Disk** - Storage such a flash memory

**opaqu** - Internal functions

**nvram** - Internal NVRAM.  Used for startup config

**network** - External file systems.  FTP/TFTP

```
R1# show version
R1# show flash
```

```
! tftp: = source
! flash: = destination
R1# copy tftp: flash:
```

 ```
 ! without this routers will use the first IOS file it finds in flash
 R1(config)# boot system flash:xyz.bin
```

##### FTP Config

```
R1(config)# ip ftp username cisco
R1(config)# ip ftp password ccna
R1(config)# ip ftp source Lo0
```

