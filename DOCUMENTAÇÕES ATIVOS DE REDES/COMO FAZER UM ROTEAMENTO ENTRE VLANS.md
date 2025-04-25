
![[Pasted image 20250414155617.png]]

## ADICIONANDO IP AOS VPCS
## VPC1 

```
VPCS>ip 192.168.0.10 255.255.255.0 192.168.0.1 VLAN 2
```

## VPC2

```
VPCS>192.168.10.10 255.255.255.0 192.168.10.1 VLAN 3
```

## ADICIONANDO OS PCS NAS DEVIDAS VLAS E COLOCANDO A PORTA QUE ESTÁ LIGADA COM O ROTEADOR NO MODO TRUNK

# SW1

```
enable
configure terminal

interface e0/1
switchport mode access
switchport access vlan 2
exit

interface e0/0
switchport mode access
switchport access vlan 3
exit

interface E0/2
switchport mode trunk
switchport trunk encapsulation dot1q
exit

```

# ROUTER
#### Configurar o Roteador (Router-on-a-Stick)
```
enable
configure terminal

interface e0/0.2
encapsulation dot1Q 2
ip address 192.168.0.1 255.255.255.0 
exit

interface e0/0.3
encapsulation dot1Q 3
ip address 192.168.10.1 255.255.255.0 
exit

interface e0/0
no shutdown

```
