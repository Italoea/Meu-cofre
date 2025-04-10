
---

# 📘 Documentação: Configuração Detalhada do Spanning Tree (STP) com 3 Switches

## 🎯 Objetivo

Evitar loops de camada 2 e garantir redundância entre switches, utilizando o protocolo Spanning Tree Protocol (STP).

## 🧠 Conceitos Básicos

- **STP** é um protocolo que impede loops de rede em topologias redundantes.
    
- Ele **desativa automaticamente portas** para formar uma **árvore sem ciclos**.
    
- **Bridge ID = prioridade (padrão 32768) + MAC**
    
- A **Bridge com menor Bridge ID** vira a **Root Bridge**.
    
- Tipos de portas STP:
    
    - **Root Port (RP)**: melhor caminho para a Root Bridge.
        
    - **Designated Port (DP)**: melhor porta para um segmento.
        
    - **Blocked Port**: desativada para evitar loops.
        

---

## 🖧 Topologia (Exemplo)

```
         [SW1] <----- Root Bridge
        /     \
     [SW2]   [SW3]
        \     /
         -------
```

## ✅ Pré-requisitos

- Todos os switches configurados com IPs para gerenciamento (opcional).
    
- Conexões físicas entre os switches usando interfaces FastEthernet ou Gigabit.
    
- Acesso ao modo privilegiado dos switches.
    

---

## 🔧 Etapas da Configuração

### 1. **Verificar se o STP está ativado**

Nos switches Cisco, STP já vem ativado por padrão:

```bash
SW1# show spanning-tree
```

---

### 2. **Escolher a Root Bridge (SW1 no exemplo)**

Configure a prioridade do switch SW1 com valor menor (quanto menor, maior a chance de ser Root):

```bash
SW1(config)# spanning-tree vlan 1 priority 4096
```

> Valor padrão é 32768. Pode usar 4096, 8192, etc.

Nos outros switches, pode deixar o padrão ou forçar a não ser Root:

```bash
SW2(config)# spanning-tree vlan 1 priority 32768
SW3(config)# spanning-tree vlan 1 priority 32768
```

---

### 3. **Configurar trunk entre os switches**

```bash
SW1(config)# interface range f0/1 - 2
SW1(config-if-range)# switchport mode trunk
```

Repita isso em todas as portas que conectam switches entre si.

---

### 4. **Verificar o status STP**

Após conectar os switches:

```bash
SW1# show spanning-tree vlan 1
```

Verifique:

- Qual switch é Root
    
- Quais portas estão em estado **Forwarding** e **Blocking**
    

---

### 5. **Ajustar PortFast para hosts (não switches!)**

```bash
SW(config)# interface f0/10
SW(config-if)# switchport mode access
SW(config-if)# spanning-tree portfast
```

> **Nunca ative PortFast em links entre switches!**

---

## 🔍 Comandos de Verificação Úteis

```bash
show spanning-tree            ! mostra a árvore STP
show spanning-tree vlan 1    ! mostra detalhes por VLAN
show interfaces status       ! vê quais interfaces estão ativas
```

---

## 📌 Dicas Extras

- Use **RSTP** (modo mais rápido) com:
    
    ```bash
    SW(config)# spanning-tree mode rapid-pvst
    ```
    
- Em ambientes com múltiplas VLANs, configure STP por VLAN (`PVST+`):
    
    ```bash
    SW(config)# spanning-tree vlan 10 priority 4096
    SW(config)# spanning-tree vlan 20 priority 8192
    ```
    

---
