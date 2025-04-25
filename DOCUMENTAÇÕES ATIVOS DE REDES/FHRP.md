
---

## 📘 **Documentação: Como funciona o FHRP (First Hop Redundancy Protocol)**

---

### 🔹 O que é FHRP?

FHRP (First Hop Redundancy Protocol) é um conjunto de protocolos de **alta disponibilidade** para **gateways de rede**. Ele garante que, caso o **gateway principal (roteador/switch L3)** falhe, outro dispositivo possa assumir automaticamente, **sem interromper a comunicação da rede**.

---

### 🔸 Por que usar FHRP?

Sem FHRP, se o gateway padrão (default gateway) de uma rede falha, os dispositivos da rede ficam **sem rota para fora da sub-rede**.

Com FHRP, os dispositivos da rede configuram um **gateway virtual compartilhado** e o protocolo cuida da **transição automática** entre os gateways físicos.

---

### 🚦 Como funciona?

1. Um **gateway virtual** (com um IP e MAC virtual) é criado e anunciado aos clientes.
    
2. Dois ou mais dispositivos físicos (roteadores ou switches L3) **compartilham esse gateway virtual**.
    
3. Um dos dispositivos é eleito como **ativo (Active ou Master)**.
    
4. Se o ativo falhar, outro assume o papel automaticamente.
    

---

## 🔧 Tipos de FHRP

---

### 🟦 **HSRP (Hot Standby Router Protocol)** - Cisco

- Proprietário da Cisco.
    
- Eleição entre **Active** e **Standby**.
    
- Gateway Virtual com IP e MAC virtual.
    
- **Hello Time:** 3s (padrão) | **Hold Time:** 10s.
    

**Comandos básicos:**

```bash
interface G0/0
 standby 1 ip 192.168.1.1
 standby 1 priority 110
 standby 1 preempt
```

---

### 🟩 **VRRP (Virtual Router Redundancy Protocol)** - Padrão Aberto (RFC 5798)

- Funciona de forma similar ao HSRP.
    
- Eleição entre **Master** e **Backup**.
    
- O Master usa **seu próprio IP** como IP virtual (em alguns casos).
    
- Utilizado em ambientes mistos (Cisco, Juniper, MikroTik, etc).
    

---

### 🟥 **GLBP (Gateway Load Balancing Protocol)** - Cisco

- Proprietário da Cisco.
    
- Além da redundância, também faz **balanceamento de carga**.
    
- Todos os gateways participam **ativamente** (não só um ativo e outro standby).
    
- Divide os clientes entre os roteadores.
    

---

## 📶 Exemplo com HSRP

### Topologia:

```text
PC1 ----\
          Switch ---- R1 (Active)
PC2 ----/           \
                       R2 (Standby)
```

### Configuração:

- IP virtual: 192.168.10.1
    
- R1: IP real 192.168.10.2
    
- R2: IP real 192.168.10.3
    
- PCs usam 192.168.10.1 como gateway padrão
    

Se o R1 cair, o R2 assume 192.168.10.1 automaticamente.

---

### 🧪 Teste prático:

1. Configure HSRP no R1 e R2.
    
2. Use `ping` contínuo de um PC para um IP fora da rede.
    
3. Derrube o R1 (desconecte).
    
4. Veja que o ping **continua funcionando sem queda**.
    

---

## ✅ Benefícios

- Alta disponibilidade para o gateway padrão.
    
- Mudança automática sem intervenção manual.
    
- Suporte para vários tipos de redes.
    

---

## ⚠️ Considerações

- HSRP e GLBP são Cisco-only.
    
- VRRP é ideal para ambientes multivendor.
    
- Recomenda-se usar **preempt** para o roteador principal reassumir após voltar.
    

---

### 📊 Tabela – Opções do FHRP

|**Opções do FHRP**|**Descrição**|
|---|---|
|**HSRP (Hot Standby Router Protocol)**|HSRP é um FHRP proprietário da Cisco projetado para permitir failover transparente de um dispositivo IPv4 de primeiro salto. Fornece alta disponibilidade de rede criando um gateway padrão virtual em redes IPv4. Usa um grupo de roteadores para eleger um ativo e outro de espera. O ativo encaminha pacotes, o de espera assume quando o ativo falha. O HSRP monitora o status dos dispositivos para agir rapidamente em caso de falha.|
|**HSRP para IPv6**|FHRP da Cisco com a mesma função do HSRP, mas em ambiente IPv6. O grupo HSRP IPv6 possui um MAC virtual derivado do número do grupo e do link IPv6. Envia RAs periódicos enquanto está ativo. Quando se torna inativo, os RAs param.|
|**VRRPv2 (Protocolo de Redundância de Roteador Virtual v2)**|Protocolo aberto (não proprietário) que permite a eleição dinâmica de um roteador mestre IPv4 virtual entre múltiplos roteadores. Um é eleito como mestre e os demais atuam como backup.|
|**VRRPv3**|Suporta endereços IPv4 e IPv6. Funciona com diferentes fornecedores e é mais escalável que o VRRPv2.|
|**GLBP (Gateway Load Balancing Protocol)**|FHRP proprietário da Cisco que oferece redundância e também balanceamento de carga entre roteadores ativos. Diferente do HSRP/VRRP, todos os membros podem encaminhar pacotes.|
|**GLBP para IPv6**|Mesma função do GLBP, mas para IPv6. Permite múltiplos roteadores IPv6 atuarem como primeiro salto em uma LAN. Compartilham o tráfego sem sobrecarregar um único dispositivo.|
|**IRDP (ICMP Router Discovery Protocol)**|Solução FHRP legada baseada na RFC 1256. Permite que hosts IPv4 descubram roteadores que fornecem conectividade para redes remotas (não locais).|
