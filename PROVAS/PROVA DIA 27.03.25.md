
**


| HOSTNAME        | IPV4            | IPV6                    | Sistema Operacional |
| --------------- | --------------- | ----------------------- | ------------------- |
| ISP-ROUTER      | 210.103.5.1/30  | 2025:face:2028:1::1/127 | Cisco IOS           |
|                 | 210.103.5.5/30  | 2025:face:2028:2::1/127 |                     |
|                 | 210.103.5.9/30  | 2025:face:2028:3::1/127 |                     |
| LYON-EDGE       | 210.103.5.6/30  | 2025:face:2028:2::2/127 | Cisco IOS           |
|                 | 172.16.0.1/24   | cafe:2025::1/64         |                     |
| SHANGHAI-EDGE   | 210.103.5.10/30 | 2025:face:2028:3::2/127 | Cisco IOS           |
|                 | 10.0.0.1/24     | faca:2025::1/64         |                     |
| BRAZIL-EDGE     | 210.103.5.2/30  | 2025:face:2028:1::2/127 | Cisco IOS           |
|                 | 192.168.1.1/24  | face:2025:1::1/64       |                     |
|                 | 192.168.2.1/24  | face:2025:2::1/64       |                     |
| LYON-SW         | 172.16.0.2/24   | cafe:2025::2/64         | Cisco IOS           |
| SHANGHAI-SW     | 10.0.0.2/24     | faca:2025::2/64         | Cisco IOS           |
| BRAZIL-SW-1     | 192.168.1.10/24 | face:2025::10/64        | Cisco IOS           |
| BRAZIL-SW-2     | 192.168.1.11/24 | face:2025::11/64        | Cisco IOS           |
| BRAZIL-SW-3     | 192.168.1.12/24 | face:2025::12/64        | Cisco IOS           |
| SHANGHAI-CLIENT | DHCPv4          | DHCPv6                  | Windows 11          |
| LYON-CLIENT     | DHCPv4          | DHCPv6                  | Debian 12(GUI)      |
| BRAZIL-CLIENT   | DHCPv4          | DHCPv6                  | VPCS                |
| BRAZIL-SRV      | 192.168.2.2/24  | face:2025::2/64         | Debian 12(CLI)      |



**
Tarefa

# Configuração Geral

## Todos os dispositivos

Configure o hostname como o da tabela 1.

Configure o endereçamento IP como o da tabela 1.

Configure o timezone como GMT +8.

Configure a senha Skill39@Shanghai como senha para o modo privilegiado.

# ISP-ROUTER

## OSPF

Configure OSPF com Autonomous System 2025 e área 0. 

Use Skill39 como senha para autenticação entre vizinhos.

# LYON-EDGE

## OSPF

Configure OSPF com Autonomous System 2025 e área 0. 

Use Skill39 como senha para autenticação entre vizinhos.

## ACL

Apenas requisições originadas de SHANGHAI devem ser aceitas para entrar na rede interna.

Todo o tráfego originado da rede externa não deve ser aceito.

## DHCP

Esse roteador deve distribuir informações de atribuição de endereços dinâmicos para a rede interna de acordo com o listado abaixo:

IPv4:

- Escopo: 172.16.0.100 - 172.16.0.200
    
- Máscara de rede: 255.255.255.0
    
- Gateway: 172.16.0.1
    
- DNS: 210.103.5.2
    

IPv6:

- Escopo: cafe:2025::100 - cafe:2025::2000
    
- Máscara de rede: ffff:ffff:ffff:ffff::0
    
- Gateway: cafe:2025::1
    
- DNS: 2025:face:2028:2::2
    

# LYON-SW

## Port Security

A porta do switch em que está conectado o host LYON-CLIENT deve aceitar apenas quadros que tenham o endereço MAC do LYON-CLIENT, caso a porta receba um quadro com outro endereço MAC, a porta deve ser desligada.

**

**

# LYON-CLIENT

## DHCP Cliente

Esse host deve receber as configurações de endereçamento IP dinamicamente.

## Acesso WEB

