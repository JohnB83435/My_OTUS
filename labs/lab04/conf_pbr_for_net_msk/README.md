По задумке VPC7/10.12.1.4 должен идти в интернет через PBR через провайдера «Ламас», в отличии от VPC1/10.12.0.4, который ходит в интернет через провайдер «Китрон» по умолчанию  

Перед этим, имитировал реальный интернет. В зоне провайдеров и настроил BGP:  

## R21  
<img src='pic/bgp_r21.PNG'>  

## R22  
<img src='pic/bgp_r22.PNG'>  

## R23  
<img src='pic/bgp_r23.PNG'>  

## R24  
<img src='pic/bgp_r24.PNG'>  

## R25  
<img src='pic/bgp_r25.PNG'>  

## R26
<img src='pic/bgp_r26.PNG'>  

## Настроен NAT на роутерах r14 и r15  

<img src='pic/nat_r14.PNG'>  

<img src='pic/nat_r15.PNG'>

Учитываем, что между роутерами r12 и r13 настроен HSRP и r12 является active:  

## R12  
<img src='pic/hsrp_r12.PNG'>  

## R13  
<img src='pic/hsrp_r13.PNG'>  

### show standby breef on R12
<img src='pic/hsrp_breef.PNG'>  

Настроена Route-map на R12 для VPC7/10.12.1.4 должен идти в интернет через провайдера «Ламас»  
  

<img src='pic/routemap_r12.PNG'>  

И сам ACL для него  
<img src='pic/acl_to_lamas.PNG'>  

### Наконец проверяем трассировкой хождение трафика от хостов VPC1 и VPC7  

Проверяем VPC1  
<img src='pic/vpc1_trace_10.10.0.65.PNG'>  

Проверяем VPC7  
<img src='pic/vpc7_trace_10.10.0.65.PNG'>  













