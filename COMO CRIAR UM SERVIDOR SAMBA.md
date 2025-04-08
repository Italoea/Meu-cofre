


---

## 📄 Documentação: Instalação e Configuração de um Servidor Samba no Linux

### 📌 Pré-requisitos

- Distribuição Linux instalada (Ubuntu/Debian ou CentOS/RHEL).
    
- Acesso root ou usuário com privilégios `sudo`.
    

---

### 🔧 Etapa 1: Instalar o Samba

#### Para sistemas Debian/Ubuntu:

```bash
sudo apt update
sudo apt install samba -y
```

#### Para sistemas CentOS/RHEL:

```bash
sudo dnf install samba samba-client samba-common -y
```

---

### 🛠 Etapa 2: Criar diretório compartilhado

Crie o diretório que será compartilhado:

```bash
sudo mkdir /srv/samba/compartilhado
sudo chmod -R 777 /srv/samba/compartilhado

```

---

### ✏️ Etapa 3: Configurar o Samba

Backup do arquivo de configuração original:

```bash
sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.bak
```

Editar o arquivo de configuração:

```bash
sudo nano /etc/samba/smb.conf
```

Adicione ao final do arquivo:

```ini
[compartilhado]
   path = /srv/samba/compartilhado
   browseable = yes
   read only = no
   guest ok = yes
```

Salve e feche o arquivo.

---

### 🔁 Etapa 4: Reiniciar o serviço Samba

```bash
sudo systemctl restart smbd
sudo systemctl enable smbd
```

---

### 🔓 Etapa 5: Abrir portas no firewall (se aplicável)

#### Para firewalld:

```bash
sudo firewall-cmd --permanent --zone=public --add-service=samba
sudo firewall-cmd --reload
```

#### Para UFW (Ubuntu):

```bash
sudo ufw allow 'Samba'
```

---

### 👥 Etapa 6 (Opcional): Criar usuário Samba com autenticação

Se quiser acesso com usuário/senha:

1. Crie o usuário no sistema (se necessário):
    

```bash
sudo adduser usuarioftp
```

2. Adicione ao Samba:
    

```bash
sudo smbpasswd -a usuarioftp
```

3. Altere a permissão da pasta:
    

```bash
sudo chown -R usuarioftp:usuarioftp /srv/samba/compartilhado
```

4. Atualize a configuração no `smb.conf`:
    

```ini
[compartilhado]
   path = /srv/samba/compartilhado
   valid users = usuarioftp
   read only = no
```

---

### ✅ Etapa 7: Testar a configuração

Verifique se está tudo certo:

```bash
testparm
```

---

### 🖥 Acesso via Windows

1. Pressione `Win + R` e digite:
    

```
\\IP_DO_SERVIDOR\compartilhado
```

2. Se for com autenticação, digite o usuário e senha Samba.
    

---
# PARA CRIAR USUARIOS NO WINDOWS 11 BASTA SEGUIR OS PASSOS ABAIXO:

- # 1 VÁ NO PAINEL DE CONTROLE
- # 2 CLIQUE EM:
![[Pasted image 20250407171159.png]]

- # 3 VÁ EM "GERENCIAR OUTRA CONTA"

- # 4 LOGO APÓS CLIQUE EM "ADICIOAR UM NOVO USUÁRIO NAS CONFIGURAÇÕES DO COMPUTADOR"

- # 5 CLICA EM "ADICIONAR CONTA"

- # 6 E LÁ ADICIONE O USUÁRIO E A SENHA

