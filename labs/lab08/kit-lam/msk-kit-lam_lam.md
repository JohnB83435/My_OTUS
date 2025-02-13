### hostname R21

interface Loopback0  
 ip address 10.20.4.5 255.255.255.255  
  
interface Ethernet0/0  
 description to_r15  
 ip address 10.10.0.30 255.255.255.252  
  
interface Ethernet0/1  
 ip address 10.10.0.33 255.255.255.252  
     
interface Ethernet0/2  
 ip address 10.10.0.42 255.255.255.252  
  
interface Ethernet0/3  
 no ip address  
 shutdown  
  
router bgp 301  
 bgp router-id 21.21.21.21  
 bgp log-neighbor-changes  
 network 10.10.0.28 mask 255.255.255.252  
 network 10.10.0.32 mask 255.255.255.252  
 network 10.10.0.40 mask 255.255.255.252  
 network 10.20.4.5 mask 255.255.255.255  
 neighbor 10.10.0.29 remote-as 1001  
 neighbor 10.10.0.34 remote-as 101  
 neighbor 10.10.0.41 remote-as 520  



[Ссылка обратно на задание](/labs/lab08/kit-lam/README.md#) 