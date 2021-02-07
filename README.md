Core 1 Asign Ip
-----------------
en
conf t
hostname Core 1
int fa0/9
no switchport 
ip add 192.168.1.1 255.255.255.0 
no shut
exit
ip routing

Core 2 Asign Ip
-----------------
en
conf t
hostname Core 2
int fa0/10
no switchport 
ip add 192.168.2.1 255.255.255.0 
no shut
exit
ip routing

HQ1 Asign IP 
-------------------
en
conf t
hostname HQ1
int g0/0
ip add 192.168.1.2 255.255.255.0
no shut
int se0/0/0
ip add 20.20.20.1 255.255.255.0
no shut


HQ2 Asign IP
----------------------------
en
conf t
hostname HQ2
int g0/0
ip add 192.168.2.2 255.255.255.0
no shut
int se0/0/0
ip add 11.11.11.1 255.255.255.250
no shut

ISP1 Asign IP
----------------------- 
en
conf t
int se0/0/0
ip add 20.20.20.2 255.255.255.0
no shut
int lo1
ip add 8.8.8.8 255.255.255.0
no shut

ISP2 Asign IP
----------------------------
en 
conf t
int se0/0/0
ip add 11.11.11.2 255.255.255.0
no shut
int lo1
ip add 8.8.8.8 255.255.255.0
no shut

Core 1 Create VLANs
-------------------------------
en
conf t
vlan 10
name sales
vlan 20
name accountant
vlan 30
name HR
vlan 40
name servers
vlan 50 
name voice

Core 1 Config VTP server 
-----------------------------
en
conf t
vtp mode server
vtp domain awgab
vtp version 2


Core 2 Config VTP server
---------------------------------------------
en
conf t
vtp mode server
vtp domain awgab
vtp version 2


Core 1 Trunk ports
-------------------------------------
int range fa0/1-8
switchport trunk encapsulation dot1q
switchport mode trunk

 
Core 2 Trunk ports
-------------------------------------
int range fa0/1-8
switchport trunk encapsulation dot1q
switchport mode trunk



ASW1 Config VTP client 
---------------------------------------
en
conf t
hostname ASW1
vtp mode client
vtp domain awgab
vtp version 2
exit


ASW2 Config VTP client 
---------------------------------------
en
conf t
hostname ASW2
vtp mode client
vtp domain awgab
vtp version 2
exit

ASW3 Config VTP client 
---------------------------------------
en
conf t
hostname ASW3
vtp mode client
vtp domain awgab
vtp version 2
exit

ASW4 Config VTP client 
---------------------------------------
en
conf t
hostname ASW4
vtp mode client
vtp domain awgab
vtp version 2
exit


ASW1 Create Trunk ports and access ports
-----------------------------------------

en
conf t
int range fa0/5-6
switchport trunk encapsulation dot1q
switchport mode trunk
exit

int range fa0/1-4
switchport mode access
switchport access vlan 40
exit

ASW2 Create Trunk ports and access ports
-----------------------------------------

en
conf t
int range fa0/5-6
switchport trunk encapsulation dot1q
switchport mode trunk
exit

int range fa0/1-4
switchport mode access
switchport access vlan 30
switchport voice vlan 50
exit


ASW3 Create Trunk ports and access ports
-----------------------------------------

en
conf t
int range fa0/5-6
switchport trunk encapsulation dot1q
switchport mode trunk
exit

int range fa0/1-4
switchport mode access
switchport access vlan 20
switchport voice vlan 50
exit


ASW4 Create Trunk ports and access ports
-----------------------------------------

en
conf t
int range fa0/5-6
switchport trunk encapsulation dot1q
switchport mode trunk
exit

int range fa0/1-4
switchport mode access
switchport access vlan 10
switchport voice vlan 50
exit

Core 1 Create Ether-channel
--------------------------------
en
conf t
int range fa0/5-8
channel-group 12 mode desirable
exit

Core 2 Create Ether-channel
----------------------------
en
conf t
int range fa0/5-8
channel-group 12 mode auto
exit


Core 1 Create DHCP pool for vlans
----------------------------------------
ip dhcp pool Sales
default-route 192.168.10.3 
network 192.168.10.0 255.255.255.0

ip dhcp pool accountant
default-route 192.168.20.3
network 192.168.20.0 255.255.255.0

ip dhcp pool HR
default-route 192.168.30.3
network 192.168.30.0 255.255.255.0

ip dhcp pool servers
default-route 192.168.40.3
network 192.168.40.0 255.255.255.0

ip dhcp pool voice
default-route 192.168.50.3
network 192.168.50.0 255.255.255.0



Core 1 SVI config
-----------------------------
int vlan 10
ip add 192.168.10.1 255.255.255.0
no shut

int vlan 20
ip add 192.168.20.1 255.255.255.0
no shut

int vlan 30
ip add 192.168.30.1 255.255.255.0
no shut

int vlan 40
ip add 192.168.40.1 255.255.255.0
no shut



int vlan 50
ip add 192.168.50.1 255.255.255.0
no shut


Core 2 SVI config
-----------------------------
int vlan 10
ip add 192.168.10.2 255.255.255.0
no shut

int vlan 20
ip add 192.168.20.2 255.255.255.0
no shut

int vlan 30
ip add 192.168.30.2 255.255.255.0
no shut

int vlan 40
ip add 192.168.40.2 255.255.255.0
no shut



int vlan 50
ip add 192.168.50.2 255.255.255.0
no shut



Core 1 Config HSRP
=========================
int vlan 10
standby 10 ip 192.168.10.3
standby 10 preempt

int vlan 20
standby 20 ip 192.168.20.3
standby 20 preempt

int vlan 30
standby 30 ip 192.168.30.3
standby 30 preempt


int vlan 40
standby 40 ip 192.168.40.3
standby 40 preempt

int vlan 50
standby 50 ip 192.168.50.3
standby 50 preempt


Core 2 Config HSRP
=========================
int vlan 10
standby 10 ip 192.168.10.3
standby 10 preempt

int vlan 20
standby 20 ip 192.168.20.3
standby 20 preempt

int vlan 30
standby 30 ip 192.168.30.3
standby 30 preempt


int vlan 40
standby 40 ip 192.168.40.3
standby 40 preempt

int vlan 50
standby 50 ip 192.168.50.3
standby 50 preempt


Core 1 OSPF 
------------------------






Core 2 OSPF
-------------------



HQ1
===================





HQ2
-------------------
