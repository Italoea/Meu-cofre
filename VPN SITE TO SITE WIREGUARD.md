
![[Pasted image 20250605150508.png]]


## NO SERVER A:

```
ip route add 10.100.0.0/24 via 193.193.18.2

# PARA O CLIENTEA COSEGUIR SE COMUNICAR COM O CLIENTEB
```


## NO SERVER B:

```
ip route add 10.200.0.0/24 via 193.193.18.1

# PARA O CLIENTEB COSEGUIR SE COMUNICAR COM O CLIENTEA
```


# APÓS CONFERIR QUE AS REDES ESTÃO SE COMUNICANDO FAÇA OS PASSOS ABAIXO:

## GERANDO UMA CHAVE PRIVADA NO SERVIDOR:

```
wg genkey | sudo tee /etc/wireguard/private.key

# Irá a chave privada irá aparecer no caminho apontado
```


## USANDO A CHAVE PRIVADA PARA CRIAR A CHAVE PUBLICA:

```
sudo cat /etc/wireguard/private.key | wg pubkey | sudo tee /etc/wireguard/public.key

# Mostrando aonde está a chave privada e com ela gerando uma chave publica para o caminho citado
```
# FAÇA ISSO NOS DOIS SERVIDORES


## NO SERVER A:

![[Pasted image 20250605151817.png]]

```
[Interface]
1	PrivateKey = +E0z2nYOezr5oHWASuMJJEGXTouBrdyhK7DKxyE8iEQ=
2	Address = 10.0.0.1/24
3	ListenPort = 51820


[Peer]
4	PublicKey = chave_publica_2_do_outro_server
5	AllowedIPs = 0.0.0.0/0
6	Endpoint = 193.193.18.2:51820

#1 A CHAVE PRIVADA DO MEU SERVIDOR
#2 O ENDEREÇO DO TUNNEL DA VPN
#3 A PORTA QUE MEU SERVIDOR VAI TRABALHAR
#4 CHAVE PUBLICA DO OUTRO SERVIDOR
#5 IPS QUE TÃO PERMITIDOS NO TUNNEL
#6 IP PUBLICO DO OUTRO SERVIDOR COM A PORTA
```

## NO SERVER B:

![[Pasted image 20250605151955.png]]

```
[Interface]
1	PrivateKey = +E0z2nYOezr5oHWASuMJJEGXTouBrdyhK7DKxyE8iEQ=
2	Address = 10.0.0.1/24
3	ListenPort = 51820


[Peer]
4	PublicKey = chave_publica_2_do_outro_server
5	AllowedIPs = 0.0.0.0/0
6	Endpoint = 193.193.18.1:51820

#1 A CHAVE PRIVADA DO MEU SERVIDOR
#2 O ENDEREÇO DO TUNNEL DA VPN
#3 A PORTA QUE MEU SERVIDOR VAI TRABALHAR
#4 CHAVE PUBLICA DO OUTRO SERVIDOR
#5 IPS QUE TÃO PERMITIDOS NO TUNNEL
#5 IP PUBLICO DO OUTRO SERVIDOR COM A PORTA
```



## PARA HABILITAR O TUNNEL 

```
wg-quick up wg0
```

## PARA HABILITAR A INICIALIZAÇÃO AUTOMATICA:

```
systemctl enable --now wg-quick@wg0.service
```

## PARA VERIFICAR O TUNNEL:

```
wg
```


# APÓS FECHAR O TUNNEL E VERIFICAR QUE A VPN ESTÁ FUNCIONANDO REMOVA A ANTIGA ROTA E COLOQUE A ROTA DO TUNNEL





## NO SERVER A:

```
ip route add 10.100.0.0/24 via 10.10.10.2

# PARA O CLIENTEA COSEGUIR SE COMUNICAR COM O CLIENTEB CRIPTOGRAFADO
```


## NO SERVER B:

```
ip route add 10.200.0.0/24 via 10.10.10.1

# PARA O CLIENTEB COSEGUIR SE COMUNICAR COM O CLIENTEA CRIPTOGRAFADO