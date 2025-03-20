### Смотрим на IKEv2. Тут два наших пира r27 и r28

      R15#show crypto ikev2 sa          
       IPv4 Crypto IKEv2  SA 
      
      Tunnel-id Local                 Remote                fvrf/      ivrf            Status 
      1         10.10.0.29/500        10.10.0.82/500        none/      none            READY  
            Encr: AES-CBC, keysize: 128, Hash: MD596, DH Grp:2, Auth       sign: RSA, Auth verify: RSA
            Life/Active Time: 86400/11983 sec
      
      Tunnel-id Local                 Remote                fvrf/      ivrf            Status 
      3         10.10.0.29/500        12.10.0.2/500         none/      none            READY  
            Encr: AES-CBC, keysize: 128, Hash: MD596, DH Grp:2, Auth       sign: RSA, Auth verify: RSA
            Life/Active Time: 86400/10 sec
      
      Tunnel-id Local                 Remote                fvrf/      ivrf            Status 
      2         10.10.0.29/500        10.10.0.89/500        none/      none            READY  
            Encr: AES-CBC, keysize: 128, Hash: MD596, DH Grp:2, Auth       sign: RSA, Auth verify: RSA
            Life/Active Time: 86400/11572 sec
      
       IPv6 Crypto IKEv2  SA 

### Смотрим на IPsec. Тут два наших пира r27 и r28   

R15#show crypto ipsec sa identity 

    interface: Tunnel200
        Crypto map tag: Tunnel200-head-0, local addr 10.10.0.29
    
       protected vrf: (none)
       local  ident (addr/mask/prot/port): (0.0.0.0/0.0.0.0/0/0)
       remote ident (addr/mask/prot/port): (0.0.0.0/0.0.0.0/0/0)
       current_peer (none) port 500
         DENY, flags={ident_is_root,}
        #pkts encaps: 0, #pkts encrypt: 0, #pkts digest: 0
        #pkts decaps: 0, #pkts decrypt: 0, #pkts verify: 0
        #pkts compressed: 0, #pkts decompressed: 0
        #pkts not compressed: 0, #pkts compr. failed: 0
        #pkts not decompressed: 0, #pkts decompress failed: 0
        #send errors 0, #recv errors 0
    
       protected vrf: (none)
       local  ident (addr/mask/prot/port): (10.10.0.29/255.255.255.    255/47/0)
       remote ident (addr/mask/prot/port): (10.10.0.89/255.255.255.    255/47/0)
       current_peer 10.10.0.89 port 500
         PERMIT, flags={origin_is_acl,}
        #pkts encaps: 93, #pkts encrypt: 93, #pkts digest: 93
        #pkts decaps: 99, #pkts decrypt: 99, #pkts verify: 99
        #pkts compressed: 0, #pkts decompressed: 0
        #pkts not compressed: 0, #pkts compr. failed: 0
        #pkts not decompressed: 0, #pkts decompress failed: 0
        #send errors 0, #recv errors 0
    
       protected vrf: (none)
       local  ident (addr/mask/prot/port): (10.10.0.29/255.255.255.    255/47/0)
       remote ident (addr/mask/prot/port): (10.10.0.82/255.255.255.    255/47/0)
       current_peer 10.10.0.82 port 500
         PERMIT, flags={origin_is_acl,}
        #pkts encaps: 116, #pkts encrypt: 116, #pkts digest: 116
        #pkts decaps: 105, #pkts decrypt: 105, #pkts verify: 105
        #pkts compressed: 0, #pkts decompressed: 0
        #pkts not compressed: 0, #pkts compr. failed: 0
        #pkts not decompressed: 0, #pkts decompress failed: 0
        #send errors 0, #recv errors 0
    
    interface: Tunnel100
        Crypto map tag: Tunnel100-head-0, local addr 10.10.0.29
    
       protected vrf: (none)
       local  ident (addr/mask/prot/port): (0.0.0.0/0.0.0.0/0/0)
       remote ident (addr/mask/prot/port): (0.0.0.0/0.0.0.0/0/0)
       current_peer (none) port 500
         DENY, flags={ident_is_root,}
        #pkts encaps: 0, #pkts encrypt: 0, #pkts digest: 0
        #pkts decaps: 0, #pkts decrypt: 0, #pkts verify: 0
        #pkts compressed: 0, #pkts decompressed: 0
        #pkts not compressed: 0, #pkts compr. failed: 0
        #pkts not decompressed: 0, #pkts decompress failed: 0
        #send errors 0, #recv errors 0
    
       protected vrf: (none)
       local  ident (addr/mask/prot/port): (10.10.0.29/255.255.255.    255/47/0)
       remote ident (addr/mask/prot/port): (12.10.0.2/255.255.255.    255/47/0)
       current_peer 12.10.0.2 port 500
         PERMIT, flags={origin_is_acl,}
        #pkts encaps: 18, #pkts encrypt: 18, #pkts digest: 18
        #pkts decaps: 18, #pkts decrypt: 18, #pkts verify: 18
        #pkts compressed: 0, #pkts decompressed: 0
        #pkts not compressed: 0, #pkts compr. failed: 0
        #pkts not decompressed: 0, #pkts decompress failed: 0
        #send errors 0, #recv errors 0

[Ссылка обратно на лабораторную работу](/labs/lab13/README.md) 


### Spoke to spoke работает между r27 и r28


    R27#show dmvpn
    Legend: Attrb --> S - Static, D - Dynamic, I - Incomplete
            N - NATed, L - Local, X - No Socket
            # Ent --> Number of NHRP entries with same NBMA peer
            NHS Status: E --> Expecting Replies, R --> Responding, W     --> Waiting
            UpDn Time --> Up or Down Time for a Tunnel
    =================================================================    =========
    
    Interface: Tunnel100, IPv4 NHRP Details 
    Type:Spoke, NHRP Peers:2, 
    
     # Ent  Peer NBMA Addr Peer Tunnel Add State  UpDn Tm Attrb
     ----- --------------- --------------- ----- -------- -----
         1 10.10.0.29            103.0.0.1    UP 03:07:19     S
         1 10.10.0.89            103.0.0.2    UP 00:00:11     D

     7#ping 103.0.0.2
     ype escape sequence to abort.
     ending 5, 100-byte ICMP Echos to 103.0.0.2, timeout is 2      econds:
     !!!!
     uccess rate is 100 percent (5/5), round-trip min/avg/max = 6/6/      ms