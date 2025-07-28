
## APÓS CONFIGURAR NO SERVER QUE TEM INTERFACE VÁ PARA O SERVER CORE E DÊ OS COMANDOS:


```
iSCSIcpl.exe
```

#### IRÁ ABRIR ESSA TELA, COLOQUE O IP DO SEU SERVER TARGET

![[Pasted image 20250725115521.png]]


#### APÓS ATIVAR O DISCO, DÊ O COMANDO:

```
diskpart
```
##### IRÁ ABRIR UM TERMINAL OUTRO TERMINAL COM O NOME:

```
DISKPART>
```


#### DÊ O COMANDO:

```
list disk 
```
##### PARA LISTAR OS DISCOS DISPONIVEIS


#### AGORA SELECIONE UM DISCO COM O COMANDO:

```
select disk (numero do disco)

select disk 1
```

#### PARA DEIXAR O DISCO ONLINE DÊ O COMANDO:

```
online disk
```


# DISCO CRIADO CRIADO COM SUCESSO!!


###### PARA CONFERIR AS PARTIÇÕES:

```
list partition
```

###### PARA LISTAR OS VOLUMES:

```
list volume
```

