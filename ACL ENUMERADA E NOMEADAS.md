
---

# 📄 Documentação: ACL Enumerada e Nomeada no Cisco IOS

## ✅ O que é uma ACL?

**ACL (Access Control List)** é uma lista de regras aplicadas a interfaces de roteadores ou switches Layer 3, que define **quais pacotes podem entrar ou sair** da interface com base em critérios como endereço IP, protocolo, porta, etc.

---

## 🔢 Tipos de ACLs

Existem dois tipos principais de ACLs no Cisco IOS:

### 1. ACL Enumerada (Numerada)

São definidas por **números** que representam o tipo e a função da lista.

#### 📌 Faixas de Números:

- **Standard ACLs:** 1 a 99 e 1300 a 1999
    
- **Extended ACLs:** 100 a 199 e 2000 a 2699
    

---

### 🔹 ACL Standard (Enumerada)

Filtra apenas com base no **endereço IP de origem**.

#### 📘 Sintaxe:

```bash
access-list [número] [permit|deny] [origem] [wildcard]
```

#### 📋 Exemplo:

```bash
access-list 10 permit 192.168.1.0 0.0.0.255
access-list 10 deny any
interface GigabitEthernet0/0
 ip access-group 10 in
```

---

### 🔸 ACL Extended (Enumerada)

Filtra com base em **IP de origem, IP de destino, protocolo, portas**, etc.

#### 📘 Sintaxe:

```bash
access-list [número] [permit|deny] [protocolo] [origem] [wildcard] [destino] [wildcard] [operador] [porta]
```

#### 📋 Exemplo:

```bash
access-list 100 permit tcp 192.168.1.0 0.0.0.255 any eq 80
access-list 100 deny ip any any
interface GigabitEthernet0/0
 ip access-group 100 out
```

---

## 🏷️ ACL Nomeada

Permite usar **nomes** personalizados para identificar a ACL. É mais legível e gerenciável, e permite **editar ACLs sem removê-las**.

---

### 🔹 ACL Standard (Nomeada)

#### 📘 Sintaxe:

```bash
ip access-list standard [nome]
 [permit|deny] [origem] [wildcard]
```

#### 📋 Exemplo:

```bash
ip access-list standard BLOQUEIO-REDE-A
 permit 10.0.0.0 0.0.0.255
 deny any
interface GigabitEthernet0/1
 ip access-group BLOQUEIO-REDE-A in
```

---

### 🔸 ACL Extended (Nomeada)

#### 📘 Sintaxe:

```bash
ip access-list extended [nome]
 [permit|deny] [protocolo] [origem] [wildcard] [destino] [wildcard] [operador] [porta]
```

#### 📋 Exemplo:

```bash
ip access-list extended BLOQUEIO-HTTP
 deny tcp any any eq 80
 permit ip any any
interface GigabitEthernet0/1
 ip access-group BLOQUEIO-HTTP in
```

---

## 🧠 Wildcard Mask – Explicação Rápida

A **Wildcard Mask** é o oposto da máscara de sub-rede:

|Sub-rede|Wildcard|Significado|
|---|---|---|
|255.255.255.0|0.0.0.255|Ignora o último octeto|

---

## ⚠️ Regras Importantes

- ACLs são lidas **de cima para baixo**.
    
- Existe um **"deny all" implícito** no final.
    
- Só é possível aplicar **uma ACL por direção e por interface**.
    
- Use comandos como `show access-lists` e `show ip interface` para diagnosticar.
    

---

## 🧪 Testando ACLs

Após aplicar a ACL, teste com:

```bash
ping [IP]
telnet [IP] [porta]
```

---

## ✅ Boas Práticas

- Use **ACL nomeada** para facilitar manutenção.
    
- **Documente** cada linha de ACL.
    
- Aplique ACLs em **pontos estratégicos**, preferencialmente **o mais próximo da origem para negar**.
    
- Evite bloqueios genéricos como `deny ip any any`, sem necessidade.
    

---
