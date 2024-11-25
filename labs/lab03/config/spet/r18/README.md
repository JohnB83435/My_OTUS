Building configuration...

Current configuration : 1018 bytes
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname R18
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
 ip address 10.20.1.1 255.255.255.255
!
interface Ethernet0/0
 description Link_to_R16
 ip address 10.10.0.69 255.255.255.252
!
interface Ethernet0/1
 description Link_to_R17
 ip address 10.10.0.73 255.255.255.252
!
interface Ethernet0/2
 description Link_to_R24
 ip address 10.10.0.62 255.255.255.252
!
interface Ethernet0/3
 description Link_to_R26
 ip address 10.10.0.66 255.255.255.252
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