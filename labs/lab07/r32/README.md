### Общий план топологии:  
<img src='pic/top.jpg'>  
  
   Вначале ознакомимся с настройками интерфейсов. Настройка производилась по двум протоколам, ipv4 и ipv6. 

interface Loopback0  
 ip address 10.20.1.4 255.255.255.255  
 ipv6 address 4032::1/128  
 ipv6 enable  
  
interface Ethernet0/0  
 description Link_to_R16  
 ip address 10.10.0.78 255.255.255.252  
 ipv6 address FE80::2 link-local  
 ipv6 address autoconfig  
 ipv6 enable  

Переходим к настройке EIGRP named-mode. Lo0 сделан как passive-interface, так как туда нет смысла отправлять hello пакеты и искать соседей. Присвоим router-id.  Данный роутер будет stab connected, незачем его соседу искать чужие префиксы на наем.  

router eigrp EIGRP  
   
 address-family ipv4 unicast autonomous-system 1  
    
  af-interface Loopback0  
   passive-interface  
  exit-af-interface  
    
  topology base  
  exit-af-topology  
  network 10.10.0.78 0.0.0.0  
  network 10.20.1.4 0.0.0.0  
  eigrp router-id 32.32.32.32  
  eigrp stub connected  
 exit-address-family  
   
 address-family ipv6 unicast autonomous-system 1  
    
  topology base  
  exit-af-topology  
  eigrp router-id 32.32.32.32  
 exit-address-family  


[Ссылка обратно на лабораторную работу](/labs/lab07/README.md#)  