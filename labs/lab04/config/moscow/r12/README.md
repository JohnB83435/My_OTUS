Building configuration...

Current configuration : 2413 bytes

version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption

hostname R12

boot-start-marker
boot-end-marker

no aaa new-model
mmi polling-interval 60
no mmi auto-configure
no mmi pvc
mmi snmp-timeout 180

ip cef
no ipv6 cef

multilink bundle-name authenticated

redundancy
      
track 1 ip sla 1 reachability
 delay down 15 up 15

interface Loopback0
 ip address 10.20.0.4 255.255.255.255

interface Ethernet0/0
 no ip address
 ip policy route-map TO_LAMAS

interface Ethernet0/0.3
 description SRV
 encapsulation dot1Q 3
 ip address 10.12.0.2 255.255.255.0
 standby version 2
 standby 0 ip 10.12.0.1
 standby 0 preempt

interface Ethernet0/0.103
 description BUH
 encapsulation dot1Q 103
 ip address 10.12.1.2 255.255.255.0
 standby version 2
 standby 0 ip 10.12.1.1
 standby 0 preempt
 ip policy route-map TO_LAMAS

interface Ethernet0/0.265
 description MGMT
 encapsulation dot1Q 265
 ip address 10.30.0.2 255.255.255.0
 standby version 2
 standby 0 ip 10.30.0.1
 standby 0 preempt
       
interface Ethernet0/1
 no ip address
 ip policy route-map TO_LAMAS

interface Ethernet0/1.3
 description SRV
 encapsulation dot1Q 3

interface Ethernet0/1.103
 description BUH
 encapsulation dot1Q 103

interface Ethernet0/1.265
 description SRV
 encapsulation dot1Q 265

interface Ethernet0/2
 description Link_to_R14
 ip address 10.10.0.14 255.255.255.252

interface Ethernet0/3
 description Link_to_R15
 ip address 10.10.0.26 255.255.255.252

interface Ethernet1/0
 no ip address
 shutdown

interface Ethernet1/1
 no ip address
 shutdown

interface Ethernet1/2
 no ip address
 shutdown

interface Ethernet1/3
 no ip address
 shutdown

ip forward-protocol nd

no ip http server
no ip http secure-server
ip route 0.0.0.0 0.0.0.0 10.10.0.13 40 track 1
ip route 0.0.0.0 0.0.0.0 10.10.0.25 100
ip route 10.10.0.6 255.255.255.255 Ethernet0/2 10.10.0.13 permanent

ip access-list standard TO_LAMAS
 permit 10.12.1.4

ip sla auto discovery
ip sla 1
 icmp-echo 10.10.0.6 source-interface Ethernet0/2
 threshold 20
 timeout 20
 frequency 5
ip sla schedule 1 start-time now

route-map TO_LAMAS permit 10
 match ip address TO_LAMAS
 set ip next-hop 10.10.0.25

control-plane

line con 0
 logging synchronous
line aux 0
line vty 0 4
 login
 transport input all


end
