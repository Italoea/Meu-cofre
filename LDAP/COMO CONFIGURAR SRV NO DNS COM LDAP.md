
### A ENTRADA SRV DETALHA O SRVIÇO, O PROTOCOLO A PRIORIDADE E O PESO.

## EXEMPLO:


![[Pasted image 20250530100412.png]]

## NA ENTRADA:
```
ldap A 192.168.10.10 
#MOSTRO AONDE ESTÁ MEU SERVIDOR LDAP
```

## JÁ NA ENTRADA

```
_ldap._tcp.meudominio. SRV 10 de prioridade e 30 de peso 389 porta do ldap e meudominio.

_ldap._tcp.meudominio. SRV 10 30 389 meudominio.

```

## PARA VERIFICAR SE A ENTRADA ESTÁ CORRETA, NO SERVIDOR DNS

```
apt install dnsutils #para instalar o dig

dig -t SRV _ldap._tcp.meudominio 

# -t para especificar o tipo no meu caso é SRV 
```






