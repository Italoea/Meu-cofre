![[Captura de tela 2025-07-02 105717 1.png]]

### NESSA TOPOLOGIA EU CONFIGUREI O EIGRP NO R14 E NO R15

### NO R15 CONFIGUREI ANUNCIANDO AS REDES:

```
R15(config)#router eirgp 1
R15(config)#network 172.10.0.0
R15(config)#network 172.20.0.0
R15(config)#network 172.30.0.0
R15(config)#network 210.103.5.0

#Caso precise dê o comando no auto summary
```

### JÁ NO R14 CONFIGUREI ANUNCIANDO AS REDES:

```
R14(config)#network 210.103.5.0
R14(config)#network 192.168.17.0
```


### NA INTERFACE E0/0 DO R15 CONFIGUREI A SUMARIZAÇÃO DAS REDES 172:

```
 R15(config)# ip summary-address eigrp 1 172.0.0.0 255.224.0.0
```

### A CONFIGURAÇÃO DA SUMARIZAÇÃO SEMPRE DEVE SERFEITA NA INTERFACE DE SAIDA.