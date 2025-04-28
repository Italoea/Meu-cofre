
# Configuração de NAT no Roteador SHANGHAI-EDGE para Acesso Externo

Este documento detalha o processo de configuração de NAT (Network Address Translation) no roteador SHANGHAI-EDGE, permitindo que os hosts da rede interna SHANGHAI (10.0.0.0/24) acessem redes externas utilizando o endereço IP público da interface do roteador (210.103.5.10). O NAT será configurado com sobrecarga (PAT - Port Address Translation) para mapear múltiplos IPs privados para um único IP público.

## Topologia de Rede

- **SHANGHAI-EDGE**: Roteador de borda.
    - Interface e0/0: Conectada ao ISP-ROUTER (rede 210.103.5.0/30, IP 210.103.5.10/30).
    - Interface e0/1: Conectada à rede interna SHANGHAI (rede 10.0.0.0/24, IP 10.0.0.1/24).
- **SHANGHAI-SW**: Switch interno conectado a SHANGHAI-EDGE.
- **SHANGHAI-CLIENT**: Host na rede 10.0.0.0/24.
- **ISP-ROUTER**: Roteador externo conectado à Internet.

## Objetivo

Configurar NAT no SHANGHAI-EDGE para que os hosts da rede 10.0.0.0/24 usem o IP público 210.103.5.10 ao acessar redes externas.

## Pré-requisitos

- Acesso ao roteador SHANGHAI-EDGE via console ou SSH.
- Privilégios administrativos no roteador.
- Interfaces já configuradas com os IPs corretos:
    - e0/0: 210.103.5.10/30.
    - e0/1: 10.0.0.1/24.
- Roteamento entre SHANGHAI-EDGE e ISP-ROUTER configurado (por exemplo, via OSPF, conforme documentação anterior).

## Passos para Configuração

### 1. Acesse o Modo de Configuração Global

Entre no modo de configuração global do roteador:

```plaintext
SHANGHAI-EDGE> enable
SHANGHAI-EDGE# configure terminal
```

### 2. Verifique e Configure as Interfaces

Certifique-se de que as interfaces estão configuradas com os IPs corretos e ativas:

```plaintext
SHANGHAI-EDGE(config)# interface ethernet0/0
SHANGHAI-EDGE(config-if)# ip address 210.103.5.10 255.255.255.252
SHANGHAI-EDGE(config-if)# description "Conexão com ISP-ROUTER"
SHANGHAI-EDGE(config-if)# no shutdown
SHANGHAI-EDGE(config-if)# exit
SHANGHAI-EDGE(config)# interface ethernet0/1
SHANGHAI-EDGE(config-if)# ip address 10.0.0.1 255.255.255.0
SHANGHAI-EDGE(config-if)# description "Conexão com SHANGHAI-SW"
SHANGHAI-EDGE(config-if)# no shutdown
SHANGHAI-EDGE(config-if)# exit
```

**Nota**: A máscara 255.255.255.252 (/30) na interface e0/0 é usada porque a rede 210.103.5.0/30 suporta apenas 2 hosts (210.103.5.9 e 210.103.5.10).

### 3. Configure uma ACL para Identificar o Tráfego Interno

Crie uma lista de controle de acesso (ACL) para identificar o tráfego da rede interna 10.0.0.0/24 que será traduzido:

```plaintext
SHANGHAI-EDGE(config)# access-list 1 permit 10.0.0.0 0.0.0.255
```

**Nota**: A wildcard mask 0.0.0.255 corresponde à sub-rede 10.0.0.0/24.

### 4. Configure o NAT de Sobrecarga

Configure o NAT dinâmico com sobrecarga para traduzir os IPs da rede 10.0.0.0/24 para o IP da interface e0/0 (210.103.5.10):

```plaintext
SHANGHAI-EDGE(config)# ip nat inside source list 1 interface ethernet0/0 overload
```

- `ip nat inside source`: Traduz os IPs de origem da rede interna.
- `list 1`: Usa a ACL 1 para identificar os IPs a serem traduzidos.
- `interface ethernet0/0`: Usa o IP da interface e0/0 (210.103.5.10) como o IP público.
- `overload`: Habilita PAT, permitindo múltiplos IPs privados compartilharem o mesmo IP público usando portas diferentes.

### 5. Defina as Interfaces como Inside e Outside

Marque as interfaces para o NAT:

```plaintext
SHANGHAI-EDGE(config)# interface ethernet0/0
SHANGHAI-EDGE(config-if)# ip nat outside
SHANGHAI-EDGE(config-if)# exit
SHANGHAI-EDGE(config)# interface ethernet0/1
SHANGHAI-EDGE(config-if)# ip nat inside
SHANGHAI-EDGE(config-if)# exit
```

- `ip nat outside`: Interface conectada à rede externa (ISP-ROUTER).
- `ip nat inside`: Interface conectada à rede interna (SHANGHAI-SW).

### 6. (Opcional) Verifique o Roteamento

Certifique-se de que o roteamento para redes externas está configurado. Se você já configurou OSPF anteriormente, inclua a rede 210.103.5.0/30 no OSPF:

```plaintext
SHANGHAI-EDGE(config)# router ospf 1
SHANGHAI-EDGE(config-router)# network 210.103.5.0 0.0.0.3 area 0
SHANGHAI-EDGE(config-router)# network 10.0.0.0 0.0.0.255 area 0
SHANGHAI-EDGE(config-router)# exit
```

