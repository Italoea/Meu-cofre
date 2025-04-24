
# Guia para Criar uma Rota Estática em um Roteador Cisco

## Introdução

Uma rota estática é uma entrada manual na tabela de roteamento de um roteador, que define o caminho que os pacotes devem seguir para alcançar uma rede de destino específica. Diferentemente das rotas dinâmicas, que são aprendidas automaticamente por protocolos de roteamento (como OSPF, EIGRP ou BGP), as rotas estáticas são configuradas diretamente pelo administrador de rede. Elas são úteis em redes pequenas ou quando há necessidade de controle preciso sobre o encaminhamento de pacotes.

Este guia detalha o processo de criação de uma rota estática em um roteador Cisco, incluindo o acesso ao roteador, a configuração da rota, e a verificação da implementação.

---

## Pré-requisitos

Antes de começar, certifique-se de que:

- Você tem acesso físico (via cabo de console) ou remoto (via SSH/Telnet) ao roteador Cisco.
- Você conhece as credenciais de acesso (usuário/senha ou apenas senha para o modo EXEC privilegiado).
- Você sabe o endereço de destino (rede) e o próximo salto (next-hop) ou a interface de saída para a rota estática.
- O roteador está inicializado e funcionando corretamente.
- Você entende a topologia da rede, incluindo os endereços IP das interfaces envolvidas.

### Exemplo de Topologia

Considere a seguinte topologia para este guia:

- **Roteador R1**:
    - Interface Ethernet0/0: 192.168.10.1/24 (conectada à rede local 192.168.10.0/24).
    - Interface Ethernet0/1: 172.16.0.1/16 (conectada ao Roteador R2).
- **Roteador R2**:
    - Interface Ethernet0/1: 172.16.0.2/16 (conectada ao Roteador R1).
    - Interface Ethernet0/0: 10.10.0.1/24 (conectada à rede local 10.10.0.0/24).
- **Objetivo**: Configurar uma rota estática em R1 para que ele saiba como enviar pacotes para a rede 10.10.0.0/24 (rede conectada a R2) através do próximo salto 172.16.0.2.

---

## Passo a Passo para Criar uma Rota Estática

### 1. Acesse o Roteador

1. **Conexão Física ou Remota**:
    
    - Se estiver usando um cabo de console, conecte o cabo ao roteador e use um software de terminal como PuTTY ou Tera Term.
    - Se estiver acessando remotamente, use SSH ou Telnet. Exemplo de comando para SSH:
        
        ```
        ssh -l <username> <ip-do-roteador>
        ```
        
        Exemplo: `ssh -l admin 192.168.10.1`
    - Caso use Telnet (menos seguro), o comando seria:
        
        ```
        telnet 192.168.10.1
        ```
        
2. **Entre no Modo EXEC**:
    
    - Ao se conectar, você estará no modo EXEC do usuário (prompt `>`). Digite:
        
        ```
        enable
        ```
        
    - Insira a senha, se solicitada. O prompt mudará para `#`, indicando o modo EXEC privilegiado.
    
    Exemplo de saída:
    
    ```
    Router> enable
    Password: ******
    Router#
    ```
    

### 2. Verifique a Tabela de Roteamento Atual

Antes de adicionar a rota estática, é importante verificar a tabela de roteamento atual para entender quais rotas já estão configuradas.

1. Use o comando:
    
    ```
    show ip route
    ```
    
    - Isso exibe a tabela de roteamento atual, incluindo rotas conectadas (`C`), estáticas (`S`), e dinâmicas (como `O` para OSPF).
    
    Exemplo de saída (antes de adicionar a rota estática):
    
    ```
    Router# show ip route
    Codes: C - connected, S - static, R - RIP, M - mobile, B - BGP
           D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
           N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
           E1 - OSPF external type 1, E2 - OSPF external type 2
           i - IS-IS, su - IS-IS summary, L1 - IS-IS level-1, L2 - IS-IS level-2
           ia - IS-IS inter area, * - candidate default, U - per-user static route
           o - ODR, P - periodic downloaded static route
    
    Gateway of last resort is not set
    
    C    192.168.10.0/24 is directly connected, Ethernet0/0
    C    172.16.0.0/16 is directly connected, Ethernet0/1
    ```
    
    - Note que não há uma rota para 10.10.0.0/24, o que significa que R1 não sabe como alcançar essa rede.
2. Verifique as interfaces e seus endereços IP para confirmar a configuração:
    
    ```
    show ip interface brief
    ```
    
    Exemplo de saída:
    
    ```
    Interface              IP-Address      OK? Method Status                Protocol
    Ethernet0/0            192.168.10.1    YES manual up                    up
    Ethernet0/1            172.16.0.1      YES manual up                    up
    ```
    
    - Certifique-se de que as interfaces estão no estado "up/up". Se alguma estiver "down", ative-a no modo de configuração com `no shutdown`.

