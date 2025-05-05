## 1	Организовать сети провайдеров.   

### На стенде имеется два провайдера (ROSTELECOM и MTC), а также точка обмена трафиком данными между ними, маршрутизация по протоколу BGP. В точке обмена внутренняя динамическая маршрутизация по протоколу IS-IS.   

#### 1.1	ROSTELECOM
   Провайдер находится в AS 90, при нем два роутера связанных между собой, каждый из них подключен к точке обмена трафиком. Со стороны каждого роутера выделяются порты для подключения роутеров предприятия согласно иллюстрации №1.   

#### 1.1.1	Выгрузка конфигурации R1_RTK   

     R1_RTK#show run
     Building configuration...
     
     Current configuration : 1697 bytes
     !
     version 15.2
     service timestamps debug datetime msec
     service timestamps log datetime msec
     no service password-encryption
     !
     hostname R1_RTK
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
     no ip domain lookup
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
      ip address 10.87.255.1 255.255.255.255
      ip ospf 1 area 0
     !
     interface Ethernet0/0
      description TO_H1_C1_MSK
      ip address 87.10.11.1 255.255.255.248
     !
     interface Ethernet0/1
      description TO_R1_MSK_XI
      ip address 87.87.10.1 255.255.255.252
     !
     interface Ethernet0/2
      description TO_R2_RTK
      ip address 87.10.10.1 255.255.255.252
      ip ospf 1 area 0
     !
     interface Ethernet0/3
      no ip address
      shutdown
     !
     router ospf 1
      router-id 10.87.255.1
      passive-interface Loopback0
     !
     router bgp 90
      bgp router-id 5.5.5.5
      bgp log-neighbor-changes
      network 10.87.255.1 mask 255.255.255.255
      network 87.10.11.0 mask 255.255.255.248
      neighbor 10.87.255.2 remote-as 90
      neighbor 10.87.255.2 update-source Loopback0
      neighbor 10.87.255.2 next-hop-self
      neighbor 10.87.255.2 soft-reconfiguration inbound
      neighbor 10.91.255.1 remote-as 100
      neighbor 10.91.255.1 ebgp-multihop 2
      neighbor 10.91.255.1 update-source Loopback0
      neighbor 10.91.255.1 next-hop-self
      neighbor 10.91.255.1 soft-reconfiguration inbound
     !
     ip forward-protocol nd
     !
     !
     no ip http server
     no ip http secure-server
     ip route 10.91.255.1 255.255.255.255 87.87.10.2
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
      exec-timeout 0 0
      logging synchronous
     line aux 0
     line vty 0 4
      login
      transport input all
     !
     !
     End


     
