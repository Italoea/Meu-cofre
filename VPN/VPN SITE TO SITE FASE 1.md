
![[Pasted image 20250522144100.png]]



### APÓS CONFIGURAR AS INTERFACES COM OS DEVIDOS IPS

# PRIMEIRA PARTE: CRIAR UMA POLITICA E UMA CHAVE USANDO ISAKMP (FASE 1)

##### CONFIGUREI ROTAS PADRÃO NOS DEVIDOS ROTADORES
#### EM R1:

```
R1(config)# ip route 0.0.0.0 0.0.0.0 200.165.100.2
```

#### EM R3:

```
R3(config)# ip route 0.0.0.0 0.0.0.0 200.165.200.2
```


##### CONFIGUREI ACLs 
#### EM R1

```
R1(config)# access-list 100 permit ip 192.168.10.0 0.0.0.255 192.168.30.0 0.0.0.255 

#PARA PERMITIR QUALQUER IP DA REDE 192.168.10.0 POSSA ACESSAR QUALQUER IP DA REDE 192.168.30.0
```

#### EM R3:

```
R3(config)# access-list 100 permit ip 192.168.30.0 0.0.0.255 192.168.10.0 0.0.0.255

#PARA PERMITIR QUALQUER IP DA REDE 192.168.30.0 POSSA ACESSAR QUALQUER IP DA REDE 192.168.10.0
```


#### R1:

##### SIGA SEMPRE A ORDEM DOS COMANDOS CITADOS ABAIXO:

```
R1(config)# crypto isakmp policy 10

#Cria a política ISAKMP número 10 (quanto menor o número, maior a prioridade).
```

```
R1(config-isakmp)# encryption aes 256

#Define o algoritmo de criptografia como AES com chave de 256 bits, garantindo segurança na troca de chaves.
```

```
R1(config-isakmp)# authentication pre-share

#Define que a autenticação será feita via chave pré-compartilhada (pre-shared key).
```

```
R1(config-isakmp)# group 5

#Define o grupo de **Diffie-Hellman 5 (1536 bits), que é usado para gerar a chave compartilhada de forma segura durante a negociação.
```

#### FAÇA A MESMA COISA NO R3!!

##### LOGO EM SEGUIDA EM R1:

```
R1(config)# crypto isakmp key secretkey address 200.165.200.1

#"Use a chave secreta 'secretkey' para autenticar com o peer que tem o IP 200.165.200.1."
```

##### EM R3:

```
R3(config)#crypto isakmp key secretkey address 200.165.100.1

"Use a chave secreta 'secretkey' para autenticar com o peer que tem o IP 200.165.100.1."
```

# FIM DA FASE 1, AGORA VÁ PARA A FASE [[VPN SITE TO SITE FASE 2]]




