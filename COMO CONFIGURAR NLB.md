
Para configurar o **NLB (Network Load Balancing)** no **Windows Server 2022** pela **interface gráfica (GUI)** e balancear os serviços **HTTP (80), HTTPS/ADFS (443)** nos servidores **SRV1 e SRV2**, siga este passo a passo:

---

### ✅ **Pré-requisitos**

- SRV1 e SRV2 devem:
    
    - Ter IPs fixos na mesma sub-rede.
        
    - Ter o recurso “Network Load Balancing” instalado.
        
    - Estar com as funções Web e ADFS já instaladas e funcionando.
        
    - Ter firewall liberando portas 80 e 443.
        

---

### 🔧 **Passo a passo – GUI**

#### 🧩 1. Instalar o recurso NLB

Em **SRV1 e SRV2**:

1. Abra o **Server Manager**.
    
2. Clique em **"Add Roles and Features"**.
    
3. Vá clicando em **Next** até **"Features"**.
    
4. Marque a opção **"Network Load Balancing"**.
    
5. Conclua a instalação.
    

---

#### 🖥️ 2. Abrir o Gerenciador NLB

Em **SRV1**:

1. Pressione `Windows + R`, digite:
    
    ```
    nlbmgr.msc
    ```
    
    ou pesquise **"Network Load Balancing Manager"** no menu iniciar.
    

---

#### 📦 3. Criar novo Cluster

1. No menu **"Network Load Balancing Manager"**, clique com o **botão direito em “Network Load Balancing Clusters” > New Cluster**.
    
2. Em **"Host"**, digite o nome ou IP de **SRV1** e clique em **Connect**.
    
3. Selecione a interface de rede usada no NLB (geralmente a principal) e clique em **Next**.
    
4. Em **"Host Parameters"**, deixe:
    
    - **Priority (Unique Host ID):** 1 para SRV1.
        
    - Marque **"Started"**.
        
    - Clique em **Next**.
        

---

#### 🌐 4. Definir o IP Virtual (Cluster IP)

1. Clique em **"Add"** e adicione o IP:
    
    ```
    192.168.0.50
    ```
    
2. Subnet mask: (exemplo) `255.255.255.0`
    
3. Clique em **OK** e depois **Next**.
    

---

#### 🔤 5. Nome do Cluster e Modo de Operação

1. Em **"Full Internet Name"**, digite:
    
    ```
    SRV
    ```
    
2. **Cluster operation mode:** deixe como **Unicast** (ou Multicast, se seu ambiente exigir).
    
3. Clique em **Next**.
    

---

#### 🔁 6. Regras de Portas (Port Rules)

1. Apague a regra padrão (`All Ports`).
    
2. Clique em **Add** três vezes para adicionar as seguintes regras:
    

|Start Port|End Port|Protocols|
|---|---|---|
|80|80|TCP|
|443|443|TCP|

> Ambas podem ser configuradas com:

- Filtering mode: **Multiple host**
    
- Affinity: **Single** (para sessões persistentes em ADFS) ou **None** (para web puro)
    

3. Clique em **Finish**.
    

---

#### ➕ 7. Adicionar SRV2 ao Cluster

1. Clique com o botão direito no cluster **SRV** > **Add Host to Cluster**.
    
2. Digite o nome de **SRV2** > **Connect**.
    
3. Selecione a interface de rede > **Next**.
    
4. Defina:
    
    - Priority: **2**
        
    - Status: **Started**
        
    - Clique em **Next > Finish**.
        

---

### ✅ Verificações Finais

- Verifique se o cluster está online.
    
- Teste acesso ao IP virtual `192.168.0.50` via HTTP e HTTPS.
    
- Use `nlb.exe` ou `Get-NlbCluster` no PowerShell para verificação avançada.
    

---

Se quiser, posso gerar esse passo a passo em PDF com imagens. Deseja isso?