### 3. Entre no Modo de Configuração Global

Para adicionar a rota estática, você precisa entrar no modo de configuração global.

1. Digite:
    
    ```
    configure terminal
    ```
    
    Ou, abreviadamente:
    
    ```
    conf t
    ```
    
    - O prompt mudará para `Router(config)#`.
    
    Exemplo:
    
    ```
    Router# conf t
    Enter configuration commands, one per line.  End with CNTL/Z.
    Router(config)#
    ```
    

### 4. Adicione a Rota Estática

Agora, configure a rota estática usando o comando `ip route`. A sintaxe básica é:

```
ip route <rede-destino> <máscara> <próximo-salto> [distância-administrativa]
```

- `<rede-destino>`: Endereço de rede de destino (ex.: 10.10.0.0).
- `<máscara>`: Máscara de sub-rede (ex.: 255.255.255.0 para /24).
- `<próximo-salto>`: Endereço IP do próximo roteador ou interface de saída.
- `[distância-administrativa]` (opcional): Valor de prioridade da rota (padrão é 1 para rotas estáticas).

#### Exemplo de Configuração

Para nosso cenário, queremos que R1 envie pacotes para a rede 10.10.0.0/24 através do próximo salto 172.16.0.2 (endereço de R2 na rede 172.16.0.0/16). O comando seria:

```
ip route 10.10.0.0 255.255.255.0 172.16.0.2
```

1. Digite o comando no modo de configuração global:
    
    ```
    Router(config)# ip route 10.10.0.0 255.255.255.0 172.16.0.2
    ```
    
2. (Opcional) Se quiser especificar uma distância administrativa diferente (por exemplo, 5), adicione o valor no final:
    
    ```
    Router(config)# ip route 10.10.0.0 255.255.255.0 172.16.0.2 5
    ```
    

#### Alternativa: Usar uma Interface de Saída

Em vez de especificar o próximo salto, você pode configurar a rota estática apontando diretamente para a interface de saída. Isso é menos comum e pode causar problemas em redes multiacesso (como Ethernet), mas é válido em cenários ponto a ponto. Exemplo:

```
Router(config)# ip route 10.10.0.0 255.255.255.0 Ethernet0/1
```

- **Nota**: Use o próximo salto (IP) em vez da interface de saída sempre que possível, para evitar resolução ARP desnecessária.

### 5. Saia do Modo de Configuração

Após adicionar a rota, saia do modo de configuração global:

```
Router(config)# exit
Router#
```

Ou pressione `Ctrl+Z` para voltar diretamente ao modo EXEC privilegiado:

```
Router(config)# ^Z
Router#
```

### 6. Verifique a Nova Rota Estática

Confirme que a rota estática foi adicionada corretamente à tabela de roteamento.

1. Use o comando:
    
    ```
    show ip route
    ```
    
    Exemplo de saída após adicionar a rota:
    
    ```
    Router# show ip route
    Codes: C - connected, S - static, R - RIP, M - mobile, B - BGP
           D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
           N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
           E1 - OSPF external type 1, E2 - OSPF external type 2
           i - IS-IS, su - IS-IS summary, L1 - IS-IS level-1, L2 - IS-IS level-2
           ia - IS-IS inter area, * - candidate default, U - per-user static route
           o - ODR, P - periodic downloaded static route
    
    Gateway of last resort is not set
    
    C    192.168.10.0/24 is directly connected, Ethernet0/0
    C    172.16.0.0/16 is directly connected, Ethernet0/1
    S    10.10.0.0/24 [1/0] via 172.16.0.2
    ```
    
    - A linha com `S` indica a rota estática recém-adicionada. O `[1/0]` significa que a distância administrativa é 1 (padrão) e a métrica é 0 (como é estática).
2. Verifique a configuração atual para confirmar que a rota foi salva:
    
    ```
    show running-config | include ip route
    ```
    
    Exemplo de saída:
    
    ```
    Router# show running-config | include ip route
    ip route 10.10.0.0 255.255.255.0 172.16.0.2
    ```
    

### 7. Salve a Configuração

Para garantir que a rota estática persista após um reinício do roteador, salve a configuração atual na memória não volátil (NVRAM):

```
Router# write memory
```

Ou, abreviadamente:

```
Router# wr
```

Exemplo de saída:

```
Router# wr
Building configuration...
[OK]
Router#
```

### 8. Teste a Conectividade

