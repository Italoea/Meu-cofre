
---

# 📘 Documentação: Configuração de DHCPv4 em Roteador Cisco

---

## 🧠 Objetivo

Permitir que dispositivos em uma rede local obtenham **endereços IPv4 automaticamente** a partir de um **roteador Cisco configurado como servidor DHCP**.

---

## 🛠️ Pré-requisitos

- Roteador Cisco com IOS atualizado.
    
- Interface de rede configurada e ativa.
    
- Conhecimentos básicos de acesso ao CLI (Console, Telnet ou SSH).
    

---

## 🌐 Exemplo de Cenário

```
Rede LAN: 192.168.10.0/24
Gateway (interface do roteador): 192.168.10.1
Escopo DHCP: 192.168.10.100 – 192.168.10.200
DNS: 8.8.8.8
```

---

## 📋 Etapas da Configuração

### 1️⃣ Acesse o modo de configuração global

```bash
Router> enable
Router# configure terminal
```

---

### 2️⃣ Configure a interface da LAN com o IP do gateway

```bash
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip address 192.168.10.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
```

---

### 3️⃣ Crie o pool DHCP

```bash
Router(config)# ip dhcp pool REDE_LOCAL
```

---

### 4️⃣ Defina os parâmetros do DHCP

```bash
Router(dhcp-config)# network 192.168.10.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.10.1
Router(dhcp-config)# dns-server 8.8.8.8
Router(dhcp-config)# domain-name rede.local
Router(dhcp-config)# lease 8 12 0  ! (dias horas minutos - opcional)
Router(dhcp-config)# exit
```

---

### 5️⃣ Exclua IPs que **não devem ser entregues** (reservados para servidores, impressoras etc)

```bash
Router(config)# ip dhcp excluded-address 192.168.10.1 192.168.10.99
Router(config)# ip dhcp excluded-address 192.168.10.201 192.168.10.254
```

---

## ✅ Verificação

### Ver dispositivos com IPs atribuídos:

```bash
Router# show ip dhcp binding
```

### Ver estatísticas do serviço DHCP:

```bash
Router# show ip dhcp server statistics
```

### Ver configuração do pool:

```bash
Router# show running-config | section dhcp
```

---

## ❌ Solução de Problemas

|Problema|Solução|
|---|---|
|Clientes não recebem IP|Verifique se a interface está com IP e `no shutdown`|
|IPs fora do intervalo sendo atribuídos|Verifique o intervalo excluído e o escopo configurado|
|DHCP não responde|Verifique se há conflito com outro servidor DHCP na rede|

---

## 🛡️ Segurança

- Em ambientes maiores, use:
    
    - **DHCP Snooping** em switches para proteger contra DHCP spoofing.
        
    - VLANs dedicadas para separar tráfego DHCP.
        

---

