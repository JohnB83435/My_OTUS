Building configuration...

Current configuration : 1175 bytes
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname R23
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
 ip address 10.20.4.1 255.255.255.255
!
interface Ethernet0/0
 description Link_to_R22
 ip address 10.10.0.38 255.255.255.252
!
interface Ethernet0/1
 description Link_to_R25
 ip address 10.10.0.49 255.255.255.252
!
interface Ethernet0/2
 description Link_to_R24
 ip address 10.10.0.45 255.255.255.252
!
interface Ethernet0/3
 no ip address
 shutdown
!
interface Ethernet1/0
 no ip address
 shutdown
!
interface Ethernet1/1
 no ip address
 shutdown
!
interface Ethernet1/2
 no ip address
 shutdown
!
interface Ethernet1/3
 no ip address
 shutdown
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