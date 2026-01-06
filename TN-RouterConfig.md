! ============================================
! TechNova Solutions - Router Configuratie
! Cisco 4321 Router (TN-Router)
! ============================================

enable
configure terminal

! Hostname
hostname TN-Router

! Wachtwoord beveiliging
enable secret secret

line console 0
password secret
login
exit

line vty 0 4
password secret
login
exit

! Hoofdinterface activeren
interface GigabitEthernet0/0/0
no shutdown
exit

! Subinterface VLAN 10 - Ontwikkelaars
interface GigabitEthernet0/0/0.10
encapsulation dot1Q 10
ip address 192.168.1.1 255.255.255.224
exit

! Subinterface VLAN 20 - Administratie/HR
interface GigabitEthernet0/0/0.20
encapsulation dot1Q 20
ip address 192.168.1.33 255.255.255.224
exit

! Subinterface VLAN 30 - Gasten
interface GigabitEthernet0/0/0.30
encapsulation dot1Q 30
ip address 192.168.1.65 255.255.255.224
exit

end

! extra
enable
configure terminal

ip access-list extended GUEST-RESTRICT
deny ip 192.168.1.64 0.0.0.31 192.168.1.0 0.0.0.31
deny ip 192.168.1.64 0.0.0.31 192.168.1.32 0.0.0.31
permit ip any any
exit

interface GigabitEthernet0/0/0.30
ip access-group GUEST-RESTRICT in
exit

end
