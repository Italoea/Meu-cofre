
## A DMVNP FUNCIONA COM A TOPOLOGIA HUB AND SPOKE DESSA FORMA:



```
             (Spoke 1)
                 |
                 |
    (Spoke 2) — [ Hub ] — (Spoke 3)
                 |
                 |
             (Spoke 4)

```




## PARA CONFIGURAR UM HUB NA DMVPN:
##### NESSE CONTEXTO USAREMOS A INTERFACE LOOPBACK
```
int lo0 ip address 2.2.2.2 255.255.255.0
no sh
ex

int tunnel0
ip address 192.168.0.20 255.255.255.0
ip nhrp map multicast dynamic
ip nhrp authentication cisco
ip nhrp network-id 1
tunnel source lo0
tunnel mode gre multipoint
```
# NO HUB SÓ PRECISA FAZER ESSSA CONFIGURAÇÃO UMA UNICA VEZ, JÁ NOS SPOKES O COMANDO É O MESMO SÓ MUDA O IP  DA INTERFACE VPN E O DA LOOPBACK.


## PARA CONFIGURAR UM SPOKE USE OS COMANDOS:

##### NESSE CONTEXTO USAREMOS A INTERFACE LOOPBACK
```
int lo0
ip address 1.1.1.1 255.255.255.255
ex

interface tunnel 0
ip address 192.168.0.10 255.255.255.0 <-- IP DA VPN
ip nhrp nhs 192.168.0.100
ip nhrp network-id 1 <-- TODOS TEM QUE TER ESSE NUMERO
ip nhrp map 192.168.0.100 <-- IP DA INT VPN DO HUB 3.3.3.3 IP DA LO
ip nhrp map multicast 192.168.0.100 <-- IP DO HUB
ip nhrp authentication cisco <-- SENHA
tunnel source loopback0
tunnel mode gre multipoint 
no sh
```

#### LEMBRANDO QUE PARA FUNCIONAR TODOS DEVEM TER ROTAS, ENTÃO SEMPRE ANTES DE CONFIGURAR A DMVPN CONFIGURE UM PROTOCÓLO DE ROTEAMENTO DINÂMICO PARA QUE TODOS TENHAM ROTA UM PRO OUTRO.
