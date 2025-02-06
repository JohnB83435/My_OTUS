### Общий план топологии:
<img src='pic/top.jpg'>  

Нужно отправить только маршрут (distribute) по умолчанию соседу R32, остальное все дропнется. Создадим префикс лист в котором разрешаем только передачу статического машрута от роутера R16:   

ip prefix-list SUMR seq 10 permit 0.0.0.0/0  
ipv6 prefix-list SUMR seq 10 permit ::/0  

Сделаем настройку Topology base. Нужно указать с какого интерфейса и в какую сторону будет работать правило, будет на out:  

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

 Перед этим создадим статический маршрут на роутере R17 и зарестрибутим его:  

ip route 0.0.0.0 0.0.0.0 Null0  
ipv6 route ::/0 Null0  

router eigrp EIGRP  
 
 address-family ipv4 unicast autonomous-system 1  
          
  af-interface Loopback0  
   passive-interface  
  exit-af-interface  
    
  af-interface Ethernet0/1  
   summary-address 10.0.0.0 255.0.0.0  
  exit-af-interface  
    
  topology base  
   redistribute static metric 10000 0 255 1 1500  
  exit-af-topology  
  network 10.10.0.74 0.0.0.0  
  network 10.20.1.2 0.0.0.0  
  network 10.30.1.0 0.0.0.255  
  network 10.82.0.0 0.0.0.255  
  network 10.82.1.0 0.0.0.255  
  eigrp router-id 17.17.17.17  
 exit-address-family  
   
 address-family ipv6 unicast autonomous-system 1  
    
  topology base  
   redistribute static  
  exit-af-topology  
  eigrp router-id 17.17.17.17  
 exit-address-family  

[Ссылка обратно на лабораторную работу](/labs/lab07/README.md#)