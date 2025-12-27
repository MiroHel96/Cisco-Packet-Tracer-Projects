# Simple LAN with VLANs

In this packet tracer project I create a simple LAN with 2 different VLANs `IT` and `Marketing`. This execsise also includes basic L2 network security principles. 

## Network topology 

<img width="810" height="1014" alt="image" src="https://github.com/user-attachments/assets/d5103b97-58ad-4242-9727-86404fd59112" />


## Addresses

I use /28 mask which means I have 16 addresses and 14 IPs for hosts:
- `192.168.1.1` default gateway
- `192.168.1.16` broadcast address
- `192.168.1.2` SW1 management address
- `192.168.1.3` SW2 management address
- `192.168.1.4` SW3 management address

Hosts:
- `192.168.1.5 - 192.168.1.13`

IT
- PC1 192.168.1.5 
- PC2 192.168.1.6
- PC3 192.168.1.7

Marketing
- PC1 192.168.1.8
- PC2 192.168.1.9
- PC3 192.168.1.10
  



## Basic Switch and Router configurations 

Configuring SW1_IT 

<img width="1396" height="1702" alt="image" src="https://github.com/user-attachments/assets/cdf09f8c-2737-485d-9d2f-058709c61ce1" />

I used the following commands to create basic configuration for both of the switches, SW2_Marketing has different host name but other settings are the same. I copied the configuration to SW2 and changed hostname and VLAN 99 management IP address to `192.168.1.2`. Now I have configured both switches with basic configurations.

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
## SW3 

Next I configured SW3 between SW1 and SW2 and connected router to it. I copied SW1 configuration and changed hostname and management IP address for it. 

<img width="1272" height="212" alt="image" src="https://github.com/user-attachments/assets/7d6c8c8c-6211-43cd-ae1f-26a54431e87f" />

I also configured trunk ports for interfaces FastEthernet 0/23 - 24. 

<img width="1266" height="440" alt="image" src="https://github.com/user-attachments/assets/df739288-832b-49f2-9d7d-5e72bba416b9" />


## Router basic configuration 

Next I configured Router1 basic configuration. 

```
Router configuration 

configure terminal
hostname R1

enable secret superSecret

line console 0
password ubuntu
login
exit

line vty 0 4
password ubuntu
login
exit

interface gigabitEthernet 0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit


ip route 0.0.0.0 0.0.0.0 192.168.1.254


ip dhcp pool LAN
network 192.168.1.0 255.255.255.0
default-router 192.168.1.1
dns-server 8.8.8.8
exit

```



<img width="1268" height="268" alt="image" src="https://github.com/user-attachments/assets/d2036b5c-5cd8-4627-893a-82526347a07a" />


## VLANS 

In this part I create two VLANs for SW1 and SW2. The VLANs will be 10 `IT` and 20 `Marketing`. 

<img width="1280" height="240" alt="image" src="https://github.com/user-attachments/assets/9438c9b5-2790-48f9-9515-cea014de8a93" />

I configured SW1 FastEthernet 0/1 - 3 ports with the following commands: 
- `switchport mode access`
- `switchport access vlan 10`

<img width="1266" height="864" alt="image" src="https://github.com/user-attachments/assets/a527868e-7774-4fee-8f49-f9ac7dbec684" />

Next I configured Marketing VLAN for SW2:
- `switchport mode access`
- `switchport access vlan 20`

<img width="1276" height="372" alt="image" src="https://github.com/user-attachments/assets/71341978-5103-483e-b055-76234ab1a356" />


### Trunking ports for router on a stick method 

Creating a router on a stick method is the best model for this network. It uses single link with trunking ports to deliver untagged traffic betwreen R1 and SW3. I configured both SW1 and SW2 interfaces with the following commands in both ends of the links connecting to SW3:
-`switchport mode trunking`
-`switchport nonegotiate`

Same principles were done for R1 and SW3 Links connecting to eachother. 


<img width="1264" height="262" alt="image" src="https://github.com/user-attachments/assets/954cb8bc-fd92-4e6e-8362-f9856c4e3b5e" />

<img width="1274" height="288" alt="image" src="https://github.com/user-attachments/assets/840a190d-2195-44c7-901e-2e4b57362c67" />


## Router sub-interfaces 

Next I configured router sub-intercaes without these the router does not know where to route packets from different VLANs.

```

interface gigabitEthernet0/2.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0

interface gigabitEthernet0/2.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0

interface gigabitEthernet0/2
no shutdown
```

## Switch Security 

Basic L2 security principles are to shutdown all unused ports and move them to blackhole vlan, use port-security, disable trunking in all access ports and so on.
