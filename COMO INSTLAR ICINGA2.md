

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
mysql> CREATE DATABASE icinga;  
mysql> GRANT ALL PRIVILEGES ON icinga.* TO 'icingauser'@'localhost' IDENTIFIED BY 'icinga';
mysql> FLUSH PRIVILEGES;  
mysql> quit
```

### PARA CONFIGURAR O IDO-MYSQL:
```
apt install icinga2-ido-mysql monitoring-plugins
```
