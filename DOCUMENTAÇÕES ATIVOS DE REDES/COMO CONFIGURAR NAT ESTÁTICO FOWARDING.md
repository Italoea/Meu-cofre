
---

# 📄 **Documentação Técnica: Configuração de NAT com Port Forwarding**

## 1. Introdução

**NAT com Port Forwarding** (Redirecionamento de Portas) permite que dispositivos da Internet acessem serviços em um servidor localizado dentro de uma rede privada (LAN), mapeando uma porta específica do IP público para um IP interno.

Essa configuração é comum para:

- Servidores Web (HTTP/HTTPS)
    
- Servidores FTP
    
- Servidores SSH
    
- Jogos online
    
- Câmeras de segurança
    

---

## 2. Cenário de Exemplo

|Elemento|Endereço IP|Descrição|
|---|---|---|
|Interface WAN (Internet)|200.1.1.1|IP público do roteador|
|Interface LAN (Rede Interna)|192.168.1.1|IP privado do roteador|
|Servidor Interno|192.168.1.100|Servidor Web (porta 80)|

Objetivo: Acessar o servidor interno via Internet utilizando a porta **8080** do IP público.

---

## 3. Configuração Passo a Passo

### 3.1 Definir interfaces NAT "inside" e "outside"

No roteador Cisco:

```bash
conf t
interface GigabitEthernet0/0
 ip address 200.1.1.1 255.255.255.0
 ip nat outside
exit

interface GigabitEthernet0/1
 ip address 192.168.1.1 255.255.255.0
 ip nat inside
exit
```

**Explicação**:

- `ip nat inside` → Marca a interface da rede interna (LAN).
    
- `ip nat outside` → Marca a interface da rede externa (Internet).
    

---

### 3.2 Criar regra de Port Forwarding

```bash
ip nat inside source static tcp 192.168.1.100 80 interface GigabitEthernet0/0 8080
```

**Explicação**:

- `tcp` → Protocolo usado.
    
- `192.168.1.100 80` → IP e porta do servidor interno.
    
- `GigabitEthernet0/0 8080` → Interface pública e porta de acesso externa.
    

---

### 3.3 Verificar a configuração NAT

```bash
show ip nat translations
```

**Saída esperada:**

```
Pro Inside global         Inside local          Outside local         Outside global
tcp 200.1.1.1:8080        192.168.1.100:80       ---                   ---
```

---

## 4. Considerações importantes

- **Firewall:** Certifique-se que a porta (8080) esteja liberada no firewall do roteador.
    
- **Servidor interno:** Deve estar funcionando corretamente no IP e porta indicados.
    
- **Endereço IP:** Se o IP público for dinâmico, considere usar um serviço de DDNS.
    
- **Múltiplos serviços:** Podem ser configuradas várias portas para serviços diferentes.
    

### Exemplo adicional de múltiplas portas:

```bash
ip nat inside source static tcp 192.168.1.100 22 interface GigabitEthernet0/0 2222  # SSH
ip nat inside source static tcp 192.168.1.100 21 interface GigabitEthernet0/0 2121  # FTP
```

---

## 5. Diagnóstico de Problemas (Troubleshooting)

- Verifique a tabela NAT:
    
    ```bash
    show ip nat translations
    ```
    
- Verifique se a interface correta está marcada como `inside` e `outside`.
    
- Verifique se o servidor está ativo e aceitando conexões na porta desejada.
    
- Teste com `telnet` ou `nc` (netcat) para validar a abertura da porta.
    

---

# 📌 Resumo Visual

```plaintext
[Internet]
    ↓
(200.1.1.1:8080)
    ↓
[Roteador Cisco NAT]
    ↓
(192.168.1.100:80)
    ↓
[Servidor Web Interno]
```

---
