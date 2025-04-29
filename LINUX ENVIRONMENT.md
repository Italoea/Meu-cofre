# ATIVIDADE REALIZADA NO ESXI 8.0

![[Pasted image 20250429084210.png]]


![[Pasted image 20250429084305.png]]


![[Pasted image 20250429084323.png]]


# 1° PASSO: COLOCAR O DEVIDO IP NAS INTERFACES:

### DEV MACHINE: nano/etc/network/interfaces


```
auto ens192
iface ens192 inet static
address 210.103.5.2
netmask 255.255.255.252

iface ens192 inet6 static
address cafe:2025:2028::2/64
```

### ISP ROUTER: nano/etc/network/interfaces

```
	REDE ISP E DEV MACHINE

auto ens192
iface ens192 inet static
address 210.103.5.1
netmask 255.255.255.252

iface ens192 inet6 static
address cafe:2025:2028::1/64

	REDE SHANGAHI

auto ens224
iface ens224 inet static
address 192.168.1.1
netmask 255.255.255.0

iface ens224 inet6 static
address face:2025:2028::1/64

	REDE BRAZIL

auto ens256
iface ens256 inet static
address 10.0.0.1
netmask 255.255.255.0

iface ens256 inet6 static
address faca:2025:2028::1/64

```



### BRAZIL-CLIENT: nano/etc/network/interfaces

```
auto ens192 
iface ens192 inet dhcp
iface ens192 inet dhcp
```


### BRAZIL-SRV: nano/etc/network/interfaces

```
auto ens192
iface ens192 inet static
address 10.0.0.2
netmask 255.255.255.0

iface ens192 inet6 static
address faca:2025:2028::2/64
```


### SHANGHAI-DC-1: nano/etc/network/interfaces

```
auto ens192
iface ens192 inet static
address 192.168.1.2
netmask 255.255.255.0

iface ens192 inet6 static
address face:2025:2028::2/64
```


### SHANGHAI-DC-2: nano/etc/network/interfaces

```
auto ens192
iface ens192 inet static
address 192.168.1.3
netmask 255.255.255.0

iface ens193 inet6 static
address face:2025:2028::3/64
```


### SHANGHAI-DC-3: nano/etc/network/interfaces

```
auto ens192
iface ens192 inet static
address 192.168.1.4

iface ens192 inet6 static 
address face:2025:2028::4/64
```


# 2º PASSO: VERIFICAR TODAS AS CONECTIVIDADES SE ESTÃO PINGANDO NA MESMA REDE OU NÃO.

![[Pasted image 20250429142529.png]]

# 3º PASSO: