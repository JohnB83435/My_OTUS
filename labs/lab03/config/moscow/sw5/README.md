Building configuration...

Current configuration : 1888 bytes
!
! Last configuration change at 17:42:05 UTC Wed Nov 13 2024
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname SW5
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
interface Port-channel1
 description Trunk_to_SW4
 switchport trunk allowed vlan 3,101-104,265
 switchport trunk encapsulation dot1q
 switchport mode trunk
 spanning-tree port-priority 192
 spanning-tree cost 200
!
interface Ethernet0/0
 switchport trunk allowed vlan 3,103,265
 switchport trunk encapsulation dot1q
 switchport mode trunk
!
interface Ethernet0/1
 switchport trunk allowed vlan 3,101-104,265
 switchport trunk encapsulation dot1q
 switchport mode trunk
!
interface Ethernet0/2
 description LACP
 switchport trunk allowed vlan 3,101-104,265
 switchport trunk encapsulation dot1q
 switchport mode trunk
 channel-protocol lacp
 channel-group 1 mode active
!
interface Ethernet0/3
 description LACP
 switchport trunk allowed vlan 3,101-104,265
 switchport trunk encapsulation dot1q
 switchport mode trunk
 channel-protocol lacp
 channel-group 1 mode active
!
interface Ethernet1/0
 switchport trunk allowed vlan 3,101-104,265
 switchport trunk encapsulation dot1q
 switchport mode trunk
!
interface Ethernet1/1
 switchport trunk allowed vlan 3,101-104,265
 switchport trunk encapsulation dot1q
 switchport mode trunk
!
interface Ethernet1/2
!
interface Ethernet1/3
!
interface Vlan265
 ip address 10.30.0.50 255.255.255.0
!
ip forward-protocol nd
!
no ip http server
no ip http secure-server
!
ip route 0.0.0.0 0.0.0.0 10.30.0.1
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
