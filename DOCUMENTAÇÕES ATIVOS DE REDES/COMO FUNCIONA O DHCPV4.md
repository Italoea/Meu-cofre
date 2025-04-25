
---

# 📘 Documentação: Funcionamento do DHCPv4

---

## 📌 O que é o DHCPv4?

O **DHCPv4 (Dynamic Host Configuration Protocol versão 4)** é um protocolo de rede utilizado para **atribuir dinamicamente endereços IPv4** e outras informações de configuração (como máscara de sub-rede, gateway padrão e servidores DNS) aos dispositivos em uma rede, permitindo que eles se comuniquem sem a necessidade de configuração manual.

---

## 🎯 Objetivo do DHCP

- Automatizar a atribuição de endereços IP.
    
- Reduzir conflitos de IP.
    
- Centralizar a administração da rede.
    
- Oferecer parâmetros adicionais de configuração (DNS, gateway, etc).
    

---

## 📦 Componentes do DHCP

|Componente|Descrição|
|---|---|
|**Servidor DHCP**|Responsável por atribuir e gerenciar os endereços IP.|
|**Cliente DHCP**|Dispositivo que solicita configuração IP (ex: PC, notebook, celular).|
|**Agente Revezador (Relay)**|Encaminha requisições de DHCP entre clientes e servidores em redes diferentes.|

---

## 🔁 Processo de Funcionamento (DORA)

O DHCP funciona com o processo **DORA**, que consiste em 4 etapas principais:

### 1. **D – Discover (Descoberta)**

- O cliente envia um **pacote broadcast** para encontrar servidores DHCP disponíveis na rede.
    
- IP de origem: `0.0.0.0`, IP de destino: `255.255.255.255`
    
- Porta de origem: 68 (cliente), Porta de destino: 67 (servidor)
    

```
Cliente DHCP → Broadcast → "Tem algum servidor DHCP aí?"
```

### 2. **O – Offer (Oferta)**

- Um ou mais servidores DHCP respondem com uma **oferta de endereço IP** e outras configurações.
    
- Contém:
    
    - Endereço IP disponível
        
    - Máscara de sub-rede
        
    - Gateway padrão
        
    - Tempo de concessão (lease time)
        
    - Servidores DNS
        

```
Servidor DHCP → Cliente → "Tenho esse IP pra você: 192.168.1.10"
```

### 3. **R – Request (Solicitação)**

- O cliente responde **solicitando** o IP oferecido pelo servidor desejado (pode haver mais de um).
    
- Também é enviado em broadcast.
    

```
Cliente → Broadcast → "Quero usar o IP 192.168.1.10 daquele servidor."
```

### 4. **A – Acknowledge (Confirmação)**

- O servidor confirma a concessão (lease) do IP ao cliente.
    

```
Servidor → Cliente → "IP 192.168.1.10 está reservado para você. Pode usar."
```

---

## ⏳ Lease Time (Tempo de Concessão)

- O IP atribuído tem validade definida (ex: 8 horas).
    
- O cliente tenta renovar a concessão após 50% do tempo.
    
- Caso o servidor não responda:
    
    - 87,5% do tempo: nova tentativa.
        
    - Se falhar: o cliente libera o IP e volta ao processo de descoberta (DORA).
        

---

## 🧠 Outras Informações que o DHCP Pode Fornecer

- Endereço de gateway padrão (default gateway)
    
- Endereços de servidores DNS
    
- Domínio de busca DNS
    
- Nome do host (hostname)
    
- Parâmetros para PXE Boot (arranque via rede)
    

---

## 🌐 DHCP Relay (Agente Revezador)

Se o cliente e o servidor DHCP estão em **redes diferentes (sub-redes distintas)**, um **DHCP Relay** pode ser usado:

- Ele **captura** o pacote DHCP Discover enviado pelo cliente.
    
- **Encaminha** para o servidor DHCP na outra rede (unicast).
    
- Usa a configuração de **`ip helper-address`** em roteadores Cisco, por exemplo.
    

---

## 📜 Formato de Pacote DHCP (Simplificado)

- **Opções DHCP** (campo que carrega dados de configuração como IP, DNS, gateway).
    
- Outros campos:
    
    - `op`: tipo de mensagem (1 = requisição, 2 = resposta)
        
    - `xid`: identificador da transação
        
    - `yiaddr`: "Your IP address" – o IP que será atribuído
        
    - `chaddr`: endereço MAC do cliente
        
    - `flags`: usado para determinar broadcast/unicast
        

---

## 🛡️ Segurança e Riscos

- DHCP é vulnerável a ataques como:
    
    - **DHCP Spoofing**: um servidor falso oferece IPs e desvia tráfego.
        
    - **Starvation Attack**: um atacante consome todos os IPs disponíveis.
        
- Soluções:
    
    - **DHCP Snooping** em switches gerenciáveis.
        
    - Controle de portas confiáveis.
        
    - VLANs separadas para clientes e servidores.
        

---
