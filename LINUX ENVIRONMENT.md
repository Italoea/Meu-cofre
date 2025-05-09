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
gateway 210.103.5.1

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
gateway 10.0.0.1

iface ens192 inet6 static
address faca:2025:2028::2/64
```


### SHANGHAI-DC-1: nano/etc/network/interfaces

```
auto ens192
iface ens192 inet static
address 192.168.1.2
netmask 255.255.255.0
gateway 192.168.1.1

iface ens192 inet6 static
address face:2025:2028::2/64
```


### SHANGHAI-DC-2: nano/etc/network/interfaces

```
auto ens192
iface ens192 inet static
address 192.168.1.3
netmask 255.255.255.0
gateway 192.168.1.1

iface ens193 inet6 static
address face:2025:2028::3/64
```


### SHANGHAI-DC-3: nano/etc/network/interfaces

```
auto ens192
iface ens192 inet static
address 192.168.1.4
gateway 192.168.1.1

iface ens192 inet6 static 
address face:2025:2028::4/64
```


# 2º PASSO: VERIFICAR TODAS AS CONECTIVIDADES SE ESTÃO PINGANDO NA MESMA REDE OU NÃO.

![[Pasted image 20250429142529.png]]

# 3º PASSO: CONFIGURAR O SERVIDOR DHCP NO ISP-ROUTER

IPv4:

- Escopo: 10.0.0.200 - 10.0.0.250
    
- Máscara de sub-rede: 255.255.255.0
    
- Gateway: 10.0.0.1
    
- DNS: 192.168.1.3
    

IPv6:

- Escopo: faca:2025:2028::300 - faca:2025:2028::500
    
- Máscara de sub-rede: ffff:ffff:ffff:ffff::0
    
- Gateway: faca:2025:2028::1
    
- DNS: face:2025:2028::3
    
### Para instalar o servidor dhcp

```
apt install isc-dhcp-server
```

### PARA CONFIGURAR DHCP ***IPV4:*** nano /etc/dhcp/dhcp/dhcpd.conf

```
subnet 10.0.0.0 netmask 255.255.255.0 {
range 10.0.0.200 10.0.0.250; #Range de IP
option routers 10.0.0.1; #Default gatwey
option domain-name-servers 192.168.1.3; #Servidor DNS
default-lease-time 600;
max-lease-time7200;
}
```

### PARA CONFIGURAR DHCP ***IPV6***: nano /etc/dhcp/dhcp/dhcpd6.conf

```
subnet6 faca:2025:2028::/64 {
range6 faca:2025:2028::300 faca:2025:2028::500; #Range de IP
option dhcp6.name-servers face:2025:2028::3; #Servidor DNS
option dhcp6.info-refresh-time 21600;
}
```

### PARA CONFIGURAR A INTERFACE QUE O DHCP VAI RODAR VÁ PARA: nano/etc/defautl/isc-dhcp-server

```
	DESCOMENTE ESSAS LINHAS
DHCPDv6_CONF=/etc/dhcp/dhcpd6.conf
DHCPDv6_PID=/var/run/dhcpd6.pid

	PARA CONFIGURAR A INTERFACE QUE O DHCP VAI RODAR
INTERFACESv4="ens256"
INTERFACESv6="ens256"
```


# 4° PASSO: CONFIGURAR AS ROTAS DE ACORDO COM A PROVA.

#### **Todas as redes internas devem se comunicar!

```
COMO AS INTERFACES DE GATEWEY ESTÃO EM UM ÚNICO SERVIDOR, APÓS AS CONFIGURAÇÕES ACIMA, ELES DEVERÃO SE COMUNICAR SEM ÊXITO.
```


# 5° PASSO: BAIXAR O ANSIBLE NA MÁQUINA DEV-MACHINE E CRIAR O DIRETÓRIO.

```
apt install ansible
mkdir -p /data/ansible
```

## Caso dê erro de unable to fetch some archives, maybe run apt-get update or try with --fix-missing

 ## Vá para nano /etc/apt/sources.list
## Comente as linhas dos repositórios se for netinst e deixe só a do dlbd


![[Pasted image 20250509145415.png]]


# 6° PASSO: CRIAR O INVENTARIO "HOSTS" E O ARQUIVO DE CONFIGURAÇÃO "ANSIBLE.CFG"

```
touch hosts
touch ansible.cfg
```

## Configurar o inventario "hosts"

```
[shanghai]
192.168.1.2
192.168.1.3
192.168.1.4

[shanghai:vars]
ansible_user=root
ansible_password=P@ssw0rd
ansible_become=yes
ansible_become_method=sudo
ansible_ssh_common_args='-o StrictHostKeyChecking=no'

[monitoring]
192.168.1.4

[monitoring:vars]
ansible_user=root
ansible_password=P@ssw0rd
ansible_become=yes
ansible_become_method=sudo
ansible_ssh_common_args='-o StrictHostKeyChecking=no'

```

## Cofigurar o arquivo de configuração "ansible.cfg"

```
[defaults]
inventory =/data/ansible/hosts
remote_user = remote-user
host_key_checking= False
retry_file_enabled= False
timeout= 10
become = Trust

[ssh_connection]
pipelinig = True

```