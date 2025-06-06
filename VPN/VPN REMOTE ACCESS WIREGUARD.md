

![[Pasted image 20250604163912.png]]

## NO CLIENTE E NO SERVIDOR 

```
sudo apt install wireguard
```


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


## CRIE O ARQUIVO /ETC/WIREGUARD/WG0.CONF  E NELE DEVE CONTER:

```
[Interface]
1	PrivateKey = +E0z2nYOezr5oHWASuMJJEGXTouBrdyhK7DKxyE8iEQ=
2	Address = 10.0.0.1/24
3	ListenPort = 51820


[Peer]
4	PublicKey = chave_publica_2_do_cliente
5	AllowedIPs = 0.0.0.0/0

#1 A CHAVE PRIVADA DO MEU SERVIDOR
#2 O ENDEREÇO DO TUNNEL DA VPN
#3 A PORTA QUE MEU SERVIDOR VAI TRABALHAR
#4 CHAVE PUBLICA DO CLIENTE
#5 IPS QUE TÃO PERMITIDOS NO TUNNEL

```

## NO CLIENTE CRIE O MESMO PAR DE CHAVES E O MESMO ARQUIVO /ETC/WIREGUARD/WG0.CONF

# NO CLIENTE

```
[Interface]
1	PrivateKey = +E0z2nYOezr5oHWASuMJJEGXTouBrdyhK7DKxyE8iEQ=
2	Address = 10.0.0.2/24



[Peer]
3	PublicKey = chave_publica_2_do_server
4	AllowedIPs = 0.0.0.0/0
5	Endpoint = 10.10.10.22:51820


#1 A CHAVE PRIVADA DO CLIENTE
#2 O ENDEREÇO DO TUNNEL DA VPN
#3 CHAVE PUBLICA DO MEU SERVIDOR
#4 IPS QUE TÃO PERMITIDOS NO TUNNEL
#5 SOCKET DO MEU SERVER 
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


ip route del 10.100.0.0/24 via 193.193.18.2