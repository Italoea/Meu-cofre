
---

# 📄 Diferença entre ACL Padrão e ACL Estendida (Cisco)

---

|Característica|ACL Padrão|ACL Estendida|
|---|---|---|
|**Filtra por**|Somente IP de origem|IP de origem, IP de destino, protocolo, portas TCP/UDP|
|**Nível de controle**|Simples (básico)|Avançado (específico)|
|**Onde aplicar**|Perto do destino|Perto da origem|
|**Número de ACL**|1–99 (antigo) / 1300–1999 (novo)|100–199 (antigo) / 2000–2699 (novo)|
|**Exemplos de uso**|Bloquear ou permitir uma rede inteira|Permitir tráfego HTTP, bloquear FTP, liberar ICMP, etc|
|**Configuração**|Mais simples, menos parâmetros|Mais detalhada, vários parâmetros|
|**Comando principal**|`access-list [número] permit/deny [origem]`|`access-list [número] permit/deny [protocolo] [origem] [destino] [porta]`|

---

## 📘 Resumo rápido:

- **ACL Padrão**: Só vê **quem envia** (IP de origem).
    
- **ACL Estendida**: Vê **quem envia**, **quem recebe**, **o que está sendo enviado** (tipo de tráfego) e **qual serviço/porta**.
    

---

## 🛠 Exemplos Práticos

### ACL Padrão

Permitir a rede `192.168.1.0/24`:

```bash
access-list 10 permit 192.168.1.0 0.0.0.255
```

### ACL Estendida

Permitir tráfego HTTP (porta 80) da rede `192.168.1.0/24` para `10.0.0.0/8`:

```bash
access-list 110 permit tcp 192.168.1.0 0.0.0.255 10.0.0.0 0.255.255.255 eq 80
```

Aqui:

- `tcp` = protocolo.
    
- `192.168.1.0 0.0.0.255` = IP de origem.
    
- `10.0.0.0 0.255.255.255` = IP de destino.
    
- `eq 80` = porta HTTP.
    

---

## 🎯 Quando usar cada uma?

|Quando usar ACL Padrão|Quando usar ACL Estendida|
|---|---|
|Controle simples baseado apenas no IP de quem está enviando.|Controle avançado: IP de origem, destino, protocolo e portas específicas.|
|Quando não importa qual serviço está sendo acessado.|Quando você precisa permitir ou bloquear serviços específicos (ex: HTTP, FTP, SSH).|

---

# 📚 Conclusão

- Use **ACL Padrão** para filtros rápidos e simples.
    
- Use **ACL Estendida** para controle detalhado sobre o tráfego de rede.
    
- Lembre-se de aplicar a ACL no local correto:
    
    - ACL Padrão → Perto do destino.
        
    - ACL Estendida → Perto da origem.
        

---
