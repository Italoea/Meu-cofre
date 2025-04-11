

---

## ✅ **Resumo dos Tipos de Portas no STP/RSTP**

|**Tipo de Porta**|**Função**|
|---|---|
|**🟩 Porta Designada**|Porta responsável por **encaminhar quadros em um segmento** da rede. Sempre há **uma por segmento**, e ela está no estado **Forwarding**.|
|**🟥 Desativado**|Porta que está **administrativamente desativada** (via configuração) ou com erro físico. Não participa do STP.|
|**🟦 Porta Raiz**|Também chamada de **Root Port (RP)**. É a porta de um switch (que não é a root) com o **melhor caminho até a Root Bridge**. Apenas **uma Root Port por switch**. Está em **Forwarding**.|
|**🟨 Porta Alternativa**|Porta que **fica em espera**, pronta para assumir caso a porta ativa falhe. Estado típico no **RSTP**, equivalente a **Blocking no STP**.|

---

### 📘 Dica:

- **STP clássico (802.1D):** usa os termos Root Port, Designated Port e Blocking.
    
- **RSTP (802.1w):** moderniza e introduz papéis como **Porta Alternativa** e **Backup**, com **convergência mais rápida**.
    

Se quiser, posso montar um **esquema visual com exemplo de rede** pra mostrar cada tipo dessas portas em ação. Deseja isso em PDF com imagens?