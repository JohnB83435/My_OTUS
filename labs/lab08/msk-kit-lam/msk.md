### hostname R14

interface Loopback0  
 ip address 10.20.0.14 255.255.255.255  
 ip ospf 1 area 0  
  
interface Ethernet0/0  
 description Link_to_R12  
 ip address 10.10.0.13 255.255.255.252  
 ip nat inside  
 ip virtual-reassembly in  
 ip ospf 1 area 10  
   
interface Ethernet0/1  
 description Link_to_R13  
 ip address 10.10.0.9 255.255.255.252  
 ip nat inside  
 ip virtual-reassembly in  
 ip ospf 1 area 10  
  
interface Ethernet0/2  
 description Link_to_R22  
 ip address 10.10.0.5 255.255.255.252  
 ip nat outside  
 ip virtual-reassembly in  
  
interface Ethernet0/3  
 description Link_to_R19  
 ip address 10.10.0.1 255.255.255.252  
 ip nat inside  
 ip virtual-reassembly in  
 ip ospf 1 area 101  
  
interface Ethernet1/0  
 description to_r15  
 ip address 10.10.0.93 255.255.255.252  
 ip ospf 1 area 0  
  
interface Ethernet1/1  
 no ip address  
 shutdown  
  
interface Ethernet1/2  
 no ip address  
 shutdown  
  
interface Ethernet1/3  
 no ip address  
 shutdown  
  
router ospf 1  
 router-id 14.14.14.14  
 area 101 stub no-summary  
 default-information originate always metric 100  
  
router bgp 1001  
 bgp router-id 14.14.14.14  
 bgp log-neighbor-changes  
 network 10.10.0.0 mask 255.255.255.252  
 network 10.10.0.4 mask 255.255.255.252  
 network 10.10.0.12 mask 255.255.255.252  
 network 10.20.0.14 mask 255.255.255.255  
 network 192.168.0.0  
 network 192.168.2.0  
 neighbor 10.10.0.6 remote-as 101  
  
ip nat inside source list NAT interface Ethernet0/2 overload  
ip route 0.0.0.0 0.0.0.0 10.10.0.6  
ip route 10.12.0.0 255.255.255.0 10.10.0.14 50  
ip route 10.12.0.0 255.255.255.0 10.10.0.10 100  
ip route 10.12.1.0 255.255.255.0 10.10.0.14 50  
ip route 10.12.1.0 255.255.255.0 10.10.0.10 100  
ip route 10.30.0.0 255.255.255.0 10.10.0.14 50  
ip route 10.30.0.0 255.255.255.0 10.10.0.10 100  
  
ip access-list standard NAT  
 permit 10.10.0.10  
 permit 10.10.0.14  
 permit 10.12.0.0 0.0.0.255  
 permit 10.12.1.0 0.0.0.255  

## hostname R15

interface Loopback0  
 ip address 10.20.0.15 255.255.255.255  
 ip ospf 1 area 0  
  
interface Ethernet0/0  
 description Link_to_R13  
 ip address 10.10.0.21 255.255.255.252  
 ip nat inside  
 ip virtual-reassembly in  
 ip ospf 1 area 10  
      
interface Ethernet0/1  
 description Link_to_R12  
 ip address 10.10.0.25 255.255.255.252  
 ip nat inside  
 ip virtual-reassembly in  
 ip ospf 1 area 10  
  
interface Ethernet0/2  
 description Link_to_R21  
 ip address 10.10.0.29 255.255.255.252  
 ip nat outside  
 ip virtual-reassembly in  
  
interface Ethernet0/3  
 description Link_to_R20  
 ip address 10.10.0.17 255.255.255.252  
 ip nat inside  
 ip virtual-reassembly in  
 ip ospf 1 area 102  
  
interface Ethernet1/0  
 description to_r14  
 ip address 10.10.0.94 255.255.255.252  
 ip ospf 1 area 0  
  
interface Ethernet1/1  
 no ip address  
 shutdown  
  
interface Ethernet1/2  
 no ip address  
 shutdown  
  
interface Ethernet1/3  
 no ip address  
 shutdown  
  
router ospf 1  
 router-id 15.15.15.15  
 area 102 filter-list prefix no_192.168.0.0 in  
 default-information originate always metric 200  
  
router bgp 1001  
 bgp router-id 15.15.15.15  
 bgp log-neighbor-changes  
 network 10.10.0.16 mask 255.255.255.252  
 network 10.10.0.20 mask 255.255.255.252  
 network 10.10.0.28 mask 255.255.255.252  
 network 10.20.0.15 mask 255.255.255.255  
 network 192.168.0.0  
 network 192.168.2.0  
 neighbor 10.10.0.30 remote-as 301  
  
no ip http server  
no ip http secure-server  
ip nat inside source list NAT interface Ethernet0/2 overload  
ip route 0.0.0.0 0.0.0.0 10.10.0.30  
ip route 10.12.0.0 255.255.255.0 10.10.0.26 50  
ip route 10.12.0.0 255.255.255.0 10.10.0.22 100  
ip route 10.12.1.0 255.255.255.0 10.10.0.26 50  
ip route 10.12.1.0 255.255.255.0 10.10.0.22 100  
ip route 10.30.0.0 255.255.255.0 10.10.0.26 50  
ip route 10.30.0.0 255.255.255.0 10.10.0.22 100  
  
ip access-list standard NAT  
 permit 10.10.0.22  
 permit 10.10.0.26  
 permit 10.12.0.0 0.0.0.255  
 permit 10.12.1.0 0.0.0.255  
  
ip prefix-list no_192.168.0.0 seq 5 deny 192.168.0.0/24  
ip prefix-list no_192.168.0.0 seq 10 permit 0.0.0.0/0 le 32  

[Ссылка обратно на задание](/labs/lab08/msk-kit-lam/README.md#) 