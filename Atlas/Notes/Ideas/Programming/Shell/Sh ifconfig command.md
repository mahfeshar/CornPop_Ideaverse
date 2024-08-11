#note/develop🍃 
- **ifconfig** stands for "interface configuration."
- It is used to configure or view the configuration of a [[Network]] interface

>[!Note]
>The [[Sh ip command]] has replaced ifconfig on modern Linux systems

## Options

| Command | Output                                                                            |
| ------- | --------------------------------------------------------------------------------- |
| `-a`    | All network interfaces, even if they are down                                     |
| `-s`    | A short list in a format, identical to [[Sh netstat command#^0d9c81\|netstat -i]] |
| `-v`    | Verbose mode; Display additional information for certain error conditions         |

## Syntax
- Without arguments
```sh
ifconfig
```
displays information about all network interfaces currently in operation
#### Output
```plaintext
eth0      Link encap:Ethernet  HWaddr 09:00:12:90:e3:e5  
          inet addr:192.168.1.29 Bcast:192.168.1.255  Mask:255.255.255.0
          inet6 addr: fe80::a00:27ff:fe70:e3f5/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:54071 errors:1 dropped:0 overruns:0 frame:0
          TX packets:48515 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:22009423 (20.9 MiB)  TX bytes:25690847 (24.5 MiB)
          Interrupt:10 Base address:0xd020 
lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:16436  Metric:1
          RX packets:83 errors:0 dropped:0 overruns:0 frame:0
          TX packets:83 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:7766 (7.5 KiB)  TX bytes:7766 (7.5 KiB)
wlan0     Link encap:Ethernet  HWaddr 58:a2:c2:93:27:36  
          inet addr:192.168.1.64  Bcast:192.168.2.255  Mask:255.255.255.0
          inet6 addr: fe80::6aa3:c4ff:fe93:4746/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:436968 errors:0 dropped:0 overruns:0 frame:0
          TX packets:364103 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:115886055 (110.5 MiB)  TX bytes:83286188 (79.4 MiB)
```
Here, **eth0**, **lo** and **wlan0** are the names of the active network interfaces on the system.

- **eth0** is the first Ethernet interface. (Additional Ethernet interfaces would be named **eth1**, **eth2**, etc.) This type of interface is usually a [[MAC Address#NIC (Network Interface Card)|NIC]] connected to the network by a [[Network Components#Twisted pair cable|CAT 5]] cable.
- **lo** is the [[IP Address#Loopback address|loopback]] interface. This is a special network interface that the system uses to communicate with itself.
- **wlan0** is the name of the first [[Network Components#Transmission media|wireless]] interface on the system. Additional wireless interfaces would be named **wlan1**, **wlan2**, etc.
