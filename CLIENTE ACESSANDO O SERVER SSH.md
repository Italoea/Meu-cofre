
### GERANDO A CHAVE NO CLIENTE:

```
ssh-keygen -b 4096 -t rsa
[fingerprint yes/no] yes
senha
senha
```

### AGORA PARA COPIAR A CHAVE PUBLICA PARA O SERVIDOR

```
ssh-copy-id -i /root/.ssh/id_rsa.pub nomedeusuario@ipdeusuario
```


### COMO DELETAR UM USUÁRIO NO LDAP 

```
ldapdelete -D "cn=admindc=senaidf,dc=com,dc=br" -W "uid=usuario,ou=dousuario,dc=senaidf,dc=com,dc=br"
```