**Nota**: A wildcard mask 0.0.0.3 corresponde à sub-rede 210.103.5.0/30.

### 7. Salve a Configuração

Salve as alterações para que persistam após reinicializações:

```plaintext
SHANGHAI-EDGE(config)# exit
SHANGHAI-EDGE# write memory
```

## Verificação da Configuração

Use os seguintes comandos para verificar o funcionamento do NAT:

- Verificar as traduções NAT ativas:

```plaintext
SHANGHAI-EDGE# show ip nat translations
```

Exemplo de saída esperada:

```plaintext
Pro Inside global      Inside local       Outside local      Outside global
tcp 210.103.5.10:12345 10.0.0.100:12345   ---                ---
```

- Verificar o status das interfaces:

```plaintext
SHANGHAI-EDGE# show ip interface brief
```

Exemplo de saída:

```plaintext
Interface       IP-Address      OK? Method Status                Protocol
Ethernet0/0     210.103.5.10    YES manual up                    up
Ethernet0/1     10.0.0.1        YES manual up                    up
```

- Verificar a configuração NAT:

```plaintext
SHANGHAI-EDGE# show running-config | section ip nat
```

Exemplo de saída:

```plaintext
ip nat inside source list 1 interface Ethernet0/0 overload
interface Ethernet0/0
 ip nat outside
interface Ethernet0/1
 ip nat inside
```

- Verificar a ACL:

```plaintext
SHANGHAI-EDGE# show access-lists
```

Exemplo de saída:

```plaintext
Standard IP access list 1
    10 permit 10.0.0.0, wildcard bits 0.0.0.255
```

- Verificar as rotas:

```plaintext
SHANGHAI-EDGE# show ip route
```

## Teste de Conectividade

1. A partir de um host na rede 10.0.0.0/24 (como SHANGHAI-CLIENT), tente acessar um recurso externo (por exemplo, pingar um IP público ou acessar um site).
2. Verifique as traduções NAT para confirmar que o tráfego está sendo traduzido corretamente.

## Exemplo Completo

Comando completo para configurar o NAT no roteador SHANGHAI-EDGE:

```plaintext
SHANGHAI-EDGE> enable
SHANGHAI-EDGE# configure terminal
SHANGHAI-EDGE(config)# interface ethernet0/0
SHANGHAI-EDGE(config-if)# ip address 210.103.5.10 255.255.255.252
SHANGHAI-EDGE(config-if)# description "Conexão com ISP-ROUTER"
SHANGHAI-EDGE(config-if)# no shutdown
SHANGHAI-EDGE(config-if)# exit
SHANGHAI-EDGE(config)# interface ethernet0/1
SHANGHAI-EDGE(config-if)# ip address 10.0.0.1 255.255.255.0
SHANGHAI-EDGE(config-if)# description "Conexão com SHANGHAI-SW"
SHANGHAI-EDGE(config-if)# no shutdown
SHANGHAI-EDGE(config-if)# exit
SHANGHAI-EDGE(config)# access-list 1 permit 10.0.0.0 0.0.0.255
SHANGHAI-EDGE(config)# ip nat inside source list 1 interface ethernet0/0 overload
SHANGHAI-EDGE(config)# interface ethernet0/0
SHANGHAI-EDGE(config-if)# ip nat outside
SHANGHAI-EDGE(config-if)# exit
SHANGHAI-EDGE(config)# interface ethernet0/1
SHANGHAI-EDGE(config-if)# ip nat inside
SHANGHAI-EDGE(config-if)# exit
SHANGHAI-EDGE(config)# router ospf 1
SHANGHAI-EDGE(config-router)# network 210.103.5.0 0.0.0.3 area 0
SHANGHAI-EDGE(config-router)# network 10.0.0.0 0.0.0.255 area 0
SHANGHAI-EDGE(config-router)# exit
SHANGHAI-EDGE(config)# exit
SHANGHAI-EDGE# write memory
```

## Solução de Problemas

- **Hosts não conseguem acessar redes externas**:
    - Verifique as traduções NAT com `show ip nat translations`. Se não houver traduções, confira a ACL e as marcações de `inside`/`outside`.
    - Confirme que as interfaces estão ativas com `show ip interface brief`.
- **Tráfego não está sendo roteado**:
    - Verifique as rotas com `show ip route`. Certifique-se de que o roteador sabe como alcançar redes externas via ISP-ROUTER.
    - Se OSPF estiver configurado, verifique os vizinhos com `show ip ospf neighbor`.
- **ACL bloqueando tráfego**:
    - Confirme que a ACL 1 está permitindo o tráfego da rede 10.0.0.0/24 com `show access-lists`.
- **Conexão bloqueada pelo ISP-ROUTER**:
    - Verifique se há ACLs ou firewalls no ISP-ROUTER bloqueando o tráfego NAT. Pode ser necessário ajustar políticas no ISP-ROUTER.

## Considerações Adicionais

- **Segurança**: Considere configurar ACLs adicionais para restringir o tráfego de entrada na interface e0/0, permitindo apenas respostas ao tráfego iniciado pela rede interna.
- **Monitoramento**: Use comandos como `debug ip nat` para depurar o processo de NAT, mas tenha cuidado, pois isso pode gerar muitas mensagens no log.