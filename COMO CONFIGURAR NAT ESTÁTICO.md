
### O QUE É O NAT ESTÁTICO?

O **NAT Estático** faz a tradução de **um IP privado para um IP público fixo**, de forma permanente.  
➡️ Sempre que o dispositivo interno se comunica, usa o **mesmo IP público**.


![[Pasted image 20250521115102.png]]

### PARA FAZER ESSA CONFIGURAÇÃO ENDERECEI TODOS OS HOSTS EM SUAS DEVIDAS REDES E AS INTERFCES DO ROTEADOR.

### NO R1:

```c
R1(config)# ip nat inside source static 192.168.10.10 209.165.201.5
R1(config)# int e0/0 
R1(config)# ip nat inside
R1(config)# int e0/1 
R1(config)# ip nat outside
```


### ORIGEM DO IP PARA O IP PUBLICO:

```
ip nat inside source static 192.168.10.10 209.165.201.5
```


### INTERFACE INSIDE SEMPRE VAI  SER A INTERFACE DA REDE PRIVADA

```C
R1(config)# int e0/0 
R1(config)# ip nat inside
```

### INTERFACE OUTSIDE SEMPRE VAI SER A INTERFACE DA REDE PUBLICA

```c
R1(config)# int e0/1 
R1(config)# ip nat outside
```

## SENDO ASSIM O IP 192.168.10.10 SERÁ TRADUZIDO PARA O 209.165.201.5

#### VOCE PODE ACOMPANHAR DANDO O COMANDO 

```c
ip nat translations
```