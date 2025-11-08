## Cisco Packet Tracer basic LAN to LAN. 

In this project I create simple LAN network with the following setup: 

- 2 hosts (PC1 and PC2)
- 2 switches (Switch1 and Switch2)
- 2 routers (Router1 and Router2)

## Network Topology 



<img width="2062" height="730" alt="image" src="https://github.com/user-attachments/assets/e5c0af05-0041-4974-beaf-851384dcfba9" />



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


## Switch basic configuartion 


## Static Routing 



