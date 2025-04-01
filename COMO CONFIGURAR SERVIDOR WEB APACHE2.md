
# Instalação e Configuração do Apache2 na Porta 80

## Requisitos

Antes de começar, certifique-se de que:

- Você tem acesso root ou permissões sudo no sistema.
    
- O sistema está atualizado.
    

## Passos de Instalação

### 1. Atualizar o Sistema

```bash
sudo apt update && sudo apt upgrade -y
```

### 2. Instalar o Apache2

```bash
sudo apt install apache2 -y
```

### 3. Verificar o Status do Apache

```bash
sudo systemctl status apache2
```

Se o Apache não estiver rodando, inicie com:

```bash
sudo systemctl start apache2
```

### 4. Habilitar o Apache para Iniciar Automaticamente

```bash
sudo systemctl enable apache2
```

## Configuração da Porta 80

O Apache usa a porta 80 por padrão. Para garantir que está configurado corretamente:

### 1. Verificar Configuração de Porta

Abra o arquivo de configuração:

```bash
sudo nano /etc/apache2/ports.conf
```

Verifique se a seguinte linha está presente:

```apache
Listen 80
```

Se não estiver, adicione-a.

### 2. Configurar Virtual Host (Opcional)

Edite ou crie um arquivo de Virtual Host:

```bash
sudo nano /etc/apache2/sites-available/000-default.conf
```

Verifique ou modifique a linha:

```apache
<VirtualHost *:80>
    DocumentRoot /var/www/html
</VirtualHost>
```

Salve e saia.

### 3. Reiniciar o Apache

```bash
sudo systemctl restart apache2
```

## Testar o Servidor
```sh
curl (IP_DO_SERVIDOR)
```
Abra um navegador e acesse:

```
http://seu_ip_servidor/
```

Se estiver rodando localmente, use:

```
http://localhost/
```

Se a página padrão do Apache aparecer, a instalação foi bem-sucedida!

## Firewall (Caso Necessário)

Se estiver usando UFW, libere a porta 80:

```bash
sudo ufw allow 80/tcp
sudo ufw reload
```

## Conclusão

O Apache2 foi instalado e configurado para rodar na porta 80. Agora, você pode hospedar seus sites e serviços!