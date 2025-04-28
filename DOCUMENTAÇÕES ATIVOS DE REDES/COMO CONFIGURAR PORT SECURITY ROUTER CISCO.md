
---

# 📄 Resumo: Configurar Port Security em Switch Cisco

## Objetivo

Proteger a porta do switch aceitando apenas o **endereço MAC** do host (`LYON-CLIENT`).  
Se chegar outro MAC, a porta **desliga automaticamente** (shutdown).

---

## 1. Se souber o endereço MAC:

- Configure manualmente o MAC permitido.
    
- Comandos principais:
    
    ```bash
    interface FastEthernet0/10
     switchport mode access
     switchport port-security
     switchport port-security maximum 1
     switchport port-security mac-address [MAC-DO-LYON-CLIENT]
     switchport port-security violation shutdown
    ```
    

---

## 2. Se **não souber** o endereço MAC:

- Use **Port Security Sticky** para aprender o MAC automaticamente.
    
- Comandos principais:
    
    ```bash
    interface FastEthernet0/10
     switchport mode access
     switchport port-security
     switchport port-security maximum 1
     switchport port-security mac-address sticky
     switchport port-security violation shutdown
    ```
    

---

## 3. Verificações

- Ver o MAC aprendido:
    
    ```bash
    show port-security address
    ```
    
- Verificar status da interface:
    
    ```bash
    show port-security interface FastEthernet0/10
    ```
    

---

## 4. Se a porta for desligada (err-disabled)

- Reativar manualmente:
    
    ```bash
    interface FastEthernet0/10
     shutdown
     no shutdown
    ```
    

---

# 📌 Dicas finais:

- Sempre aplicar `switchport mode access` antes de ativar o port security.
    
- Lembrar de salvar a configuração se usar o sticky:
    
    ```bash
    copy running-config startup-config
    ```
    

---