#### 1.1.2 Выгрузка конфигурации R2_RTK   

       R2_RTK#show run
    Building configuration...
    
    Current configuration : 1998 bytes
    !
    version 15.2
    service timestamps debug datetime msec
    service timestamps log datetime msec
    no service password-encryption
    !
    hostname R2_RTK
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
    no ip domain lookup
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
     ip address 10.87.255.2 255.255.255.255
     ip ospf 1 area 0
    !
    interface Ethernet0/0
     description TO_R3_MSK-XI
     ip address 87.87.11.1 255.255.255.252
    !
    interface Ethernet0/1
     description TO_R1_RTK
     ip address 87.10.10.2 255.255.255.252
     ip ospf 1 area 0
    !
    interface Ethernet0/2
     description TO_R1_SPB
     ip address 87.10.12.1 255.255.255.252
    !
    interface Ethernet0/3
     description TO_R1_TMB
     ip address 87.10.13.1 255.255.255.252
    !
    interface Ethernet1/0
     description TO_R1_MRN
     ip address 87.10.14.1 255.255.255.252
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
    router ospf 1
     router-id 10.87.255.2
     passive-interface Loopback0
    !
    router bgp 90
     bgp router-id 6.6.6.6
     bgp log-neighbor-changes
     network 10.87.255.2 mask 255.255.255.255
     network 87.10.12.0 mask 255.255.255.252
     network 87.10.13.0 mask 255.255.255.252
     network 87.10.14.0 mask 255.255.255.252
     neighbor 10.87.255.1 remote-as 90
     neighbor 10.87.255.1 update-source Loopback0
     neighbor 10.87.255.1 next-hop-self
     neighbor 10.87.255.1 soft-reconfiguration inbound
     neighbor 10.91.255.3 remote-as 100
     neighbor 10.91.255.3 ebgp-multihop 2
     neighbor 10.91.255.3 update-source Loopback0
     neighbor 10.91.255.3 next-hop-self
     neighbor 10.91.255.3 soft-reconfiguration inbound
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
     exec-timeout 0 0
     logging synchronous
    line aux 0
    line vty 0 4
     login
     transport input all
    !
    !
    End    

 #### 1.2	МТС   

 Провайдер находится в AS 110, при нем два роутера связанных между собой, каждый из них подключен к точке обмена трафиком. Со стороны каждого роутера выделяются порты для подключения роутеров предприятия согласно иллюстрации №1.   

 #### 1.2.1 Выгрузка конфигурации R1_MTS   

     R1_MTS#show run
    Building configuration...
    
    Current configuration : 1705 bytes
    !
    version 15.2
    service timestamps debug datetime msec
    service timestamps log datetime msec
    no service password-encryption
    !
    hostname R1_MTS
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
    no ip domain lookup
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
     ip address 10.76.255.1 255.255.255.255
     ip ospf 1 area 0
    !
    interface Ethernet0/0
     description TO_HUB1_CLOUD2_MSK
     ip address 76.10.11.1 255.255.255.248
    !
    interface Ethernet0/1
     description TO_R2_MSK-XI
     ip address 76.76.10.2 255.255.255.252
    !
    interface Ethernet0/2
     description TO_R2_MTS
     ip address 76.10.10.1 255.255.255.252
     ip ospf 1 area 0
    !
    interface Ethernet0/3
     no ip address
     shutdown
    !
    router ospf 1
     router-id 10.76.255.1
     passive-interface Loopback0
    !
    router bgp 110
     bgp router-id 7.7.7.7
     bgp log-neighbor-changes
     network 10.76.255.1 mask 255.255.255.255
     network 76.10.11.0 mask 255.255.255.248
     neighbor 10.76.255.2 remote-as 110
     neighbor 10.76.255.2 update-source Loopback0
     neighbor 10.76.255.2 next-hop-self
     neighbor 10.76.255.2 soft-reconfiguration inbound
     neighbor 10.91.255.2 remote-as 100
     neighbor 10.91.255.2 ebgp-multihop 2
     neighbor 10.91.255.2 update-source Loopback0
     neighbor 10.91.255.2 next-hop-self
     neighbor 10.91.255.2 soft-reconfiguration inbound
    !
    ip forward-protocol nd
    !
    !
    no ip http server
    no ip http secure-server
    ip route 10.91.255.2 255.255.255.255 76.76.10.1
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
     exec-timeout 0 0
     logging synchronous
    line aux 0
    line vty 0 4
     login
     transport input all
    !
    !
    End
    1.1.1	Выгрузка конфигурации R2_MTS
       R2_MTS#show run
    Building configuration...
    
    Current configuration : 2036 bytes
    !
    version 15.2
    service timestamps debug datetime msec
    service timestamps log datetime msec
    no service password-encryption
    !
    hostname R2_MTS
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
    no ip domain lookup
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
     ip address 10.76.255.2 255.255.255.255
     ip ospf 1 area 0
    !
    interface Ethernet0/0
     description R4_MSK-XI
     ip address 76.76.11.2 255.255.255.252
    !
    interface Ethernet0/1
     description R2_SPB
     ip address 76.10.12.1 255.255.255.252
    !
    interface Ethernet0/2
     description R2_TMB
     ip address 76.10.13.1 255.255.255.252
    !
    interface Ethernet0/3
     description R2_MRN
     ip address 76.10.14.1 255.255.255.252
    !
    interface Ethernet1/0
     description TO_R1_MTS
     ip address 76.10.10.2 255.255.255.252
     ip ospf 1 area 0
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
    router ospf 1
     router-id 10.76.255.2
     passive-interface Loopback0
    !
    router bgp 110
     bgp router-id 8.8.8.8
     bgp log-neighbor-changes
     network 10.76.255.2 mask 255.255.255.255
     network 76.10.12.0 mask 255.255.255.252
     network 76.10.13.0 mask 255.255.255.252
     network 76.10.14.0 mask 255.255.255.252
     neighbor 10.76.255.1 remote-as 110
     neighbor 10.76.255.1 update-source Loopback0
     neighbor 10.76.255.1 next-hop-self
     neighbor 10.76.255.1 soft-reconfiguration inbound
     neighbor 10.91.255.4 remote-as 100
     neighbor 10.91.255.4 ebgp-multihop 2
     neighbor 10.91.255.4 update-source Loopback0
     neighbor 10.91.255.4 next-hop-self
     neighbor 10.91.255.4 soft-reconfiguration inbound
    !
    ip forward-protocol nd
    !
    !
    no ip http server
    no ip http secure-server
    ip route 10.91.255.4 255.255.255.255 76.76.11.1
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
     exec-timeout 0 0
     logging synchronous
    line aux 0
    line vty 0 4
     login
     transport input all
    !
    !
    end

 #### 1.2.2 Выгрузка конфигурации R1_MTS   

     R2_MTS#show run
    Building configuration...
    
    Current configuration : 2036 bytes
    !
    version 15.2
    service timestamps debug datetime msec
    service timestamps log datetime msec
    no service password-encryption
    !
    hostname R2_MTS
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
    no ip domain lookup
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
     ip address 10.76.255.2 255.255.255.255
     ip ospf 1 area 0
    !
    interface Ethernet0/0
     description R4_MSK-XI
     ip address 76.76.11.2 255.255.255.252
    !
    interface Ethernet0/1
     description R2_SPB
     ip address 76.10.12.1 255.255.255.252
    !
    interface Ethernet0/2
     description R2_TMB
     ip address 76.10.13.1 255.255.255.252
    !
    interface Ethernet0/3
     description R2_MRN
     ip address 76.10.14.1 255.255.255.252
    !
    interface Ethernet1/0
     description TO_R1_MTS
     ip address 76.10.10.2 255.255.255.252
     ip ospf 1 area 0
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
    router ospf 1
     router-id 10.76.255.2
     passive-interface Loopback0
    !
    router bgp 110
     bgp router-id 8.8.8.8
     bgp log-neighbor-changes
     network 10.76.255.2 mask 255.255.255.255
     network 76.10.12.0 mask 255.255.255.252
     network 76.10.13.0 mask 255.255.255.252
     network 76.10.14.0 mask 255.255.255.252
     neighbor 10.76.255.1 remote-as 110
     neighbor 10.76.255.1 update-source Loopback0
     neighbor 10.76.255.1 next-hop-self
     neighbor 10.76.255.1 soft-reconfiguration inbound
     neighbor 10.91.255.4 remote-as 100
     neighbor 10.91.255.4 ebgp-multihop 2
     neighbor 10.91.255.4 update-source Loopback0
     neighbor 10.91.255.4 next-hop-self
     neighbor 10.91.255.4 soft-reconfiguration inbound
    !
    ip forward-protocol nd
    !
    !
    no ip http server
    no ip http secure-server
    ip route 10.91.255.4 255.255.255.255 76.76.11.1
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
     exec-timeout 0 0
     logging synchronous
    line aux 0
    line vty 0 4
     login
     transport input all
    !
    !
    end


    
