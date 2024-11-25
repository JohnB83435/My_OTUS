Building configuration...

Current configuration : 1823 bytes
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname R12
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
 ip address 10.20.0.4 255.255.255.255
!
interface Ethernet0/0
 no ip address
!
interface Ethernet0/0.3
 description SRV
 encapsulation dot1Q 3
 ip address 10.12.0.2 255.255.255.0
 standby version 2
 standby 0 ip 10.12.0.1
 standby 0 preempt
!
interface Ethernet0/0.103
 description BUH
 encapsulation dot1Q 103
 ip address 10.12.1.2 255.255.255.0
 standby version 2
 standby 0 ip 10.12.1.1
 standby 0 preempt
!
interface Ethernet0/0.265
 description MGMT
 encapsulation dot1Q 265
 ip address 10.30.0.2 255.255.255.0
 standby version 2
 standby 0 ip 10.30.0.1
 standby 0 preempt
!
interface Ethernet0/1
 no ip address
!
interface Ethernet0/1.3
 description SRV
 encapsulation dot1Q 3
!
interface Ethernet0/1.103
 description BUH
 encapsulation dot1Q 103
!
interface Ethernet0/1.265
 description SRV
 encapsulation dot1Q 265
!
interface Ethernet0/2
 description Link_to_R14
 ip address 10.10.0.14 255.255.255.252
!
interface Ethernet0/3
 description Link_to_R15
 ip address 10.10.0.26 255.255.255.252
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
