


Primeiro passo, configurar a ACL sempre no roteador mais perto dos hosts que pretendo restringir.

Claro! Vou montar uma documentação simples, no estilo profissional, para **configuração de uma ACL padrão (Standard ACL)** em roteadores Cisco.

---

# 📄 Documentação Técnica

## Configuração de ACL Padrão (Standard ACL) em Equipamentos Cisco

---

## 1. Objetivo

Configurar uma ACL padrão para **permitir o tráfego** de uma rede específica e **negar o tráfego** das demais redes.

---

## 2. Requisitos

- Acesso privilegiado ao roteador (`enable`).
    
- Entrar no modo de configuração global (`configure terminal`).
    
- Conhecimento da rede que deverá ser permitida.
    

---

## 3. Conceitos Importantes

- **Standard ACL** filtra **somente** pelo **endereço IP de origem**.
    
- A ACL deve ser aplicada o mais próximo possível do **destino**.
    
- **Wildcard Mask** é usada para definir a faixa de IPs.
    

---

## 4. Comandos

### 4.1 Criar uma ACL numérica

```bash
R1(config)# access-list [Número da ACL] permit [IP] [Wildcard Mask]
R1(config)# access-list [Número da ACL] deny any
```

**Exemplo**:

```bash
R1(config)# access-list 10 permit 192.168.10.0 0.0.0.255
R1(config)# access-list 10 deny any
```

### 4.2 Criar uma ACL nomeada

```bash
R1(config)# ip access-list standard [Nome da ACL]
R1(config-std-nacl)# permit [IP] [Wildcard Mask]
R1(config-std-nacl)# deny any
```

**Exemplo**:

```bash
R1(config)# ip access-list standard PERMIT-REDE10
R1(config-std-nacl)# permit 192.168.10.0 0.0.0.255
R1(config-std-nacl)# deny any
```

---

## 5. Aplicar a ACL na Interface

Escolha a interface que irá controlar o tráfego, e aplique a ACL:

```bash
R1(config)# interface [Interface]
R1(config-if)# ip access-group [Número ou Nome da ACL] [in | out]
```

- `in` → tráfego que **entra** na interface.
    
- `out` → tráfego que **sai** pela interface.
    

**Exemplo**:

```bash
R1(config)# interface GigabitEthernet0/0
R1(config-if)# ip access-group 10 in
```

ou

```bash
R1(config)# interface GigabitEthernet0/0
R1(config-if)# ip access-group PERMIT-REDE10 in
```

---

## 6. Verificação

Após a configuração, verifique se a ACL foi criada e aplicada corretamente:

```bash
show access-lists
show ip interface [Interface]
```

**Exemplo**:

```bash
show access-lists
show ip interface GigabitEthernet0/0
```

Esses comandos mostram quais ACLs estão configuradas e associadas às interfaces.

---

## 7. Notas

- Sempre lembre que existe um **"deny any" implícito** ao final da ACL.
    
- Se nenhuma linha `permit` combinar com o pacote, ele será **automaticamente bloqueado**.
    
- Wildcard Masks:
    
    - `0.0.0.0` = corresponde exatamente a um IP específico.
        
    - `0.0.0.255` = corresponde a qualquer IP dentro de uma sub-rede /24.
        

---

# 📈 Exemplo Prático de Funcionamento

|Origem|Resultado|
|---|---|
|192.168.10.5|Permitido|
|192.168.10.250|Permitido|
|192.168.11.10|Negado|
|10.1.1.1|Negado|

---

**Quer que eu também gere essa documentação já formatada em PDF, com imagens ilustrando a aplicação da ACL na interface?** 🎯  
Posso mandar pra você baixar se quiser!