### 1.3	Точка обмена   

   Находится в AS 100, при ней четыре роутера связанных между собой одним линком с каждым соседним. Каждый роутер подключается одним линком к провайдеру согласно иллюстрации №1. Route reflector R4_MSK-XI.   

#### 1.3.1 Выгрузка конфигурации R1_MSK-XI   

     R1_MSK-XI#show run
     Building configuration...
     
     Current configuration : 1756 bytes
     !
     version 15.2
     service timestamps debug datetime msec
     service timestamps log datetime msec
     no service password-encryption
     !
     hostname R1_MSK-XI
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
     no ip domain lookup
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
      ip address 10.91.255.1 255.255.255.255
     !
     interface Ethernet0/0
      description TO_R1_RTK
      ip address 87.87.10.2 255.255.255.252
     !
     interface Ethernet0/1
      description TO_R2_MSK-XI
      ip address 91.10.10.1 255.255.255.252
      ip router isis 49.1000
     !
     interface Ethernet0/2
      description TO_R3_MSK-XI
      ip address 91.10.10.5 255.255.255.252
      ip router isis 49.1000
     !
     interface Ethernet0/3
      no ip address
      shutdown
     !
     router isis 49.1000
      net 49.1000.0100.9125.5001.00
      is-type level-2-only
      passive-interface Loopback0
     !
     router bgp 100
      bgp router-id 1.1.1.1
      bgp log-neighbor-changes
      network 10.91.255.1 mask 255.255.255.255
      neighbor FORALL peer-group
      neighbor FORALL remote-as 100
      neighbor FORALL update-source Loopback0
      neighbor FORALL next-hop-self
      neighbor FORALL soft-reconfiguration inbound
      neighbor 10.87.255.1 remote-as 90
      neighbor 10.87.255.1 ebgp-multihop 2
      neighbor 10.87.255.1 update-source Loopback0
      neighbor 10.87.255.1 next-hop-self
      neighbor 10.87.255.1 soft-reconfiguration inbound
      neighbor 10.91.255.4 peer-group FORALL
     !
     ip forward-protocol nd
     !
     !
     no ip http server
     no ip http secure-server
     ip route 10.87.255.1 255.255.255.255 87.87.10.1
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
      exec-timeout 0 0
      logging synchronous
     line aux 0
     line vty 0 4
      login
      transport input all
     !
     !
     End

