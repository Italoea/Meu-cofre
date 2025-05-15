


![[Pasted image 20250515100136.png]]


## APÓS CONFIGURAR OS DEVIDOS IPS EM CADA INTERFACE CONFIGOUREI A ACL, COM AS DEVIDAS PRETENÇÕES:

	PC 1 PODE PINGAR O PC3
	PC 2 NÃO PODE PINGAR O PC3

## NO R1 CONFIGUREI A ACL:

```sh
Router(config)# access-list 1 permit host 192.168.10.10 # para permitir o host 192.168.10.10
Router(config)# access-list 1 deny host 192.168.20.10 # para negar o host 192.168.20.10
```

## PARA ADICONAR A INTERFACE NA ACL:

```Sh
Router(config)#interface e0/2
Router(config)# ip access-group 1 out <-- para ser a porta de saida
```



![[Pasted image 20250515102702.png]]