
---

## 📄 Documentação: Como Configurar o Modo Trunk em um Switch Cisco

### 🎯 Objetivo

Configurar uma interface de switch para operar em modo **trunk**, permitindo a passagem de múltiplas VLANs por um único link.

---

### 🛠️ Pré-requisitos

- Dois switches conectados entre si.
    
- Acesso ao CLI de pelo menos um dos switches.
    
- VLANs já criadas (ou serão propagadas via VTP, se habilitado).
    
- Privilegios de modo EXEC privilegiado (`enable`).
    

---

### 🔹 Etapa 1: Acessar o Switch

```bash
Switch> enable
Switch# configure terminal
```

---

### 🔹 Etapa 2: Entrar na Interface que será Trunk

```bash
Switch(config)# interface FastEthernet0/24
```

---

### 🔹 Etapa 3: Configurar o Modo Trunk

```bash
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk encapsulation dot1q
```

> ⚠️ **Atenção**:
> 
> - Alguns switches mais modernos já utilizam somente **802.1Q (dot1q)** e não aceitam `isl`.
>     
> - Em switches que não suportam encapsulamento configurável, o comando `switchport trunk encapsulation dot1q` pode não ser necessário.
>     

---

### 🔹 Etapa 4: (Opcional) Permitir VLANs Específicas no Trunk

```bash
Switch(config-if)# switchport trunk allowed vlan 10,20,30
```

> 💡 Isso restringe o trunk para passar apenas as VLANs 10, 20 e 30.

---

### 🔹 Etapa 5: (Opcional) Definir VLAN Nativa

```bash
Switch(config-if)# switchport trunk native vlan 99
```

> A VLAN nativa é a usada para quadros **sem tag VLAN**.

---

### 🔹 Etapa 6: Sair e Salvar Configuração

```bash
Switch(config-if)# exit
Switch(config)# end
Switch# write memory
```

---

### 🔍 Etapa 7: Verificação

```bash
Switch# show interfaces trunk
```

> Exemplo de saída:

```
Port        Mode         Encapsulation  Status        Native vlan
Fa0/24      on           802.1q         trunking      99

Port        Vlans allowed on trunk
Fa0/24      10,20,30

Port        Vlans in spanning tree forwarding state and not pruned
Fa0/24      10,20,30
```

---

### ✅ Pronto!

Agora a interface está configurada como **trunk**, permitindo o tráfego de múltiplas VLANs.

Se quiser, posso montar essa documentação em PDF também. Deseja isso? E quer um exemplo prático com dois switches no EVE-NG?