Building configuration...

Current configuration : 1015 bytes
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname R14
!
boot-start-marker
boot-end-marker
!
!
!
no aaa new-model
mmi polling-interval 60
no mmi auto-configure
no mmi pvc
mmi snmp-timeout 180
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
multilink bundle-name authenticated
!
!
!
!
!
!
!
!
!
redundancy
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
!
interface Loopback0
 ip address 10.20.0.1 255.255.255.255
!
interface Ethernet0/0
 description Link_to_R12
 ip address 10.10.0.13 255.255.255.252
!
interface Ethernet0/1
 description Link_to_R13
 ip address 10.10.0.9 255.255.255.252
!
interface Ethernet0/2
 description Link_to_R22
 ip address 10.10.0.5 255.255.255.252
!
interface Ethernet0/3
 description Link_to_R19
 ip address 10.10.0.1 255.255.255.252
!
ip forward-protocol nd
!
!
no ip http server
no ip http secure-server
!
!
!
!
control-plane
!
!
!
!
!
!         
!
line con 0
 logging synchronous
line aux 0
line vty 0 4
 login
 transport input all
!
!
end