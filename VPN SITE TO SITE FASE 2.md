
![[Pasted image 20250522144100.png]]


#### EM R1:

```
R1(config)# ipsec transform-set R1-R3 esp-aes 256 esp-sha-hmac

#Defina que no túnel IPsec os dados serão criptografados com AES 256 e autenticados com SHA (HMAC).
```

#### EM R3:

```
R3(config)# ipsec transform-set R3-R1 esp-aes 256 esp-sha-hmac

#Defina que no túnel IPsec os dados serão criptografados com AES 256 e autenticados com SHA (HMAC).
```

#### EM R1:

```
R1(config)# crypto map IPSEC-MAP 10 ipsec-isakmp

# Cria um crypto map chamado `IPSEC-MAP`, sequência 10, que usa IPSec com ISAKMP (IKE).
```

```
R1(config)# set peer 200.165.200.1

#Define o peer remoto, ou seja, o IP público do outro roteador.
```

```
R1(config)# set pfs group5

#Habilita o Perfect Forward Secrecy (PFS) com Diffie-Hellman grupo 5, garantindo que as chaves da fase 2 sejam únicas e não dependam das da fase 1.
```

```
R1(config)# set security-association lifetime seconds 86400

#Define o tempo de vida da associação de segurança (SA) para 86400 segundos (24 horas) antes de renegociar.
```

```
R1(config)# set transform-set R1-R3

#Aponta para o transform-set previamente criado, que define como o tráfego será protegido (AES 256 + HMAC-SHA).
```

```
R1(config)# match address 100

#Define qual tráfego irá passar pela VPN usando a **ACL 100**, que foi criada separadamente para definir os fluxos permitidos na VPN.
```

## EM R3 FAÇA A MESMA COISA SÓ MUDANDO O SET PEER E O SET TRANSFORM
