

---

## 📄 Documentação: Como Criar e Adicionar uma VLAN em Switch Cisco

### 🎯 Objetivo

Criar uma VLAN, atribuir um nome a ela e adicioná-la a uma interface específica do switch.

---

### 🛠️ Pré-requisitos

- Acesso ao console do switch (CLI) via terminal ou telnet/SSH.
    
- Privilegios de modo EXEC privilegiado (`enable`).
    
- Interface de rede identificada para atribuição da VLAN.
    

---

### 🔹 Etapa 1: Acessar o Switch

```bash
Switch> enable
Switch# configure terminal
```

---

### 🔹 Etapa 2: Criar a VLAN

```bash
Switch(config)# vlan 10
Switch(config-vlan)# name VENDAS
Switch(config-vlan)# exit
```

> 💡 Explicação:
> 
> - `vlan 10`: Cria a VLAN de número 10.
>     
> - `name VENDAS`: Dá o nome "VENDAS" à VLAN.
>     

---

### 🔹 Etapa 3: Atribuir a VLAN a uma Interface

```bash
Switch(config)# interface FastEthernet0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
Switch(config-if)# exit
```

> 💡 Explicação:
> 
> - `switchport mode access`: Coloca a interface no modo de acesso.
>     
> - `switchport access vlan 10`: Atribui a VLAN 10 à interface.
>     

---

### 🔹 Etapa 4: (Opcional) Verificar a Configuração

```bash
Switch# show vlan brief
```

> Exemplo de saída esperada:

```
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/2, Fa0/3, ...
10   VENDAS                           active    Fa0/1
```

---

### ✅ Pronto!

A VLAN foi criada e atribuída a uma porta de acesso.

Se quiser, posso complementar com:

- Como criar VLANs em trunk.
    
- Como aplicar isso via Ansible.
    
- Como salvar a configuração (`write memory` ou `copy run start`).
    

Quer que eu coloque tudo isso em um PDF?