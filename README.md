Project Documentation
Project/Documentation: Design and Build an Enterprise Small Office Network using Cisco Packet Tracer
Objective
The objective of this project is to design, configure, and simulate a small office network using Cisco Packet Tracer, showcasing VLAN segmentation, inter-VLAN routing, HSRP-based redundancy, NAT configuration, and overall network security. 
Network Overview
•	Devices Used: 2 MLS {MLS switch (MLS 1, MLS 2)}, 2 Switches (SW1, SW2), 6 PCs, 1 ISP Router
•	Software: Cisco Packet Tracer
•	VLANs: VLAN 10 (Management), VLAN 20 (Voice), VLAN 30 (Data)
•	Topology: R1 and R2 configured for inter-VLAN routing and redundancy, SW1–SW2 connected via EtherChannel trunk, R2 connected to ISP via NAT, HSRP configured for gateway redundancy

 

Key Configurations
•	Created VLANs 10, 20, and 30 and assigned respective ports on switches.
•	Configured Inter-VLAN routing using sub interfaces {Router on stick} on routers.
•	Implemented HSRP between R1 and R2 for gateway redundancy.
•	Established an EtherChannel trunk between SW1 and SW2.
•	Configured NAT overload on R2 for Internet access.
•	Applied ACLs to secure internal networks and control traffic flow.
•	Verified end-to-end connectivity and Internet access through simulations.


Network Topology Overview{example}
Device	Interface	IP Address	VLAN / Purpose
MLS1	G0/0/0.10	192.168.10.1	VLAN 10 (Mgmt)
MLS1	G0/0/0.20	192.168.20.1	VLAN 20 (Voice)
MLS1	G0/0/0.30	192.168.30.1	VLAN 30 (Data)
MLS2	G0/0/0.10	192.168.10.2	VLAN 10 (Mgmt)
MLS2	G0/0/0.20	192.168.20.2	VLAN 20 (Voice)
MLS2	G0/0/0.30	192.168.30.2	VLAN 30 (Data)
MLS1– MLS2 Interconnect	G0/0/1 ↔ G0/0/1	192.168.100.0/30	Router-to-Router Link
MLS2–ISP	S0/1/0 ↔ S0/1/0	203.0.113.2 / 203.0.113.1	WAN Connection
PCs	Fa0	192.168.10.x / 20.x / 30.x	Client Machines


Check/Ensure at last
Configure/check on end devices ping to check reachability. 

Outcome
Successfully built and tested a functional small office network supporting inter-VLAN communication, gateway redundancy using HSRP, and Internet access via NAT.
Skills Demonstrated
•	Network Design and Planning
•	Routing and Switching Configuration
•	VLAN and Subnet Management
•	HSRP, NAT, and ACL Implementation
•	Network Troubleshooting and Documentation


exapmle of CLI

Configuration Demonstration (CLI Samples)
1.	VLAN Creation on Switches:
SW1(config)# vlan 10
SW1(config-vlan)# name MANAGEMENT
SW1(config)# vlan 20
SW1(config-vlan)# name VOICE
SW1(config)# vlan 30
SW1(config-vlan)# name DATA
Verification:
show vlan brief
Result: VLANs successfully created and active on respective ports.
{{optional 
2.	 Inter-VLAN Routing on Routers:
interface g0/0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
!
interface g0/0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
!
interface g0/0/0.30
 encapsulation dot1Q 30
 ip address 192.168.30.1 255.255.255.0
Result: Each VLAN can now route via router-on-a-stick configuration.}}
3.	HSRP Configuration:
interface g0/0/0.10
 standby 10 ip 192.168.10.254
 standby 10 priority 110
 standby 10 preempt
!
interface g0/0/0.20
 standby 20 ip 192.168.20.254
 standby 20 priority 110
 standby 20 preempt
Verification:
show standby brief
Result: HSRP configured for gateway redundancy.
4.	NAT Configuration (R2 – Internet Gateway):
access-list 1 permit 192.168.10.0 0.0.0.255
access-list 1 permit 192.168.20.0 0.0.0.255
access-list 1 permit 192.168.30.0 0.0.0.255
ip nat inside source list 1 interface s0/1/0 overload

interface s0/1/0
 ip nat outside
interface g0/0/0.10
 ip nat inside
interface g0/0/0.20
 ip nat inside
interface g0/0/0.30
 ip nat inside
Verification:
show ip nat translations
Result: NAT Overload configured successfully.
5.	Connectivity Testing:
PC> ping 8.8.8.8
PC> tracert 8.8.8.8
Result: Successful Internet reachability through R2’s NAT.


