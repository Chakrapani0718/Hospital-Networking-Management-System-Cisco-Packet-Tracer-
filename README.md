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

 Router One Output:<img width="975" height="681" alt="Image" src="https://github.com/user-attachments/assets/c20f467c-935b-476b-aed4-acb23a702fd8" />

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
Switch One Output:<img width="954" height="641" alt="Image" src="https://github.com/user-attachments/assets/7be549d4-0794-496b-a630-232d55cd4b2d" />

# Second-Floor  <br>
<img width="769" height="358" alt="Image" src="https://github.com/user-attachments/assets/a006d27f-cff2-444a-bbd1-fb99145bf087" />
<br>

Devices Used:

End Devices:

3 PCs (PC2, PC3, PC4)

3 Printers (Printer2, Printer3, Printer4)

1 Laptop (Laptop1)

1 Smartphone (Smartphone0)

Networking Devices:

1 Switch (2960-24TT)

1 Access Point (Access Point5)

Router (Gig0/0 interface connected to switch)

VLANs Configured:

VLAN 30 → 192.168.3.0/24 (PC2 + Printer2)

VLAN 40 → 192.168.4.0/24 (PC3 + Printer3)

VLAN 50 → 192.168.5.0/24 (PC4 + Printer4)

Connections:

PCs and Printers connected to switch (Fa0/3–Fa0/7).

Access Point provides WiFi for Laptop1 and Smartphone0.

Router provides DHCP, Inter-VLAN routing, and OSPF.
# Complete Configuration  <br>
hostname Router2
!
ip dhcp pool VLAN30
 network 192.168.3.0 255.255.255.0
 default-router 192.168.3.1
 dns-server 8.8.8.8
!
ip dhcp pool VLAN40
 network 192.168.4.0 255.255.255.0
 default-router 192.168.4.1
 dns-server 8.8.8.8
!
ip dhcp pool VLAN50
 network 192.168.5.0 255.255.255.0
 default-router 192.168.5.1
 dns-server 8.8.8.8
!
interface g0/0.30
 encapsulation dot1Q 30
 ip address 192.168.3.1 255.255.255.0
!
interface g0/0.40
 encapsulation dot1Q 40
 ip address 192.168.4.1 255.255.255.0
!
interface g0/0.50
 encapsulation dot1Q 50
 ip address 192.168.5.1 255.255.255.0
!
interface s0/3/0
 ip address 10.10.10.5 255.255.255.252
 no shutdown
!
interface s0/3/1
 ip address 10.10.10.9 255.255.255.252
 no shutdown
!
router ospf 10
 network 192.168.3.0 0.0.0.255 area 0
 network 192.168.4.0 0.0.0.255 area 0
 network 192.168.5.0 0.0.0.255 area 0
 network 10.10.10.4 0.0.0.3 area 0
 network 10.10.10.8 0.0.0.3 area 0
!
username chetan secret cisco123
ip domain-name hospital.local
crypto key generate rsa
ip ssh version 2
line vty 0 4
 transport input ssh
 login local<br>
 Router Two Output:<img width="988" height="614" alt="Image" src="https://github.com/user-attachments/assets/ec4b84ad-2b26-40ac-9bff-5a435e6b8489" />
 <br>
Switch2 Configuration
hostname Switch2
!
vlan 30
 name Reception
vlan 40
 name Pharmacy
vlan 50
 name Nursing
!
interface fa0/1
 switchport mode trunk
 switchport trunk allowed vlan 1,30,40,50
!
interface fa0/2
 switchport mode access
 switchport access vlan 30
!
interface fa0/3
 switchport mode access
 switchport access vlan 30
!
interface fa0/4
 switchport mode access
 switchport access vlan 40
!
interface fa0/5
 switchport mode access
 switchport access vlan 40
!
interface fa0/6
 switchport mode access
 switchport access vlan 50
!
interface fa0/7
 switchport mode access
 switchport access vlan 50
!
interface fa0/8
 switchport mode access
 switchport access vlan 50<br>

 Switch Two Output:<img width="891" height="595" alt="Image" src="https://github.com/user-attachments/assets/3e7c8835-3ffb-4dde-96ca-136cfd0c5ba0" />

# Third-Floor  <br>
<img width="799" height="308" alt="Image" src="https://github.com/user-attachments/assets/3533bff2-3684-4ef0-a492-1ee0b5dde528" />

<br>
# Devices Used:
End Devices:

2 PCs (PC0, PC1)

2 Printers (Printer0, Printer1)

1 Laptop (Laptop2)

1 Smartphone (Smartphone1)

Networking Devices:

1 Switch (2960-24TT)

1 Access Point (Access Point6)

Router (connected via Fa0/1 to switch)

VLANs Configured:

VLAN 10 → 192.168.1.0/24 (PC0 + Printer0)

VLAN 20 → 192.168.2.0/24 (PC1 + Printer1)

# Complete Configuration  <br>
Router 3 Configuration

hostname Router3
!
ip dhcp pool VLAN10
 network 192.168.1.0 255.255.255.0
 default-router 192.168.1.1
 dns-server 8.8.8.8
!
ip dhcp pool VLAN20
 network 192.168.2.0 255.255.255.0
 default-router 192.168.2.1
 dns-server 8.8.8.8
!
interface g0/0.10
 encapsulation dot1Q 10
 ip address 192.168.1.1 255.255.255.0
!
interface g0/0.20
 encapsulation dot1Q 20
 ip address 192.168.2.1 255.255.255.0
!
interface s0/3/0
 ip address 10.10.10.2 255.255.255.252
 clock rate 64000
 no shutdown
!
interface s0/3/1
 ip address 10.10.10.6 255.255.255.252
 no shutdown
!
router ospf 10
 network 192.168.1.0 0.0.0.255 area 0
 network 192.168.2.0 0.0.0.255 area 0
 network 10.10.10.0 0.0.0.3 area 0
 network 10.10.10.4 0.0.0.3 area 0
!
username mani secret cisco123
ip domain-name hospital.local
crypto key generate rsa
ip ssh version 2
line vty 0 4
 transport input ssh
 login local

<br>








