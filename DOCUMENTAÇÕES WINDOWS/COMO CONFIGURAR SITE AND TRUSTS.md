

## **1. Configuração Manual pelo Console**

### **Passo 1 – Abrir o Active Directory Sites and Services**

1. No DC (pode ser o do domínio pai ou filho), abra:
    
    - **Server Manager > Tools > Active Directory Sites and Services**.
        

---

### **Passo 2 – Criar os Sites**

1. Clique com o botão direito em **Sites > New Site**.
    
2. Crie o site **WORLDSKILLS** e associe ao **DefaultIPSiteLink**.
    
3. Repita e crie o site **EURO**.
    

---

### **Passo 3 – Configurar as Sub-redes**

1. Clique com o botão direito em **Subnets > New Subnet**:
    
    - Crie **192.168.0.0/24** e associe ao site **WORLDSKILLS**.
        
    - Crie **172.16.0.0/24** e associe ao site **EURO**.
        

---

### **Passo 4 – Mover os Controladores de Domínio**

1. Em **Sites > Default-First-Site-Name > Servers**:
    
    - Localize o **DC (do domínio worldskills.org)** e mova para o site **WORLDSKILLS**.
        
    - Localize o **BRDC (do domínio euro.worldskills.org)** e mova para o site **EURO**.
        
2. Para mover:
    
    - Clique com o botão direito no servidor → **Move** → selecione o site correto.
        

---

### **Passo 5 – Configurar a Replicação Entre Sites**

1. Em **Sites > Inter-Site Transports > IP**, abra **DefaultIPSiteLink**.
    
2. Verifique se ambos os sites (**WORLDSKILLS** e **EURO**) estão listados.
    
    - Se não, adicione.
        
3. Ajuste a **frequência de replicação**:
    
    - Por padrão: **180 minutos (3 horas)**.
        
    - Pode reduzir para **15 minutos** se a rede tiver boa largura de banda.
        

---

### **Passo 6 – Garantir Catálogo Global (GC)**

1. Em cada site, certifique-se de que pelo menos um DC é **GC**:
    
    - Clique com o botão direito no servidor → **Properties**.
        
    - Aba **NTDS Settings** → marque **Global Catalog**.
        

---

### **Passo 7 – Testar e Validar**

- Forçar replicação:
    
    powershell
    
    CopiarEditar
    
    `repadmin /syncall /AdeP`
    
- Verificar o site que cada servidor acha que pertence:
    
    powershell
    
    CopiarEditar
    
    `nltest /dsgetsite`
    
- Checar estado da replicação:
    
    powershell
    
    CopiarEditar
    
    `repadmin /replsummary`