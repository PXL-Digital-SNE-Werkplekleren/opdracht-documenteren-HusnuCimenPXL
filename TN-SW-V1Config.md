! ============================================
! TechNova Solutions - Switch Configuratie
! Cisco 2960 Switch (TN-SW-V1)
! ============================================

enable
configure terminal

! Hostname
hostname TN-SW-V1

! Wachtwoord beveiliging
enable secret secret

line console 0
password secret
login
exit

line vty 0 15
password secret
login
exit

! VLANs aanmaken
vlan 10
name ONTWIKKELAARS
exit

vlan 20
name ADMIN-HR
exit

vlan 30
name GASTEN
exit

! Trunk poort naar Router
interface GigabitEthernet0/1
switchport mode trunk
exit

! Trunk poort naar Switch V2
interface GigabitEthernet0/2
switchport mode trunk
exit

! Access poorten voor Ontwikkelaars (VLAN 10)
interface range FastEthernet0/1-12
switchport mode access
switchport access vlan 10
exit

end


! ============================================
! EINDE CONFIGURATIE
! ============================================