
# Configuração de Rota Dinâmica OSPF em Roteador Cisco

Este documento descreve o processo de configuração de uma rota dinâmica utilizando o protocolo OSPF (Open Shortest Path First) em um roteador Cisco. O OSPF é um protocolo de roteamento de estado de enlace que permite a troca de informações de roteamento entre roteadores de forma eficiente.

## Pré-requisitos

- Acesso ao roteador Cisco via console, SSH ou Telnet.
- Privilégios administrativos no roteador.
- Conhecimento das interfaces de rede e sub-redes que serão configuradas.
- Endereços IP já configurados nas interfaces do roteador.

## Passos para Configuração

### 1. Acesse o Modo de Configuração Global

Entre no modo de configuração global do roteador:

```plaintext
Router> enable
Router# configure terminal
```

### 2. Inicie o Processo OSPF

Inicie o processo OSPF com um ID de processo (por exemplo, 1). O ID de processo é local ao roteador e não precisa ser o mesmo em todos os roteadores.

```plaintext
Router(config)# router ospf 1
```

### 3. Configure o Router-ID (Opcional)

Defina um Router-ID único para identificar o roteador no domínio OSPF. Se não configurado, o roteador usará o maior endereço IP de suas interfaces.

```plaintext
Router(config-router)# router-id 192.168.1.1
```

### 4. Anuncie as Redes

Especifique as redes que o roteador anunciará no OSPF, incluindo a máscara de sub-rede inversa (wildcard mask) e a área OSPF (por exemplo, área 0).

```plaintext
Router(config-router)# network 192.168.1.0 0.0.0.255 area 0
Router(config-router)# network 192.168.2.0 0.0.0.255 area 0
```

**Nota**: Substitua os endereços de rede e a área conforme sua topologia. A wildcard mask é calculada como o inverso da máscara de sub-rede (por exemplo, 255.255.255.0 → 0.0.0.255).

### 5. (Opcional) Configure Parâmetros Adicionais

Ajuste parâmetros como a prioridade do roteador ou o custo das interfaces, se necessário:

- Definir prioridade para eleição de DR/BDR:

```plaintext
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip ospf priority 10
```

- Definir custo da interface:

```plaintext
Router(config-if)# ip ospf cost 10
```

### 6. Salve a Configuração

Salve as alterações para que persistam após reinicializações:

```plaintext
Router# write memory
```

## Verificação da Configuração

Use os seguintes comandos para verificar o status do OSPF:

- Verificar vizinhos OSPF:

```plaintext
Router# show ip ospf neighbor
```

- Verificar tabelas de roteamento OSPF:

```plaintext
Router# show ip route ospf
```

- Verificar detalhes do protocolo OSPF:

```plaintext
Router# show ip ospf
```

## Exemplo Completo

Suponha que o roteador tenha duas interfaces:

- GigabitEthernet0/0: 192.168.1.1/24
- GigabitEthernet0/1: 192.168.2.1/24

Comando completo:

```plaintext
Router> enable
Router# configure terminal
Router(config)# router ospf 1
Router(config-router)# router-id 192.168.1.1
Router(config-router)# network 192.168.1.0 0.0.0.255 area 0
Router(config-router)# network 192.168.2.0 0.0.0.255 area 0
Router(config-router)# exit
Router(config)# write memory
```

## Solução de Problemas

- **Sem vizinhos OSPF**: Verifique se as interfaces estão ativas (`show ip interface brief`) e se os endereços de rede estão corretamente anunciados.
- **Rotas ausentes**: Confirme que as áreas estão corretamente configuradas e que não há filtros bloqueando anúncios.
- **Configuração não persiste**: Certifique-se de salvar a configuração com `write memory`.