
# Documentação sobre a Configuração do BIND9

## Introdução

O **BIND9** (Berkeley Internet Name Domain) é um dos servidores DNS mais utilizados. Ele permite a resolução de nomes de domínios para endereços IP, garantindo a comunicação entre dispositivos na rede.

A configuração do BIND9 envolve vários arquivos principais, sendo os mais importantes:

- `/etc/bind/named.conf`
    
- `/etc/bind/named.conf.options`
    
- `/etc/bind/named.conf.local`
    
- `/etc/bind/named.conf.default-zones`
    
- Arquivos de zona (exemplo: `/etc/bind/db.example.com`)
    

A seguir, detalharemos cada um desses arquivos e suas configurações.

---

## 1. **Arquivo named.conf**

Este é o arquivo principal de configuração do BIND9. Ele inclui outros arquivos de configuração para modularidade. Um exemplo básico deste arquivo:

```bash
include "/etc/bind/named.conf.options";
include "/etc/bind/named.conf.local";
include "/etc/bind/named.conf.default-zones";
```

Cada uma dessas inclusões referencia arquivos adicionais que configuram o funcionamento do servidor DNS.

---

## 2. **Arquivo named.conf.options**

Define opções globais do servidor DNS, como endereços de escuta, encaminhadores e segurança. Um exemplo:

```bash
options {
    directory "/var/cache/bind"; # Diretório onde ficam armazenados os arquivos de cache e zonas
    
    dnssec-validation auto; # Habilita a validação DNSSEC
    
    listen-on port 53 { 127.0.0.1; 192.168.1.1; }; # Define interfaces para escuta
    allow-query { any; }; # Permite consultas de qualquer origem
    
    forwarders {
        8.8.8.8;
        8.8.4.4;
    };
};
```

- **directory**: Define o diretório padrão dos arquivos do BIND.
    
- **dnssec-validation auto**: Habilita a validação de segurança DNSSEC.
    
- **listen-on port 53**: Especifica em quais IPs o BIND deve escutar.
    
- **allow-query**: Define quem pode consultar o DNS.
    
- **forwarders**: Configura servidores DNS externos para resolver consultas não locais.
    

---

## 3. **Arquivo named.conf.local**

Configura zonas adicionais (autoridade sobre determinados domínios). Exemplo de configuração para um domínio local:

```bash
zone "example.com" {
    type master;
    file "/etc/bind/db.example.com";
};

zone "1.168.192.in-addr.arpa" {
    type master;
    file "/etc/bind/db.192";
};
```

- **zone "example.com"**: Define a configuração para um domínio.
    
- **type master**: Indica que este servidor é o primário da zona.
    
- **file "/etc/bind/db.example.com"**: Aponta para o arquivo de configuração da zona.
    
- **zone "1.168.192.in-addr.arpa"**: Configuração para resolução reversa.
    

---

## 4. **Arquivo named.conf.default-zones**

Contém as zonas padrão usadas pelo BIND, como `localhost`, `127.0.0.1` e `0.0.127.in-addr.arpa`. É recomendável não modificar esse arquivo a menos que seja necessário.

Exemplo:

```bash
zone "localhost" {
    type master;
    file "/etc/bind/db.local";
};

zone "127.in-addr.arpa" {
    type master;
    file "/etc/bind/db.127";
};
```

---

## 5. **Arquivo de Zona (db.example.com)**

Define os registros DNS para um domínio específico. Exemplo:

```bash
$TTL 86400
@   IN  SOA ns1.example.com. admin.example.com. (
        2025040101 ; Serial
        3600       ; Refresh
        1800       ; Retry
        604800     ; Expire
        86400      ; Minimum TTL
    )

@       IN  NS      ns1.example.com.
@       IN  A       192.168.1.100
www     IN  A       192.168.1.100
mail    IN  A       192.168.1.101
@       IN  MX 10   mail.example.com.
```

- **$TTL 86400**: Define o tempo padrão de vida dos registros (Time To Live).
    
- **SOA (Start of Authority)**: Define informações sobre a zona, como:
    
    - **ns1.example.com.**: Servidor DNS primário.
        
    - **admin.example.com.**: Email do administrador (substituir `@` por `.`).
        
    - **Serial**: Versão da zona (deve ser incrementado a cada mudança).
        
    - **Refresh, Retry, Expire, Minimum TTL**: Parâmetros para servidores secundários.
        
- **NS (Name Server)**: Define o servidor de nomes.
    
- **A (Address Record)**: Associa um nome de domínio a um IP.
    
- **MX (Mail Exchange)**: Define o servidor de email do domínio.
    

---

## 6. **Modelo de Arquivo de Zona**

O BIND9 fornece modelos de arquivos de zona que podem ser usados como base para novas configurações. Eles estão localizados em:

```bash
/usr/share/bind/db.local
/usr/share/bind/db.127
```

Para criar um novo arquivo de zona, basta copiar um desses modelos:

```bash
sudo cp /usr/share/bind/db.local /etc/bind/db.example.com
```

E então editá-lo conforme as necessidades do seu domínio.

---

## Conclusão

O BIND9 é altamente configurável e permite desde a resolução de nomes locais até implementações complexas para grandes redes. Compreender seus arquivos de configuração é essencial para garantir um DNS eficiente e seguro.

Para validar sua configuração, utilize os comandos:

```bash
sudo named-checkconf   # Verifica erros na configuração
sudo named-checkzone example.com /etc/bind/db.example.com  # Verifica erros na zona
sudo systemctl restart bind9  # Reinicia o serviço
```

Caso tenha dúvidas, consulte a documentação oficial do BIND9 ou utilize `man named` para mais informações.