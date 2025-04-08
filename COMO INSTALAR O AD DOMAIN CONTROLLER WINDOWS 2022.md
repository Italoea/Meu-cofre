
---

## 📄 Documentação: Instalação do Active Directory Domain Controller no Windows Server 2022

### 🎯 Objetivo

Instalar e configurar o serviço **Active Directory Domain Services (AD DS)** para promover o servidor como **Controlador de Domínio (DC)** em um novo domínio.

---

### 🛠️ Pré-requisitos

- Sistema: Windows Server 2022 (instalado e atualizado).
    
- Nome do servidor configurado corretamente (ex: `AD-SERVER`).
    
- IP fixo configurado.
    
- Senha de Administrador definida.
    
- Interface gráfica (Desktop Experience) instalada.
    
- (Opcional) DNS já configurado ou será instalado com o AD.
    

---

## 📌 Parte 1: Renomear o Servidor (opcional, mas recomendado)

```powershell
Rename-Computer -NewName "AD-SERVER" -Restart
```

---

## 📌 Parte 2: Configurar IP Fixo (se ainda não estiver configurado)

1. Vá em **Painel de Controle > Central de Rede > Alterar configurações do adaptador**.
    
2. Clique com o botão direito na interface de rede > **Propriedades**.
    
3. Selecione **Protocolo TCP/IPv4** > clique em **Propriedades**.
    
4. Configure:
    
    - IP: 192.168.0.10 (exemplo)
        
    - Máscara: 255.255.255.0
        
    - Gateway: 192.168.0.1
        
    - DNS Preferencial: 127.0.0.1 ou o IP do próprio servidor.
        

---

## 📌 Parte 3: Instalar o AD DS

### 🔹 Via Server Manager (Interface Gráfica)

1. Abra o **Gerenciador do Servidor (Server Manager)**.
    
2. Clique em **"Adicionar funções e recursos"**.
    
3. Clique em **Avançar** até a tela de **Funções**.
    
4. Marque **Active Directory Domain Services**.
    
5. Aceite as dependências que forem solicitadas.
    
6. Clique em **Avançar** até o final e depois em **Instalar**.
    
7. Aguarde a conclusão da instalação (não reinicie ainda).
    

---

## 📌 Parte 4: Promover o Servidor a Controlador de Domínio

1. Após a instalação, clique em **"Promover este servidor a um controlador de domínio"**.
    
2. Escolha a opção **"Adicionar uma nova floresta"**.
    
    - Nome do domínio raiz: `exemplo.local` (pode ser outro).
        
3. Clique em **Avançar** e configure:
    
    - Nível funcional da floresta e domínio: `Windows Server 2022`.
        
    - Marque **Servidor DNS**.
        
    - Defina a **senha de modo de restauração dos serviços de diretório (DSRM)**.
        
4. Clique em **Avançar** nas etapas seguintes (replicação, DNS, caminho dos arquivos).
    
5. Revise o resumo e clique em **Instalar**.
    
6. O servidor será reiniciado automaticamente.
    

---

## 📌 Parte 5: Verificar a Instalação

Após o reboot:

- Faça login como `Administrador@exemplo.local`.
    
- Verifique no **Server Manager** que o serviço AD DS está em execução.
    
- Teste com o comando:
    

```powershell
Get-ADDomain
Get-ADForest
```

---

Perfeito! Vamos continuar a documentação com as duas próximas etapas:

---

## 📥 Parte 6: Adicionar Estações de Trabalho ao Domínio

### 🎯 Objetivo

Vincular computadores clientes ao domínio criado, para que possam autenticar usuários e aplicar políticas de grupo (GPOs).

---

### 🛠️ Pré-requisitos na estação cliente:

- Windows (10, 11, ou Server).
    
- IP fixo ou DHCP que aponte para o **DNS do controlador de domínio** (ex: 192.168.0.10).
    
- Conectividade de rede com o DC.
    

---

### 🔹 Passos para adicionar ao domínio:

1. Vá em **Painel de Controle > Sistema > Configurações avançadas do sistema**.
    
2. Clique em **Nome do computador > Alterar**.
    
3. Em **Membro de**, selecione **Domínio**.
    
4. Digite o nome do domínio (ex: `exemplo.local`).
    
5. Clique em **OK**.
    
6. Insira um usuário com permissão no domínio (ex: `Administrador`).
    
7. Reinicie o computador.
    

---

### ✅ Verificação:

Após reiniciar:

- Faça login com um usuário do domínio (`EXEMPLO\usuario`).
    
- Verifique se a estação aparece no AD:  
    `Ferramentas > Active Directory Users and Computers > Computers`.
    

---

## 🌐 Parte 7: Configurar Zonas DNS

> ⚠️ Normalmente, ao instalar o AD DS, o DNS já é configurado automaticamente. Porém, você pode criar ou editar zonas conforme necessário.

### 🔹 Acessar o Gerenciador DNS:

1. Abra o **Server Manager**.
    
2. Vá em **Ferramentas > DNS**.
    

---

### 🔹 Verificar Zona de Pesquisa Direta (Forward Lookup Zone)

- A zona com nome do domínio (ex: `exemplo.local`) já estará criada.
    
- Clique nela e veja os registros **A** (hosts), **NS**, **SRV**, etc.
    

---

### 🔹 Criar novos registros DNS:

1. Clique com o botão direito na zona > **Novo Host (A ou AAAA)**.
    
2. Insira:
    
    - Nome: `pc01`
        
    - IP: `192.168.0.50`
        
3. Clique em **Adicionar Host**.
    

---

### 🔹 Criar Zona de Pesquisa Reversa (opcional):

1. Clique com botão direito em **Reverse Lookup Zones > Nova Zona**.
    
2. Configure conforme a sub-rede (ex: `192.168.0.x`).
    
3. Isso permite fazer **resolução reversa** (IP → nome).
    

---

## 🛡️ Parte 8: Criar e Aplicar GPOs (Políticas de Grupo)

### 🎯 Objetivo

Aplicar políticas administrativas centralizadas para usuários e computadores do domínio.

---

### 🔹 Acessar o Editor de GPO:

1. No Controlador de Domínio:  
    **Ferramentas > Group Policy Management**.
    

---

### 🔹 Criar uma nova GPO:

1. Clique com o botão direito no domínio (ex: `exemplo.local`) > **Criar uma GPO neste domínio e vinculá-la aqui**.
    
2. Dê um nome, ex: `Desabilitar Painel de Controle`.
    

---

### 🔹 Editar a GPO:

1. Clique com o botão direito na GPO > **Editar**.
    
2. Vá em:
    
    - **Configuração do Usuário > Políticas > Modelos Administrativos > Painel de Controle**
        
3. Habilite: **Proibir acesso ao Painel de Controle e Configurações do Computador**.
    

---

### 🔹 Aplicar a GPO:

- A GPO já estará vinculada à raiz do domínio.
    
- Pode-se também vincular a **OUs específicas** com computadores ou usuários.
    

---

### 🔹 Forçar atualização de GPO:

Nos clientes, use:

```cmd
gpupdate /force
```

---

### ✅ Verificação:

- Faça login como um usuário de domínio e tente acessar o recurso afetado pela GPO (ex: Painel de Controle).
    
- Use o comando:
    

```powershell
gpresult /r
```

para ver as políticas aplicadas.

---

