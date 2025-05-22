### O QUE É O NAT DINÂMICO?

O **NAT Dinâmico** permite que vários endereços IP privados sejam convertidos em IPs públicos de um **pool disponível**, de forma **não fixa**.  
➡️ O roteador escolhe qualquer IP livre do pool quando um dispositivo precisa acessar a internet.  
➡️ Quando a conexão encerra, o IP volta para o pool e pode ser usado por outro.


![[Pasted image 20250521142214.png]]


### PARA FAZER ESSA CONFIGURAÇÃO CRIE UM POOL DE DHCP PARA ENDEREÇAR TODOS OS HOSTS E ENDERECEI AS INTERFACES DO ROTEADOR


### CONFIGURANDO O POOL DE DHCP

```
R2(config)# ip dhcp pool REDE_TESTE #nome do pool

R2(dhcp-config)#network 192.168.10.0 255.255.255.0 #rede de endereço

R2(dhcp-config)#defaul-router 192.168.10.1 #gateway

R2(dhcp-config)#exit

R2(config)#show ip dhcp binding #para vereficar os ips atribuidos
```

### CONFIGURANDO O RANGE DE IPS PUBLICOS

```
R2(config)# ip nat pool NAT-POOL 209.165.200.2 209.165.200.8 netmask 255.255.255.0 #Criando o pool de ips publicos

R2(config)# access-list 1 permit 192.168.10.0 255.255.255.0 #criando acl pra permitir o ip na rede

R2(config)# ip nat inside source list 1 pool NAT-POOL #pra vincular a acl com o pool de ips publicos

R2(config)#interface e0/0 #interface privada do roteador
R2(config)# ip nat inside

R2(config)#interface e0/1 #interface publica do roteador
R2(config)#ip nat outside
```


