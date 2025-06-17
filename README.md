//name vlan 10-30(multilayerswitch 2)
en
conf t
vlan 10
name IT_Department
vlan 20
name Logistics_Department
vlan 30
name Sales_Department

exit
int range fa0/1-2
switchport access vlan 10
exit
int range fa0/3-4
switchport access vlan 20
exit
int range fa0/5-6
switchport access vlan 30

//name vlan 10-30(multilayerswitch 3)
en
conf t
vlan 10
name IT_Department
vlan 20
name Logistics_Department
vlan 30
name Sales_Department

exit
int range fa0/1-2
switchport access vlan 10
exit
int range fa0/3-4
switchport access vlan 20
exit
int range fa0/5-6
switchport access vlan 30


//name vlan 10 (switch 1)
en
conf t
vlan 10
name IT_Department
exit
int range fa0/5 - 10
switchport access vlan 10
no shut

//name vlan 20 (switch 2)
en
conf t
vlan 20
name Logistics_Department
exit
int range fa0/5 - 10
switchport access vlan 20
no shut

//name vlan 30 (switch 3)
en
conf t
vlan 30
name Sales_Department
exit
int range fa0/5 - 10
switchport access vlan 30
no shut
