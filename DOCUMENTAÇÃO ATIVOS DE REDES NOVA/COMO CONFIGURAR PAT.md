
### O QUE É  PAT?

O **PAT (Port Address Translation)**, também conhecido como **NAT overload**, é uma forma de NAT que permite que **vários dispositivos da rede interna compartilhem um único endereço IP público**, diferenciando as conexões pelas **portas TCP ou UDP**.

![[Pasted image 20250521153812.png]]

### PARA FAZER ESSA CONFIGURAÇÃO CRIE UM POOL DE DHCP PARA ENDEREÇAR TODOS OS HOSTS E ENDERECEI AS INTERFACES DO ROTEADOR


### CONFIGURANDO O POOL DE DHCP

```
R2(config)# ip dhcp pool REDE_TESTE #nome do pool

R2(dhcp-config)#network 192.168.10.0 255.255.255.0 #rede de endereço

R2(dhcp-config)#defaul-router 192.168.10.1 #gateway

R2(dhcp-config)#exit

R2(config)#show ip dhcp binding #para vereficar os ips atribuidos
```

### CONFIGURANDO O PAT

```
R2(config)# ip nat inside source list 1 interface e0/1 overload #pra vincular a acl com a interface do ip publico

R2(config)# access-list 1 permit 192.168.10.0 0.0.0.255 #criando a acl

R2(config)# interface e0/0

R2(config-if)# ip nat inside

R2(config-if)# exit

R2(config)# interface e0/1

R2(config-if)# ip nat outside
```

