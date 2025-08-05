

### PARA ATUALIZAR
```
apt update && upgrade
```

### PARA INSTALAR O BANCO DE DADOS:
```
apt install mariadb-server
```

### PARA INSTALAR O icinga2 E SUAS DEPENDÊNCIAS:
```
apt install icinga2 icingaweb2 icingacli
```

### PARA CONFIGURAR O BANCO DE DADOS:
```
mariadb -u root  
mariadb> CREATE DATABASE icingaweb2;  
mariadb> GRANT ALL PRIVILEGES ON icingaweb2.* TO 'icingauser'@'localhost' IDENTIFIED BY 'P@ssw0rd';
mariadb> FLUSH PRIVILEGES;  
mariadb> quit
```

### PARA CONFIGURAR O IDO-MYSQL:
```
apt install icinga2-ido-mysql monitoring-plugins
```

![[Pasted image 20250805085643.png]]

![[Pasted image 20250805085738.png]]
###### APÓS A INSTALAÇÃO DO icinga2-ido-mysql ele irá criar uma base de dados com o nome icinga2, para dar a permissão para o usuário é só dar os mesmos comandos que foi dado para criar a base de dados mas mudando somente o nome como está abaixo:
```
mariadb -u root  
mariadb> GRANT ALL PRIVILEGES ON icinga2.* TO 'icingauser'@'localhost' IDENTIFIED BY 'P@ssw0rd';
mariadb> FLUSH PRIVILEGES;  
mariadb> quit
```

### PARA ATIVAR O ido-mysql:
```
icinga2 feature enable ido-mysql
```
###### APÓS ISSO RESTARTE O SERVIÇO:
```
systemctl restart icinga2
```

### AGORA VÁ PARA O NAVEGADOR E DIGITE:
```
seuip/icingaweb2
```

### AGORA GERE O TOKEN PARA AUTENTICAR NA INTERFACE WEB:

```
icingacli setup token create
```


# APÓS TER SEGUIDO ESSE PASSO A PASSO A CONFIGURAÇÃO AGORA É SOMENTE NA INTERFACE WEB


![[Pasted image 20250805090145.png]]

___

![[Pasted image 20250805090220.png]]

---

![[Pasted image 20250805090255.png]]

---
##### ADICONE O BANCO icingaweb2 que criamos com o usuario icingauser e a senha P@ssword, PARA VALIDAR SE ESTÁ FUNCIONANDO CLIQUE EM Validate configuration se ficar verdinho lá em cima está certo
![[Pasted image 20250805090441.png]]


---

![[Pasted image 20250805090759.png]]

---
##### CRIE UMA CONTA DE ADMINISTRADOR:
![[Pasted image 20250805090942.png]]

---
![[Pasted image 20250805091040.png]]

---
##### SELECIONE O BANCO DE DADOS icinga2 que o ido-mysql CRIA AUTOMÉTICAMENTE E o USUARIO icingauser E A SENHA QUE FOI CRIADO E VALIDE TUDO:
![[Pasted image 20250805091443.png]]

---

##### AGORA SELECIONE local command File:

![[Pasted image 20250805091809.png]]

# AGORA É SÓ NEXT E NEXT!!