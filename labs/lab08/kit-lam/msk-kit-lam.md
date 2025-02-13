### hostname R22 

interface Loopback0  
 ip address 10.20.4.6 255.255.255.255  
  
interface Ethernet0/0  
 description to_r14  
 ip address 10.10.0.6 255.255.255.252  
  
interface Ethernet0/1  
 description to_r21  
 ip address 10.10.0.34 255.255.255.252  
  
interface Ethernet0/2  
 description to_r23  
 ip address 10.10.0.38 255.255.255.252  
  
interface Ethernet0/3  
 no ip address  
 shutdown  
  
router bgp 101  
 bgp router-id 22.22.22.22  
 bgp log-neighbor-changes  
 network 10.10.0.4 mask 255.255.255.252  
 network 10.10.0.32 mask 255.255.255.252  
 network 10.20.4.6 mask 255.255.255.255  
 neighbor 10.10.0.5 remote-as 1001  
 neighbor 10.10.0.33 remote-as 301  

 [Ссылка обратно на задание](/labs/lab08/kit-lam/README.md#)  