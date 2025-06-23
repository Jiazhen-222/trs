**//name (multilayerswitch 2)(MS1)**
en
conf t
hostname MS1

vlan 2
name Server
vlan 10
name IT_Department
vlan 20
name Logistics_Department
vlan 30
name Sales_Department
vlan 88
name Management
vlan 99
name native
vlan 100
name Unuse

exit
int vlan 2
ip add 205.72.2.1 255.255.255.0
no shut
int vlan 10
ip add 205.72.10.1 255.255.255.0
no shut
int vlan 20
ip add 205.72.20.1 255.255.255.0
no shut
int vlan 30
ip add 205.72.30.1 255.255.255.0
no shut
end
copy run start

conf t
vtp mode server
vtp domain lmg.com

vtp version 2
int range fa0/1, fa0/3, fa0/5
switchport trunk encapsulation dot1q
switchport mode trunk 
exit

int fa0/7
switchport mode access
switchport access vlan 2

int vlan 10
ip helper-address 205.72.2.10
int vlan 20
ip helper-address 205.72.2.10
int vlan 30
ip helper-address 205.72.2.10


**//name IT (switch 1)**
en
conf t
hostname IT_switch
vlan 2
name Server
vlan 10
name IT_Department
vlan 20
name Logistic_Department
vlan 30
name Sales_Department
vlan 88
name Management
vlan 99
name Native
vlan 100
name Unuse
exit

int fa0/1
switchport mode trunk

int range fa0/5 - 10
switchport mode access
switchport access vlan 10
no shut

int range fa0/11 - 24, g0/1-2
switchport mode access
switchport access vlan 100
end 
copy run start

//name Logi (switch 2)
en
conf t
hostname Logistics_switch
vlan 2
name Server
vlan 10
name IT_Department
vlan 20
name Logistic_Department
vlan 30
name Sales_Department
vlan 88
name Management
vlan 99
name Native
vlan 100
name Unuse
exit

int fa0/1
switchport mode trunk

int range fa0/5 - 10
switchport mode access
switchport access vlan 20
no shut

int range fa0/11 - 24, g0/1-2
switchport mode access
switchport access vlan 100
end 
copy run start

//name Sales(switch 3)
en
conf t
hostname Sales_switch
vlan 2
name Server
vlan 10
name IT_Department
vlan 20
name Logistic_Department
vlan 30
name Sales_Department
vlan 88
name Management
vlan 99
name Native
vlan 100
name Unuse
exit

int fa0/1
switchport mode trunk

int range fa0/5 - 10
switchport mode access
switchport access vlan 30
no shut

int range fa0/11 - 24, g0/1-2
switchport mode access
switchport access vlan 100
end 
copy run start

//router mlc
en 
conf t
int g/0
no shut
int g0/0.10
encapsulation dot1q 10
ip address 205.72.10.1 255.255.255.0
exit

int g0/0.20
encapsulation dot1q 20
ip address 205.72.20.1 255.255.255.0
exit


int g0/0.30
encapsulation dot1q 30
ip address 205.72.30.1 255.255.255.0
exit