#### 1.3.2 Выгрузка конфигурации R2_MSK-XI   

    R2_MSK-XI#show run
    Building configuration...
    
    Current configuration : 1757 bytes
    !
    version 15.2
    service timestamps debug datetime msec
    service timestamps log datetime msec
    no service password-encryption
    !
    hostname R2_MSK-XI
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
    no ip domain lookup
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
     ip address 10.91.255.2 255.255.255.255
    !
    interface Ethernet0/0
     description TO_R1_MSK-XI
     ip address 91.10.10.2 255.255.255.252
     ip router isis 49.1000
    !
    interface Ethernet0/1
     description TO_R4_MSK-XI
     ip address 91.10.10.9 255.255.255.252
     ip router isis 49.1000
    !
    interface Ethernet0/2
     description TO_R1_MTS
     ip address 76.76.10.1 255.255.255.252
    !
    interface Ethernet0/3
     no ip address
     shutdown
    !
    router isis 49.1000
     net 49.1000.0100.9125.5002.00
     is-type level-2-only
     passive-interface Loopback0
    !
    router bgp 100
     bgp router-id 2.2.2.2
     bgp log-neighbor-changes
     network 10.91.255.2 mask 255.255.255.255
     neighbor FORALL peer-group
     neighbor FORALL remote-as 100
     neighbor FORALL update-source Loopback0
     neighbor FORALL next-hop-self
     neighbor FORALL soft-reconfiguration inbound
     neighbor 10.76.255.1 remote-as 110
     neighbor 10.76.255.1 ebgp-multihop 2
     neighbor 10.76.255.1 update-source Loopback0
     neighbor 10.76.255.1 next-hop-self
     neighbor 10.76.255.1 soft-reconfiguration inbound
     neighbor 10.91.255.4 peer-group FORALL
    !
    ip forward-protocol nd
    !
    !
    no ip http server
    no ip http secure-server
    ip route 10.76.255.1 255.255.255.255 76.76.10.2
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
     exec-timeout 0 0
     logging synchronous
    line aux 0
    line vty 0 4
     login
     transport input all
    !
    !
    End   

