    Configurazione Nat 1 - 1:

        int g0/1
            - ip nat inside
        
        int g0/2
            - ip nat outside

        ip nat inside source static "ipdispositivo" "iprouter"


-----------------------------------------------------------------------


    Configurazione Nat 1 - 1 Port X:

            int g0/1
                - ip nat inside
            
            int g0/2
                - ip nat outside

            ip nat inside source static tcp "ipdispositivo" "porta" "iprouter" "porta"


-----------------------------------------------------------------------


    Configurazione Nat Standard:

            int g0/1
                - ip nat inside
            
            int g0/2
                - ip nat outside

            access-list 55 permit "id rete" 0.0.0.255 
            ip nat inside source list 55 interface "porta rete esterna --> gigabitEthernet 0/2" overload
            

-----------------------------------------------------------------------


    Configurazione Nat Pool:

            int g0/1
                - ip nat inside
            
            int g0/2
                - ip nat outside

            access-list 55 permit "id rete" 0.0.0.255
            ip nat pool "Pool Name" "serie di indirizzi --> 14.127.8.17 14.127.8.22" netmask 255.255.255.240
            ip nat inside source list 55 pool "Pool Name" overload