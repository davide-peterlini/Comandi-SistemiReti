    Configurazione switch base:

        Configurare nome SW:
            - ena
            - conf t
            - hostname A#-SW#

        Configurare Password:
            - line console 0
            - password cisco
            - login
            - end

        Criptaggio Password:
            - configure terminal
            - service password-encryption
            - end
            - show running-config

        Banner Messages:
            - conf t
            - banner motd 'Authorized Access Only'
            - end

        Configurazione IP:
            - configure terminal
            - interface vlan 1
            - ip address 172.16.1.254 255.255.255.0
            - no shutdown 
            - exit


-----------------------------------------------------------------------


    SSH:
        - service password-encryption
        - no ip domain-lookup
        - ip domain-name CCNA.com
        - username Davide secret cisco
        - crypto key generate rsa
        - line vty 0 15
        - transport input ssh
        - login local
        - exec-timeout 6

        //- login block-for 180 attempts 4 within 120


-----------------------------------------------------------------------


    Telnet:
        - conf t
        - line vty 0 15
        - transport input telnet
        - password cisco
        - login


-----------------------------------------------------------------------


    EtherChannel:
        - conf t
        - interface range f0/1 -4
        - channel-group 1 mode ?
            active     Enable LACP unconditionally
            auto       Enable PAgP only if a PAgP device is detected
            desirable  Enable PAgP unconditionally
            on         Enable Etherchannel only
            passive    Enable LACP only if a LACP device is detected
        - channel-group 1 mode active
        - show etherchannel summary


-----------------------------------------------------------------------


    VLAN:
        - vlan 10
        - name Gialla
        - exit
        - vlan 20
        - name Azzurra
        - exit
        - interface range fastEthernet 0/1 -12
        - switchport access vlan 10
        - interface range fastEthernet 0/13-24
        - switchport access vlan 20
        - exit
        - do sho vlan
        

-----------------------------------------------------------------------


    DHCP:
        - ip dhcp excluded-address 172.16.1.1 172.16.1.3
        - ip dhcp pool DATA
        - network 172.16.1.0 255.255.255.0
        - default-router 172.16.1.1
        - dns-server 172.16.1.1 172.16.1.21
        - lease day|infinite


-----------------------------------------------------------------------


    DHCP with SL3 & DHCP SERVER:
        
        Conf Interface Port:
            - interface GigabitEthernet1/1/1
            - switchport trunk encapsulation dot1q
            - switchport mode trunk
        
        Conf Interface Vlan:
            - interface vlan "nVlan"
            - ip address "ipvlan" 255.255.255.0
            - ip helper-address "ip dhcp server"
            - no shutdown

        Conf Gataway DHCP Server:
            - interface GigabitEthernet1/0/3
            - switchport access vlan "nVlan"
            - switchport mode access

            - interface vlan "nVlan"
            - ip address "dhcp server gataway" 255.255.255.0
            - no shutdown