# Configurando um Servidor DHCP no Linux

## Introdução

O DHCP (Dynamic Host Configuration Protocol) é um protocolo que permite a atribuição automática de endereços IP e outras configurações de rede para dispositivos conectados a uma rede. Esta documentação aborda a instalação e configuração do servidor DHCP no Linux utilizando o `isc-dhcp-server`.

## Pré-requisitos

- Um servidor Linux (Ubuntu/Debian ou CentOS/RHEL).
    
- Permissões de superusuário (`root` ou `sudo`).
    
- Conectividade de rede adequada.
    

## Passo 1: Instalação do Servidor DHCP

### Ubuntu/Debian

```bash
sudo apt update
sudo apt install isc-dhcp-server -y
```

### CentOS/RHEL

```bash
sudo yum install dhcp-server -y
```

## Passo 2: Configuração do Servidor DHCP

O arquivo principal de configuração do DHCP fica localizado em:

```
/etc/dhcp/dhcpd.conf
```

Edite o arquivo de configuração:

```bash
sudo nano /etc/dhcp/dhcpd.conf
```

### Exemplo de Configuração do DHCP

Adicione as seguintes configurações ao arquivo:

```bash
default-lease-time 600;
max-lease-time 7200;

subnet 192.168.1.0 netmask 255.255.255.0 {
  range 192.168.1.100 192.168.1.200;
  option routers 192.168.1.1;
  option subnet-mask 255.255.255.0;
  option domain-name-servers 8.8.8.8, 8.8.4.4;
  option domain-name "example.com";
}
```

Se deseja definir IPs fixos para dispositivos específicos, adicione:

```bash
host cliente1 {
  hardware ethernet 00:1A:2B:3C:4D:5E;
  fixed-address 192.168.1.50;
}
```

## Passo 3: Configuração da Interface de Rede

Defina em qual interface o servidor DHCP irá operar. Edite o arquivo:

```bash
sudo nano /etc/default/isc-dhcp-server  # Ubuntu/Debian
sudo nano /etc/sysconfig/dhcpd          # CentOS/RHEL
```

Altere ou adicione:

```bash
INTERFACESv4="ens3"
```

## Passo 4: Reiniciando e Ativando o Serviço

### Ubuntu/Debian

```bash
sudo systemctl restart isc-dhcp-server
sudo systemctl enable isc-dhcp-server
```

### CentOS/RHEL

```bash
sudo systemctl restart dhcpd
sudo systemctl enable dhcpd
```

## Passo 5: Verificando o Status do DHCP

Para verificar se o servidor DHCP está rodando corretamente, use:

```bash
sudo systemctl status isc-dhcp-server  # Ubuntu/Debian
sudo systemctl status dhcpd            # CentOS/RHEL
```

Para visualizar os logs e verificar as concessões de IP:

```bash
sudo tail -f /var/log/syslog  # Ubuntu/Debian
sudo tail -f /var/log/messages  # CentOS/RHEL
```

## Conclusão

Agora seu servidor DHCP está configurado e pronto para distribuir endereços IP na rede. Para testar, conecte um cliente à rede e verifique se ele recebe um IP automaticamente. Caso tenha problemas, verifique os logs e revise a configuração.

---

**Nota:** Certifique-se de que não há outro servidor DHCP na mesma rede para evitar conflitos de endereçamento IP.



apt-cdrom add