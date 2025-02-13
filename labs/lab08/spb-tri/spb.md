### hostname R18

ipv6 unicast-routing  
ipv6 cef  
  
interface Loopback0  
 ip address 10.20.1.1 255.255.255.255  
  
interface Ethernet0/0  
 description Link_to_R16  
 ip address 10.10.0.69 255.255.255.252  
 ipv6 address FE80::1 link-local  
 ipv6 address 3000::1/64  
 ipv6 enable  
  
interface Ethernet0/1  
 description Link_to_R17  
 ip address 10.10.0.73 255.255.255.252  
 ipv6 address FE80::1 link-local  
 ipv6 address 3001::1/64  
 ipv6 enable  
  
interface Ethernet0/2  
 description to_R24  
 ip address 10.10.0.62 255.255.255.252  
  
interface Ethernet0/3  
 description to_R26  
 ip address 10.10.0.66 255.255.255.252  
  
  
router eigrp EIGRP  
 !  
 address-family ipv4 unicast autonomous-system 1  
    
  af-interface Loopback0  
   passive-interface  
  exit-af-interface  
    
  topology base  
   redistribute static metric 1000000 1000 255 1 1500  
  exit-af-topology  
  network 10.10.0.69 0.0.0.0  
  network 10.10.0.73 0.0.0.0  
  network 10.20.1.1 0.0.0.0  
  eigrp router-id 18.18.18.18  
 exit-address-family  
   
 address-family ipv6 unicast autonomous-system 1  
    
  topology base  
  exit-af-topology  
  eigrp router-id 18.18.18.18  
 exit-address-family  
  
router bgp 2024  
 bgp router-id 18.18.18.18  
 bgp log-neighbor-changes  
 network 10.10.0.60 mask 255.255.255.252  
 network 10.10.0.64 mask 255.255.255.252  
 network 10.10.0.68 mask 255.255.255.252   
 network 10.10.0.72 mask 255.255.255.252  
 network 10.10.0.76 mask 255.255.255.252  
 network 10.30.1.0 mask 255.255.255.0  
 network 10.82.0.0 mask 255.255.255.0  
 network 10.82.1.0 mask 255.255.255.0  
 neighbor 10.10.0.61 remote-as 520  
 neighbor 10.10.0.65 remote-as 520  
  
ip route 0.0.0.0 0.0.0.0 10.10.0.61 50  
ip route 0.0.0.0 0.0.0.0 10.10.0.65 100  

[Ссылка обратно на задание](/labs/lab08/spb-tri/README.md#) 