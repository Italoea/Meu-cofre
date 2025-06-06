

## PARA BAIXAR O APACHE2 NO SERVIDOR:

```
apt install apache2
```

## PARAR TESTAR SE O APACHE ESTÁ FUNCIONAL:

```
curl (ip do meu servidor)
```

## PARA ACESSAR O ARQUIVO DE CONVIGURAÇÃO DE VIRTUAL HOST:

```
nano /etc/apache2/sites-available/00-default.conf

<VirtualHost (meusite.com):80>
    DocumentRoot /var/www/virtual.host
    ServerName (meusite)
    ServerAdmin webmaster@virtual.host
    ErrorLog /var/log/apache2/virtual.host.error.log
    CustomLog /var/log/apache2/virtual.host.access.log combined
</VirtualHost>



  #DocumentRoot /var/www/virtual.host aonde vai ficar meu arquivo index.html que lá que vou inserir o que deve aparecer quando o usuario solicitar essa página.

 #ServerName www.virtual.host meu site

#ServerAdmin webmaster@virtual.host Email do adm
#
```


## CONFIGURANDO O ARQUIVO INDEX.HTML:

```
nano /var/www/virtual.host/index.html

<html>
<body>
<div style="width: 100%; font-size: 40px; font-weight: bold; text-align: center;">
Virtual Host Test Page
</div>
</body>
</html>
```



## PARA ATIVAR O VIRTUAL HOST:

```
a2ensite virtual.host
```