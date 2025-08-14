
### PARA INSTALAR O KEEPALIVED:

```
apt install keepalived
```


### VÁ PAR O DIRETÓRIO /etc/keepalived/ lá vai tem um arquivo com o nome keepalived.conf.sample dê um:

```
cat keeplived.conf.sample >> keepalived.conf
```

##### APÓS ISSO EXCLUA TODO O ARQUIVO QUE NÃO TEM SENTIDO E DEIXE SOMENTE:

```
global_defs {
    # vrrp_strict  <-- removido para evitar bloqueio de ICMP
}

vrrp_instance VI_1 {
    state MASTER  <-- O SERVER QUE VAI SER O MASTER
    interface ens3 <-- INTERFACE QUE VAI HOSPEDAR O IP
    virtual_router_id 51 <-- TEM QUE SER O MESMO NOS DOIS PONTOS
    priority 100 <-- MAIOR PRIORIDADE = MASTER
    advert_int 1
    authentication {
        auth_type PASS <-- SE VAI TER SENHA
        auth_pass skill#39 <-- SENHA
    }
    virtual_ipaddress {
        172.16.10.100/24  # máscara ajustada
        beba:cafe::10/64
    }
```

# APÓS ISSO RESTARTE O SERVIÇO E VEJA SE ESTÁ FUNCIONANDO E NÃO SE ESQUEÇA DE REMOVER O vrrp_strict PARA RECEBER ICMP.