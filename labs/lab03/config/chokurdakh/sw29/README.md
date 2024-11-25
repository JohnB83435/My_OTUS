Building configuration...

Current configuration : 1028 bytes
!
! Last configuration change at 15:24:33 UTC Thu Nov 14 2024
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname SW29
!
boot-start-marker
boot-end-marker
!
!
!
no aaa new-model
!
!
!
!
!         
!
!
!
ip cef
no ipv6 cef
!
!
spanning-tree mode pvst
spanning-tree extend system-id
!
vlan internal allocation policy ascending
!
! 
!
!
!
!
!
!
!
!
!
!         
!
interface Ethernet0/0
 switchport access vlan 103
 switchport mode access
!
interface Ethernet0/1
 switchport access vlan 101
 switchport mode access
!
interface Ethernet0/2
 switchport trunk allowed vlan 101,103
 switchport trunk encapsulation dot1q
 switchport mode trunk
!
interface Ethernet0/3
!
interface Vlan265
 description MGMT
 ip address 10.30.2.29 255.255.255.0
!
ip forward-protocol nd
!
no ip http server
no ip http secure-server
!
ip route 0.0.0.0 0.0.0.0 10.30.2.1
!
!
!
!
!
control-plane
!
!
line con 0
 logging synchronous
line aux 0
line vty 0 4
 login
!
!
end