Após adicionar a rota estática, teste a conectividade para confirmar que ela está funcionando.

1. **Ping a partir do Roteador**:
    
    - Em R1, tente fazer um ping para um endereço na rede de destino (10.10.0.0/24). Exemplo:
        
        ```
        ping 10.10.0.60
        ```
        
        Exemplo de saída (se bem-sucedido):
        
        ```
        Router# ping 10.10.0.60
        Type escape sequence to abort.
        Sending 5, 100-byte ICMP Echos to 10.10.0.60, timeout is 2 seconds:
        !!!!!
        Success rate is 100 percent (5/5), round-trip min/avg/max = 1/2/4 ms
        ```
        
    - Se o ping falhar, pode haver problemas como:
        
        - Rota de retorno ausente no Roteador R2 (R2 precisa de uma rota estática para 192.168.10.0/24).
        - Interface desativada ou configuração incorreta.
        - ACLs ou firewall bloqueando o tráfego ICMP.
2. **Ping a partir de um Host**:
    
    - Se houver um host na rede 192.168.10.0/24 (como um PC com IP 192.168.10.24), tente fazer um ping para 10.10.0.60 a partir desse host. Isso testa a conectividade de ponta a ponta.
3. **Traceroute (Opcional)**:
    
    - Use o comando `traceroute` para ver o caminho que os pacotes estão seguindo:
        
        ```
        traceroute 10.10.0.60
        ```
        
        Exemplo de saída:
        
        ```
        Router# traceroute 10.10.0.60
        Type escape sequence to abort.
        Tracing the route to 10.10.0.60
        
        1 172.16.0.2 4 msec 4 msec 4 msec
        2 10.10.0.60 8 msec 8 msec 8 msec
        ```
        

### 9. Solução de Problemas (Opcional)

Se a conectividade não funcionar após adicionar a rota estática, siga estas etapas para diagnosticar:

1. **Verifique as Interfaces**:
    
    ```
    show ip interface brief
    ```
    
    - Certifique-se de que as interfaces relevantes (Ethernet0/0 e Ethernet0/1) estão "up/up".
2. **Verifique a Tabela ARP**:
    
    ```
    show arp
    ```
    
    - Confirme que o roteador consegue resolver o endereço MAC do próximo salto (172.16.0.2).
    
    Exemplo de saída:
    
    ```
    Router# show arp
    Protocol  Address          Age (min)  Hardware Addr   Type   Interface
    Internet  172.16.0.1              -   0012.3456.7890  ARPA   Ethernet0/1
    Internet  172.16.0.2              5   00a1.b2c3.d4e5  ARPA   Ethernet0/1
    ```
    
3. **Verifique a Rota de Retorno**:
    
    - No Roteador R2, confirme se há uma rota para a rede 192.168.10.0/24. Se não houver, adicione:
        
        ```
        ip route 192.168.10.0 255.255.255.0 172.16.0.1
        ```
        
4. **Verifique ACLs ou Firewalls**:
    
    ```
    show access-lists
    ```
    
    - Se houver uma ACL bloqueando ICMP, ajuste ou remova a regra.
5. **Debug (Avançado)**:
    
    - Use comandos de depuração para ver o que está acontecendo com os pacotes:
        
        ```
        debug ip packet
        ```
        
        - Para desativar a depuração:
        
        ```
        undebug all
        ```
        

---

## Considerações Finais

- **Vantagens das Rotas Estáticas**:
    - Simples de configurar em redes pequenas.
    - Baixa sobrecarga no roteador, pois não requer protocolos de roteamento.
    - Controle preciso sobre o encaminhamento de pacotes.
- **Desvantagens**:
    - Não escalável para redes grandes (muitas rotas manuais podem ser difíceis de gerenciar).
    - Não se adapta automaticamente a mudanças na topologia (como falhas de link).
- **Alternativas**:
    - Em redes maiores, considere usar protocolos de roteamento dinâmico como OSPF ou EIGRP, que aprendem rotas automaticamente.

Se precisar de mais ajuda com a configuração ou solução de problemas, forneça detalhes adicionais, como a topologia completa ou a saída dos comandos de verificação.

---

## Resumo dos Comandos Usados

- Acessar o modo EXEC privilegiado: `enable`
- Verificar a tabela de roteamento: `show ip route`
- Verificar interfaces: `show ip interface brief`
- Entrar no modo de configuração: `configure terminal`
- Adicionar rota estática: `ip route <rede> <máscara> <próximo-salto>`
- Salvar configuração: `write memory`
- Testar conectividade: `ping <ip>` ou `traceroute <ip>`
- Verificar configuração: `show running-config | include ip route`