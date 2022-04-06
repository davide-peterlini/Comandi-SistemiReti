    ACL:
        Configurazione di ACL standard numeriche:
            - access-list numero_ACL deny|permit ip_sorgente maschera_wildcard
            - access-list 1 permit 172.16.2.144 0.0.0.7


        Configurazione di ACL standard con nome:
            - ip access-list standard nome_ACL
            - [deny|permit] ip-sorgente

            Esempio:
                - ip access-list standard permit-ip
                - permit 172.16.2.144 0.0.0.7 


        Configurazione di ACL estese con nome:
            - ip access-list extended nome-ACL
            - deny|permit protocollo ip_sorgente wildcard_mask ip_destinazione wildcard_mask condizione applicazione

            Esempio:
                - ip access-list extended blocco-telnet
                - access-list 101 deny tcp 172.16.2.0 0.0.0.255 any eq telnet

        
        Assegnare un' ACL a un’interfaccia:
            - Router(config-line)#access-class ACL in|out

    
    ACL(IPv6):
        Creazione ACL:
        - ipv6 access-list nome_ACL
            -   perimit|deny ipv6 source destinazione
        

        Assegnazione Interfaccia:
            ipv6 trafic-filter nome_ACL in|out



-----------------------------------------------------------------------



    OSPF v2 (IPv4):
        - router ospf 10
        - rounter-id 1.1.1.1
        - network rete widecard area n_Area
        
        Esempio:
            - network 192.168.10.4 0.0.0.3 area 0


    OSPF v3 (IPv6):
        - Configurazione OSPF singola AREA 10
        - Configurazione di un singolo router con OSPFv3 per IPv6
            R1(config)#ipv6 unicast-routing
            R1(config)#interface range gigabitEthernet 0/0-2
            R1(config-if-range)#ipv6 address fe80::1 link-local
            R1(config-if-range)#exit
            R1(config)#ipv6 router ospf 100
            R1(config-rtr)#router-id 1.1.1.1

            Metto tutti i collegamenti nella stessa area 10

            //NON FUNZIONA il range… almeno in packet tracer
            //Bisogna configurare un’interfaccia singola alla volta
            R1(config)#interface range gigabitEthernet 0/0-2
            R1(config-if-range)#ipv6 ospf 100 area 10

            R1(config)#interface gigabitEthernet 0/0
            R1(config-if)#ipv6 ospf 100 area 10
            R1(config)#interface gigabitEthernet 0/1
            R1(config-if)#ipv6 ospf 100 area 10
            R1(config)#interface gigabitEthernet 0/2
            R1(config-if)#ipv6 ospf 100 area 10


-----------------------------------------------------------------------



    GRE:
        NB: fare su entrambi i rounter

        Rotte statiche:
            - ip rount 0.0.0.0 0.0.0.0 ip_RArrivo


        Tunner:
            - interface tunnel 0
            - ip address 10.1.3.1 255.255.255.252
            - tunnel mode gre ip
            - tunnel source porta_tunnel
            - tunnel destination ip_RDestinazione


        EIGRP:
            - rounter eigrp 100
            - network 10.0.0.0
            - no auto-summary