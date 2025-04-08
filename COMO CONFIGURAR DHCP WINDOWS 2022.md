
---

# 📘 Documentação: Configuração do Servidor DHCP no Windows Server 2022

## 🎯 Objetivo

Instalar, configurar e ativar o serviço DHCP no Windows Server 2022, permitindo que ele distribua automaticamente endereços IP e configurações de rede para clientes.

---

## 🛠 Pré-requisitos

- Windows Server 2022 instalado e com IP estático.
    
- Conta de usuário com privilégios de administrador.
    
- Interface de rede ativa e funcional.
    
- Acesso ao Server Manager ou PowerShell.
    

---

## 1️⃣ Instalar o DHCP Server

### Usando o Server Manager:

1. Abra o **Server Manager**.
    
2. Vá em **Manage > Add Roles and Features**.
    
3. Clique em **Next** até a tela de seleção de funções.
    
4. Marque **DHCP Server**.
    
5. Clique em **Add Features** quando for solicitado.
    
6. Continue clicando em **Next** até a tela de confirmação.
    
7. Clique em **Install**.
    
8. Aguarde a conclusão e clique em **Close**.
    

### ✅ Após isso, o DHCP estará instalado, mas ainda não configurado.

---

## 2️⃣ Abrir o Console DHCP

1. No Server Manager, vá em **Tools > DHCP**.
    
2. O console do DHCP será aberto, mostrando:
    
    - IPv4
        
    - IPv6
        

---

## 3️⃣ Criar um Escopo DHCP (IPv4)

1. Expanda o nome do servidor > clique com o botão direito em **IPv4** > selecione **New Scope…**.
    
2. No assistente:
    
    - Nome: `LAN`
        
    - Descrição: `Escopo para clientes da rede local`
        
    - IP Range: Ex: de `192.168.10.100` até `192.168.10.200`
        
    - Subnet Mask: Será sugerida, ou defina manualmente.
        
    - Exclusions: (opcional) ex: `192.168.10.150 - 192.168.10.160`
        
    - Lease Duration: Ex: 8 dias (padrão)
        
3. Escolha “Yes, I want to configure these options now”.
    

---

## 4️⃣ Configurar Opções de Escopo

- **Default Gateway (Router):** Ex: `192.168.10.1`
    
- **DNS Server:** IP do servidor DNS (local ou externo)
    
- **Domain Name:** Ex: `exemplo.local` (ou deixe em branco)
    
- **WINS Servers:** (se não usar, deixe em branco)
    
- Clique em **Next** e depois **Finish**.
    

---

## 5️⃣ Ativar o Escopo

1. Clique com o botão direito sobre o escopo recém-criado.
    
2. Selecione **Activate**.
    

---

## 6️⃣ Testar Funcionamento

Em um cliente da rede:

1. Configure a interface de rede para **obter IP automaticamente (DHCP)**.
    
2. Use o comando:
    

```bash
ipconfig /release
ipconfig /renew
ipconfig /all
```

3. Verifique se o cliente obteve IP, gateway e DNS corretamente.
    

---

## 7️⃣ (Opcional) Criar Reservas de IP

1. No console DHCP, expanda o escopo > clique com o botão direito em **Reservations > New Reservation**.
    
2. Preencha os dados:
    
    - Nome: `Printer`
        
    - IP Address: `192.168.10.50`
        
    - MAC Address: `00-11-22-33-44-55`
        
3. Clique em **Add**.
    

---

## 🔄 Reiniciar o Serviço DHCP (se necessário)

```powershell
Restart-Service dhcpserver
```

---

## 📦 Comandos em PowerShell (Instalação e Configuração Básica)

```powershell
# Instalar o DHCP Server
Install-WindowsFeature -Name DHCP -IncludeManagementTools

# Autorizar (caso use AD, senão ignore)
# Add-DhcpServerInDC -DnsName "SERVIDOR" -IpAddress 192.168.10.10

# Criar escopo
Add-DhcpServerv4Scope -Name "LAN" -StartRange 192.168.10.100 -EndRange 192.168.10.200 -SubnetMask 255.255.255.0

# Adicionar opções
Set-DhcpServerv4OptionValue -ScopeId 192.168.10.0 -Router 192.168.10.1 -DnsServer 192.168.10.10 -DnsDomain "exemplo.local"
```

---

## ✅ Conclusão

Com essas etapas, o servidor DHCP estará funcionando no Windows Server 2022, pronto para distribuir IPs aos dispositivos da rede. Essa configuração é ideal para ambientes pequenos ou médios que não exigem integração direta com Active Directory.

Se quiser, posso gerar uma versão PDF ou DOC dessa documentação também. Deseja?