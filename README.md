# Hospital-Networking-Management-System-Cisco-Packet-Tracer-
# Project Overview <br>
This project demonstrates the implementation of a Local Area Network (LAN) for a multi-floor hospital using Cisco Packet Tracer (CPT). The hotel's network infrastructure comprises three floors: the ground floor, first floor, and second floor, each containing rooms with specific purposes. The network elements, including PCs, IP phones, and printers, are interconnected through switches, and all switches are further linked with a common router that provides connectivity on each floor. Proper IP addressing has been configured for each sector of the network, ensuring seamless communication and optimal functionality. The entire network setup is virtually simulated using Cisco Packet Tracer (CPT), leveraging the technology of Cisco Certified Network Associate (CCNA).

<br>

# Complete Topology: <br><img width="1599" height="673" alt="Image" src="https://github.com/user-attachments/assets/3b5a1b14-a559-4a8c-9005-d19f3a186c6a" />
<br>
The hospital departments are distributed floor-wise, and each department is isolated using VLANs for security and traffic management. Routers and switches form the backbone of the network, while end devices (PCs, IP Phones, and printers) are connected to each VLAN. The network is designed to be scalable, modular, and secure, making it suitable for real enterprise environments.

<br>
# First Floor
<br>
<img width="757" height="530" alt="Image" src="https://github.com/user-attachments/assets/608bf119-b58b-4e04-a2f8-6d7fa810453b" />
<br>
# Devices Used:

End Devices:

3 PCs (PC5, PC6, PC7)

3 Printers (Printer5, Printer6, Printer7)

1 Laptop (Laptop0)

1 Smartphone (Smartphone2)

Networking Devices:

1 Switch (2960-24TT)

1 Access Point (Access Point4)

Router (connected via Fa0/1 to switch)

VLANs Configured:

VLAN 60 → 192.168.6.0/24 (PC5 + Printer5)

VLAN 70 → 192.168.7.0/24 (PC6 + Printer6)

VLAN 80 → 192.168.8.0/24 (PC7 + Printer7)

Connections:

PCs and Printers connected to the switch (Fa0/3–Fa0/7).

Access Point provides WiFi for Laptop0 and Smartphone2.

Router provides Inter-VLAN routing + DHCP.
# Complete Configuration  <br>
Router1 Configuration<br>
hostname Router1<br>
!<br>
ip dhcp pool VLAN60<br>
 network 192.168.6.0 255.255.255.0<br>
 default-router 192.168.6.1<br>
 dns-server 192.168.6.2<br>
!<br>
ip dhcp pool VLAN70<br>
 network 192.168.7.0 255.255.255.0<br>
 default-router 192.168.7.1<br>
 dns-server 192.168.7.2<br>
!<br>
ip dhcp pool VLAN80<br>
 network 192.168.8.0 255.255.255.0<br>
 default-router 192.168.8.1<br>
 dns-server 192.168.8.2<br>
!<br>
interface g0/0.60<br>
 encapsulation dot1Q 60<br>
 ip address 192.168.6.1 255.255.255.0<br>
!<br>
interface g0/0.70<br>
 encapsulation dot1Q 70<br>
 ip address 192.168.7.1 255.255.255.0<br>
!<br>
interface g0/0.80<br>
 encapsulation dot1Q 80<br>
 ip address 192.168.8.1 255.255.255.0<br>
!<br>
interface s0/3/0<br>
 ip address 10.10.10.1 255.255.255.252<br>
 clock rate 64000<br>
 no shutdown<br>
!<br>
interface s0/3/1<br>
 ip address 10.10.10.10 255.255.255.252<br>
 clock rate 64000<br>
 no shutdown<br>
!<br>
router ospf 10<br>
 network 192.168.6.0 0.0.0.255 area 0<br>
 network 192.168.7.0 0.0.0.255 area 0<br>
 network 192.168.8.0 0.0.0.255 area 0<br>
 network 10.10.10.0 0.0.0.3 area 0<br>
 network 10.10.10.8 0.0.0.3 area 0<br>
!<br>
username abhi secret cisco123<br>
ip domain-name hospital.local<br>
crypto key generate rsa<br>
ip ssh version 2<br>
line vty 0 4<br>
 transport input ssh<br>
 login local<br>

 <br>
 Switch1 Configuration<br>
 hostname Switch1<br>
!<br>
vlan 60<br>
 name HR<br>
vlan 70<br>
 name Finance<br>
vlan 80<br>
 name Management<br>
!<br>
interface fa0/1<br>
 switchport mode trunk<br>
 switchport trunk allowed vlan 1,60,70,80<br>
!<br>
interface fa0/2<br>
 switchport mode access<br>
 switchport access vlan 60<br>
!<br>
interface fa0/3<br>
 switchport mode access<br>
 switchport access vlan 60<br>
!<br>
interface fa0/4<br>
 switchport mode access<br>
 switchport access vlan 70<br>
!<br>
interface fa0/5<br>
 switchport mode access<br>
 switchport access vlan 70<br>
!<br>
interface fa0/6<br>
 switchport mode access<br>
 switchport access vlan 80<br>
!<br>
interface fa0/7<br>
 switchport mode access<br>
 switchport access vlan 80<br>
!<br>
interface fa0/8<br>
 switchport mode access<br>
 switchport access vlan 60<br>
<br>
# Second-Floor  <br>






