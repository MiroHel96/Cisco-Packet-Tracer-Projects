# Simple LAN with VLANs

In this packet tracer project I create a simple LAN with 2 different VLANs `IT` and `Marketing`. This execsise also includes basic L2 network security principles. 

## Network topology 

<img width="876" height="1114" alt="image" src="https://github.com/user-attachments/assets/785f7366-a993-4d3a-a4be-30414046ca37" />

## Basic Switch and Router configurations 

Configuring SW1_IT 

<img width="1396" height="1702" alt="image" src="https://github.com/user-attachments/assets/cdf09f8c-2737-485d-9d2f-058709c61ce1" />

I used the following commands to create basic configuration for both of the switches, SW2_Marketing has different host name but other settings are the same. I copied the configuration to SW2 and changed the hostname.

```
SW configuration

subnetmask 28 = 16 addresses = 14 hosts 255.255.255.240

hostname SW1_IT

enable secret letmein

Console Password
line console 0
password Linux
login
exit

VTY (telnet/SSH) Password
line vty 0 4
password windows
login
exit

MOTD-banner 
banner motd # Unauthorized access prohibited # 

Management-IP VLAN 99
interface vlan 99 
ip address 192.168.1.2 255.255.255.0
no shutdown 

Default gateway

ip default gateway 192.168.1.1 
```
## Implementing VLANs 



### Trunking ports for router on a stick method 


## Switch Security 

Basic L2 security principles are to shutdown all unused ports and move them to blackhole vlan, use port-security, disable trunking in all access ports and so on.
