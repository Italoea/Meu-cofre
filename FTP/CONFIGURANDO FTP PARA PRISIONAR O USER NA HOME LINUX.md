



## NO SERVIDOR:

```sh
apt install proftpd -y
```

## APÓS ISSO VÁ PARA O ARQUIVO DE CONFIGURAÇÃO DO FTO

#### nano /etc/proftpd/proftpd.conf

### ADICONE ISSO NO ARQUIVO DE CONFIGURAÇÃO:

```
ServerName                      "Nome do server"
DefaultRoot                     ~
UseIPv6                         off
RequireValidShell               on
```

## APÓS ISSO, CRIE UM USUÁRIO

```
adduser joao
```

## CRIE UM GFRUPO:

```
groupadd ftpusers
usermod -aG ftpusers joao
```

## E NO PROFTPD.CONF:

```
<Limit LOGIN>
  DenyAll
  AllowGroup ftpusers
</Limit>
```

## ULTIMO PASSO:
####  REINICIAR O SERVIÇO

```
systemctl restart proftpd
```

## ✅ Teste

- Use um cliente FTP (como FileZilla) ou linha de comando:

```
ftp <IP_DO_SERVIDOR>
```

- Faça login com o usuário criado.
    
- Tente navegar fora da pasta home: deve ser proibido.