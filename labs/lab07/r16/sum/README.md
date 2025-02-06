### Общий план топологии:
<img src='pic/top.jpg'>  

  Настроим суммирование маршрута. У нас под суммаризацию хорошо подпадают четыре сети - 10.82.0.0/24, 10.82.1.0/24, 10.10.0.68/30, 10.20.1.2/32 их и зассумируем по 10.0.0.0/8 в сторону R18

interface Loopback0  
 ip address 10.20.1.2 255.255.255.255  
 ipv6 address 4016::1/128  
 ipv6 enable  

interface Ethernet0/0.101  
 description PTO  
 encapsulation dot1Q 101  
 ip address 10.82.0.3 255.255.255.0  
 standby version 2  
 standby 0 ip 10.82.0.1  
 standby 0 priority 90  
 standby 1 ipv6 FE80::10  
 standby 1 priority 90  
 ipv6 address FE80::3 link-local  
 ipv6 address 3101::2/64  
 ipv6 enable  

interface Ethernet0/0.102  
 description FEO  
 encapsulation dot1Q 102  
 ip address 10.82.1.3 255.255.255.0  
 standby version 2  
 standby 0 ip 10.82.1.1  
 standby 0 priority 90  
 standby 1 ipv6 FE80::10  
 standby 1 priority 90  
 ipv6 address FE80::3 link-local  
 ipv6 address 3102::2/64  
 ipv6 enable  

interface Ethernet0/1  
 description Link_to_R18  
 ip address 10.10.0.70 255.255.255.252  
 ipv6 address FE80::2 link-local  
 ipv6 address autoconfig  
 ipv6 enable  
 interface Ethernet0/3  
 description Link_to_R32  
 ip address 10.10.0.77 255.255.255.252  
 ipv6 address FE80::1 link-local  
 ipv6 address 3016::1/64  
 ipv6 enable  

router eigrp EIGRP  
      
 address-family ipv4 unicast autonomous-system 1  
  
  af-interface Loopback0  
   passive-interface  
  exit-af-interface  
  
  af-interface Ethernet0/1  
   summary-address 10.0.0.0 255.0.0.0  
  exit-af-interface  
  
  topology base  
   distribute-list prefix SUMR out Ethernet0/3  
  exit-af-topology  
  network 10.10.0.70 0.0.0.0  
  network 10.10.0.77 0.0.0.0  
  network 10.20.1.2 0.0.0.0  
  network 10.82.0.0 0.0.0.255  
  network 10.82.1.0 0.0.0.255  
  eigrp router-id 16.16.16.16  
 exit-address-family  
 
 address-family ipv6 unicast autonomous-system 1  
         
  topology base  
   distribute-list prefix-list SUMR out Ethernet0/3  
  exit-af-topology  
  eigrp router-id 16.16.16.16  
 exit-address-family  




[Ссылка обратно на лабораторную работу](/labs/lab07/README.md#)