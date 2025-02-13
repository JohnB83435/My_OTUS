### hostname R23  
  
ipv6 unicast-routing  
ipv6 cef  
  
interface Loopback0  
 ip address 10.20.4.1 255.255.255.255  
  
interface Ethernet0/0  
 description to_r22  
 ip address 10.10.0.37 255.255.255.252  
  
interface Ethernet0/1  
 description Link_to_R25  
 ip address 10.10.0.49 255.255.255.252  
 ip router isis 49.2222  
 ipv6 address 2001::1/64  
 ipv6 enable  
  
interface Ethernet0/2  
 description Link_to_R24  
 ip address 10.10.0.45 255.255.255.252  
 ip router isis 49.2222  
 ipv6 address 2002::1/64  
 ipv6 enable  
  
interface Ethernet0/3  
 no ip address  
 shutdown  
  
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
  
router isis 49.2222  
 net 49.2222.0100.2000.4001.00  
 passive-interface Loopback0  
  
router isis  
  
router bgp 520  
 bgp router-id 23.23.23.23  
 bgp log-neighbor-changes  
 network 10.10.0.44 mask 255.255.255.252  
 network 10.10.0.48 mask 255.255.255.252  
 network 10.20.4.1 mask 255.255.255.255  
 neighbor 10.10.0.46 remote-as 520  
 neighbor 10.10.0.50 remote-as 520  
  
## hostname R24  
  
ipv6 unicast-routing  
ipv6 cef  
  
interface Loopback0  
 ip address 10.20.4.3 255.255.255.255  
  
interface Ethernet0/0  
 description Link_to_R21  
 ip address 10.10.0.41 255.255.255.252  
  
interface Ethernet0/1  
 description Link_to_R26  
 ip address 10.10.0.53 255.255.255.252  
 ip router isis 49.0024  
 ipv6 address 2003::1/64  
 ipv6 enable  
  
interface Ethernet0/2  
 description Link_to_R23  
 ip address 10.10.0.46 255.255.255.252  
 ip router isis 49.0024  
 ipv6 address 2002::2/64  
 ipv6 enable  
  
interface Ethernet0/3  
 description Link_to_R18  
 ip address 10.10.0.61 255.255.255.252  
  
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
  
router isis 49.0024  
 net 49.0024.0100.2000.4003.00  
 passive-interface Loopback0  
  
router bgp 520  
 bgp router-id 24.24.24.24  
 bgp log-neighbor-changes  
 network 10.10.0.40 mask 255.255.255.252  
 network 10.10.0.44 mask 255.255.255.252  
 network 10.10.0.52 mask 255.255.255.252  
 network 10.10.0.60 mask 255.255.255.252  
 network 10.20.4.3 mask 255.255.255.255  
 neighbor 10.10.0.42 remote-as 301  
 neighbor 10.10.0.45 remote-as 520  
 neighbor 10.10.0.54 remote-as 520  
 neighbor 10.10.0.62 remote-as 2024  
  
## hostname R25  
  
ipv6 unicast-routing  
ipv6 cef  
  
interface Loopback0  
 ip address 10.20.4.2 255.255.255.255  
  
interface Ethernet0/0  
 description Link_to_R23  
 ip address 10.10.0.50 255.255.255.252  
 ip router isis 49.2222  
 ipv6 address 2001::2/64  
 ipv6 enable  
         
interface Ethernet0/1  
 description Link_to_R27  
 ip address 10.10.0.81 255.255.255.252  
  
interface Ethernet0/2  
 description Link_to_R26  
 ip address 10.10.0.57 255.255.255.252  
 ip router isis 49.2222  
 ipv6 address 2004::2/64  
 ipv6 enable  
  
interface Ethernet0/3  
 description Link_to_R28  
 ip address 10.10.0.85 255.255.255.252  
  
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
  
router isis 49.2222  
 net 49.2222.0100.2000.4002.00  
 passive-interface Loopback0  
  
router bgp 520  
 bgp router-id 25.25.25.25  
 bgp log-neighbor-changes  
 network 10.10.0.48 mask 255.255.255.252  
 network 10.10.0.56 mask 255.255.255.252  
 network 10.20.4.2 mask 255.255.255.255  
 neighbor 10.10.0.49 remote-as 520  
 neighbor 10.10.0.58 remote-as 520  
  
## hostname R26  
  
ipv6 unicast-routing  
ipv6 cef  
  
interface Loopback0  
 ip address 10.20.4.4 255.255.255.255  
  
interface Ethernet0/0  
 description Link_to_R24  
 ip address 10.10.0.54 255.255.255.252  
 ip router isis 49.0026  
 ipv6 address 2003::2/64  
 ipv6 enable  
          
interface Ethernet0/1  
 description Link_to_R28  
 ip address 10.10.0.90 255.255.255.252  
  
interface Ethernet0/2  
 description Link_to_R25  
 ip address 10.10.0.58 255.255.255.252  
 ip router isis 49.0026  
 ipv6 address 2004::1/64  
 ipv6 enable  
  
interface Ethernet0/3  
 description Link_to_R18  
 ip address 10.10.0.65 255.255.255.252  
  
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
  
router isis 49.0026  
 net 49.0026.0100.2000.4004.00  
 passive-interface Loopback0  
  
router bgp 520  
 bgp router-id 26.26.26.26  
 bgp log-neighbor-changes  
 network 10.10.0.52 mask 255.255.255.252  
 network 10.10.0.56 mask 255.255.255.252  
 network 10.10.0.64 mask 255.255.255.252  
 network 10.20.4.4 mask 255.255.255.255  
 neighbor 10.10.0.53 remote-as 520  
 neighbor 10.10.0.57 remote-as 520  
 neighbor 10.10.0.66 remote-as 2024  

[Ссылка обратно на задание](/labs/lab08/spb-tri/README.md#) 