Esse cliente deve acessar a página web através do endereço [www.worldskillsbrasil.com.br](http://www.worldskillsbrasil.com.br) sem problemas.

  
  

# BRAZIL-EDGE

## OSPF

Configure OSPF com Autonomous System 2025 e área 0. 

Use Skill39 como senha para autenticação entre vizinhos.

## DHCP

Esse roteador deve distribuir informações de atribuição de endereços dinâmicos para as redes internas de acordo com o listado abaixo:

VLAN100:

IPv4:

- Escopo: 192.168.1.100 - 192.168.1.200
    
- Máscara de rede: 255.255.255.0
    
- Gateway: 192.168.1.1
    
- DNS: 192.168.2.1
    

IPv6:

- Escopo: face:2025:1::100 - face:2025:1::2000
    
- Máscara de rede: ffff:ffff:ffff:ffff::0
    
- Gateway: face:2025:1::1
    
- DNS: face:2025:2::1
    

VLAN200:

IPv4:

- Escopo: 192.168.2.100 - 192.168.2.200
    
- Máscara de rede: 255.255.255.0
    
- Gateway: 192.168.2.1
    
- DNS: 192.168.2.1
    

IPv6:

- Escopo: face:2025:2::100 - face:2025:2::2000
    
- Máscara de rede: ffff:ffff:ffff:ffff::0
    
- Gateway: face:2025:2::1
    
- DNS: face:2025:2::1
    

# BRAZIL-SW-1

## VLAN

Crie vlans conforme a tabela abaixo:

**

|        |         |
| ------ | ------- |
| NUMERO | NOME    |
| 100    | CLIENTE |
| 200    | SERVER  |

**
## VTP

Configure esse switch para distribuir as vlans dentro do domínio VTP.

O dominio deve ser vtp.worldskills.cisco

Esse switch deve agir como servidor.

Configure VTPv3.

Use Skill39Cisco como senha do domínio VTP.

## EtherChannel

Todos os links etherchannel devem estar no modo trunk.

Configure os links entre os switch de acordo com as informações abaixo:

- O link entre BRAZIL-SW-1 e BRAZIL-SW-2 deve ser dinamicamente atribuído como etherchannel usando um protocolo proprietário da cisco, BRAZIL-SW-2 deve iniciar a negociação.
    
- O link entre BRAZIL-SW-1 e BRAZIL-SW-3 deve ser sempre Etherchannel incondicionalmente.
    

# BRAZIL-SW-2

## VTP

Configure esse switch no dominio VTP vtp.worldskills.cisco

Esse switch deve receber todas as vlans dinamicamente.

## EtherChannel

Todos os links etherchannel devem estar no modo trunk.

Configure os links entre os switch de acordo com as informações abaixo:

- O link entre BRAZIL-SW-1 e BRAZIL-SW-2 deve ser dinamicamente atribuído como etherchannel usando um protocolo proprietário da cisco, BRAZIL-SW-2 deve iniciar a negociação.
    
- O link entre BRAZIL-SW-2 e BRAZIL-SW-3 deve ser dinamicamente atribuído como etherchannel usando um protocolo genérico, BRAZIL-SW-2 deve iniciar a negociação.
    

# BRAZIL-SW-3

## VTP

Configure esse switch no dominio VTP vtp.worldskills.cisco

Esse switch deve receber todas as vlans dinamicamente.

## EtherChannel

Todos os links etherchannel devem estar no modo trunk.

Configure os links entre os switch de acordo com as informações abaixo:

- O link entre BRAZIL-SW-2 e BRAZIL-SW-3 deve ser dinamicamente atribuído como etherchannel usando um protocolo genérico, BRAZIL-SW-2 deve iniciar a negociação.
    
- O link entre BRAZIL-SW-1 e BRAZIL-SW-3 deve ser sempre Etherchannel incondicionalmente.**


**
# BRAZIL-CLIENT

## DHCP Cliente

Esse host deve receber as configurações de endereçamento IP dinamicamente.

# BRAZIL-SRV

## WEB

Instale e configure um serviço WEB nesse servidor.

O serviço deve escutar na porta 80.

## DNS

Instale e configure um serviço DNS nesse servidor.

Crie o seguinte registro:

[www.worldskillsbrasil.com.br](http://www.worldskillsbrasil.com.br) ⇒ 210.103.5.2

O serviço deve escutar na porta 53.

# SHANGHAI-EDGE

## OSPF

Configure OSPF com Autonomous System 2025 e área 0. 

Use Skill39 como senha para autenticação entre vizinhos.

## DHCP

Esse roteador deve distribuir informações de atribuição de endereços dinâmicos para as redes internas de acordo com o listado abaixo:

IPv4:

- Escopo: 10.0.0.100 - 10.0.0.200
    
- Máscara de rede: 255.255.255.0
    
- Gateway: 10.0.0.1
    
- DNS: 210.103.5.2
    

IPv6:

- Escopo: faca:2025::100 faca:2025::2000
    
- Máscara de rede: ffff:ffff:ffff:ffff::0
    
- Gateway: faca:2025::2
    
- DNS: 2025:face:2028:1::2
    

## PAT

Hosts da rede SHANGHAI, ao acessar as redes externas, devem usar o endereço IP público do roteador

# SHANGHAI-SW

## SSH

Configure esse switch para receber conexões remotas utilizando o protocolo SSH.

Crie um usuário chamado remote-user com a senha Skill39.

**

**

# SHANGHAI-CLIENT

## DHCP Cliente

Esse host deve receber as configurações de endereçamento IP dinamicamente.

## Acesso WEB

Esse cliente deve acessar a página web através do endereço [www.worldskillsbrasil.com.br](http://www.worldskillsbrasil.com.br) sem problemas.

TOPOLOGIA

**

![[Pasted image 20250327085830.png]]
