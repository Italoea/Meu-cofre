

![[Pasted image 20250701085843.png]]


## NO SERVIDOR PRIMARIO EM /etc/bind/named.conf.defalt-zones ADICIONE:

![[Pasted image 20250701090053.png]]


```
allow-transfer {ip do servidor secundario;};
```



## NO SERVIDOR SECUNDARIO EM /etc/bind/named.conf.defalt-zones ADICIONE:

![[Pasted image 20250701090248.png]]

```
masters {ip do servidor primario;};
```

# PARA TESTAR SE O SERVIDOR SECUNDARIO ESTÁ FUNCIONANDO:

## FAÇA NO SERVIDOR SECUNDARIO

```
rndc zonestatus seudominio.local
```

## DEVERÁ VOLTAR

![[Pasted image 20250701090452.png]]