#### 1.3.3 Выгрузка конфигурации R3_MSK-XI   

    R3_MSK-XI#show run
    Building configuration...
    
    Current configuration : 1503 bytes
    !
    version 15.2
    service timestamps debug datetime msec
    service timestamps log datetime msec
    no service password-encryption
    !
    hostname R3_MSK-XI
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
    no ip domain lookup
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
     ip address 10.91.255.3 255.255.255.255
    !
    interface Ethernet0/0
     description TO_R2_RTK
     ip address 87.87.11.2 255.255.255.252
    !
    interface Ethernet0/1
     description TO_R4_MSK-XI
     ip address 91.10.10.13 255.255.255.252
     ip router isis 49.1000
    !
    interface Ethernet0/2
     description TO_R3_MSK-XI
     ip address 91.10.10.6 255.255.255.252
     ip router isis 49.1000
    !
    interface Ethernet0/3
     no ip address
     shutdown
    !
    router isis 49.1000
     net 49.1000.0100.9125.5003.00
     is-type level-2-only
     passive-interface Loopback0
    !
    router bgp 100
     bgp router-id 3.3.3.3
     bgp log-neighbor-changes
     network 10.91.255.3 mask 255.255.255.255
     neighbor FORALL peer-group
     neighbor FORALL remote-as 100
     neighbor FORALL update-source Loopback0
     neighbor FORALL next-hop-self
     neighbor FORALL soft-reconfiguration inbound
     neighbor 10.91.255.4 peer-group FORALL
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
     exec-timeout 0 0
     logging synchronous
    line aux 0
    line vty 0 4
     login
     transport input all
    !
    !
    End   

#### 1.3.4 Выгрузка конфигурации R4_MSK-XI  

    R4_MSK-XI#show run
    Building configuration...
    
    Current configuration : 1893 bytes
    !
    version 15.2
    service timestamps debug datetime msec
    service timestamps log datetime msec
    no service password-encryption
    !
    hostname R4_MSK-XI
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
    no ip domain lookup
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
     ip address 10.91.255.4 255.255.255.255
    !
    interface Ethernet0/0
     description TO_R3_MSK-XI
     ip address 91.10.10.14 255.255.255.252
     ip router isis 49.1000
    !
    interface Ethernet0/1
     description TO_R2_MSK-XI
     ip address 91.10.10.10 255.255.255.252
     ip router isis 49.1000
    !
    interface Ethernet0/2
     description TO_R2_MTS
     ip address 76.76.11.1 255.255.255.252
    !
    interface Ethernet0/3
     no ip address
     shutdown
    !
    router isis 49.1000
     net 49.1000.0100.9125.5004.00
     is-type level-2-only
     passive-interface Loopback0
    !
    router isis
    !
    router bgp 100
     bgp router-id 4.4.4.4
     bgp log-neighbor-changes
     network 10.91.255.4 mask 255.255.255.255
     neighbor FORALL peer-group
     neighbor FORALL remote-as 100
     neighbor FORALL update-source Loopback0
     neighbor FORALL route-reflector-client
     neighbor FORALL next-hop-self
     neighbor FORALL soft-reconfiguration inbound
     neighbor 10.76.255.2 remote-as 110
     neighbor 10.76.255.2 ebgp-multihop 2
     neighbor 10.76.255.2 update-source Loopback0
     neighbor 10.76.255.2 next-hop-self
     neighbor 10.76.255.2 soft-reconfiguration inbound
     neighbor 10.91.255.1 peer-group FORALL
     neighbor 10.91.255.2 peer-group FORALL
     neighbor 10.91.255.3 peer-group FORALL
    !
    ip forward-protocol nd
    !
    !
    no ip http server
    no ip http secure-server
    ip route 10.76.255.2 255.255.255.255 76.76.11.2
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
     exec-timeout 0 0
     logging synchronous
    line aux 0
    line vty 0 4
     login
     transport input all
    !
    !
    End   

[Ссылка обратно на лабораторную работу](/labs/lab14/front.md)









