Para acessar o switch remotamente, um endereço IP e uma máscara de sub-rede devem ser configurados na SVI. Para configurar um SVI em um switch, use o comando **interface vlan 1** de configuração global. Vlan 1 não é uma interface física real, mas virtual. Em seguida, atribua um endereço IPv4 usando o comando **ip address** _ip-address subnet-mask_ interface configuration. Por fim, ative a interface virtual usando o comando **no shutdown** de configuração da interface.

Após a configuração desses comandos, o switch terá todos os elementos IPv4 prontos para comunicação pela rede.

```sh
Sw-Floor-1# **configure terminal**

Sw-Floor-1(config)# **interface vlan 1**

Sw-Floor-1(config-if)# **ip address 192.168.1.20 255.255.255.0**

Sw-Floor-1(config-if)# **no shutdown**

Sw-Floor-1(config-if)# **exit**

Sw-Floor-1(config)# **ip default-gateway 192.168.1.1**
```

