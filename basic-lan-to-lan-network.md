## Cisco Packet Tracer basic LAN to LAN. 

In this project I create simple LAN network with the following setup: 

- 2 hosts (PC1 and PC2)
- 2 switches (Switch1 and Switch2)
- 2 routers (Router1 and Router2)

## Network Topology 



<img width="2078" height="822" alt="image" src="https://github.com/user-attachments/assets/9f0fb860-8721-4da8-9354-425948a38422" />




## Connections

PC1 to Swicht1 - F0/0 to F0/1
PC2 to Swicht2 - F0/0 to F0/1

Switch1 to Router1 - G0/1 to G0/0 
Switch2 to Router2 - G0/1 to G0/0 

Router1 to Router2 - G0/0 to G0/1





## Addressing Table 

Network - LAN1 - 192.168.1.0/24
- PC1 - 192.168.1.10
- Switch1 - 192.168.1.2
- Router1 - 192.168.1.1


Network - LAN2 - 192.168.2.0/24 
- PC2 - 192.168.2.20
- Switch2 - 192.168.1.2
- Router1 - 192.168.2.1

Network LAN3 - 10.10.10.0/30 
 - Router1 - 10.10.10.1
 - Router2 - 10.10.10.2


## Router basic configuration

### LAN3 Routers configuration

In this part I configured IP addresses for R1 and R2 interfaces.

Router1

Configuring interface G0/0 with IP address `10.10.10.1`. 
<img width="1400" height="1408" alt="image" src="https://github.com/user-attachments/assets/74c4c04e-f542-4288-b987-3f618ceabcd0" />

Configurin inteface G0/1 with IP address `192.168.1.1`.

<img width="1270" height="524" alt="image" src="https://github.com/user-attachments/assets/90110d37-d4ca-4bc6-b4fb-026878e1ad95" />


Router2

Configuring interface G0/1 with IP address `10.10.10.2`.
<img width="1394" height="1416" alt="image" src="https://github.com/user-attachments/assets/006c6479-3115-4d59-b702-f5839cbbe8ce" />

Configuring interface G0/0 with IP address `192.168.2.0`.


<img width="1262" height="294" alt="image" src="https://github.com/user-attachments/assets/b0ad3348-c942-4686-b5cb-3e72704b75d2" />


I also configured hostnames for Router1 and Router2


## Switch basic configuartion 


## Static Routing 

In this part I configure static rounting for R1 and R2. 

#### R1
To configure static routing for R1 is used the following command `ip route 192.168.2.0 255.255.255.0 10.10.10.2`. Destination address, subnet mask, Next-hop router's IP address. 


<img width="1386" height="1412" alt="image" src="https://github.com/user-attachments/assets/5ecc101e-980a-4dd4-9219-e090f1f46be8" />

#### R2 

I used the same command for R2 `ip route 192.168.1.0 255.255.255.0 10.10.10.1`. 

<img width="1394" height="1408" alt="image" src="https://github.com/user-attachments/assets/525233c9-29e8-4454-bb96-2f130df8b311" />


## Configuring IP addresses for PC1 and PC2

Configuring IP addresses for PC1 and PC2 is straight forward, I don't use DHCP this time so I set static IP addresses for both devices. 

<img width="1396" height="1398" alt="image" src="https://github.com/user-attachments/assets/c64eb16e-c6ef-4766-b34e-2b87aed5c830" />


## Testing network connectivity with ping. Pinging PC2 from PC1 is successfull, therefore conclusion is that the basic network works. 


<img width="1394" height="1424" alt="image" src="https://github.com/user-attachments/assets/0e1aeb92-bebe-4a1a-b3b7-5cef26141622" />

