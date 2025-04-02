
# Guia de Uso do ipcalc

## O que é o ipcalc?

O `ipcalc` é uma ferramenta de linha de comando utilizada para calcular informações sobre sub-redes a partir de um endereço IP e uma máscara de rede. Ele facilita a visualização de informações essenciais como endereço de rede, faixa de hosts, endereço de broadcast e muito mais.

## Instalação do ipcalc

Para instalar o `ipcalc` em distribuições Linux baseadas em Debian (como Ubuntu), use:

```bash
sudo apt install ipcalc
```

Para distribuições baseadas em RHEL (como Fedora e CentOS):

```bash
sudo dnf install ipcalc
```

Em distribuições Arch Linux:

```bash
sudo pacman -S ipcalc
```

## Como usar o ipcalc

O uso básico do `ipcalc` envolve passar um endereço IP seguido de sua máscara de rede. Exemplo:

```bash
ipcalc 172.16.0.0/24
```

Isso gera uma saída com informações detalhadas sobre a sub-rede.

## Explicação dos Campos

Ao executar `ipcalc`, você verá os seguintes campos:

### **Address (Endereço)**

- Exemplo: `172.16.0.0`
    
- É o endereço IP inserido para cálculo.
    
- Representa o primeiro IP da sub-rede.
    

### **Netmask (Máscara de Rede)**

- Exemplo: `255.255.255.0`
    
- Define quantos bits pertencem à parte de rede do endereço.
    
- Representa `/24`, significando que os primeiros 24 bits são reservados para a rede.
    
- Em binário: `11111111.11111111.11111111.00000000`
    

### **Wildcard**

- Exemplo: `0.0.0.255`
    
- É o inverso da máscara de rede.
    
- Em binário: `00000000.00000000.00000000.11111111`
    
- Utilizada em ACLs e filtros de rede.
    

### **Network (Rede)**

- Exemplo: `172.16.0.0/24`
    
- Representa a sub-rede.
    
- Em binário: `10101100.00010000.00000000.00000000`
    
- Utilizado para identificar a rede em tabelas de roteamento.
    

### **HostMin (Primeiro IP Válido)**

- Exemplo: `172.16.0.1`
    
- É o primeiro IP disponível para hosts na sub-rede.
    

### **HostMax (Último IP Válido)**

- Exemplo: `172.16.0.254`
    
- É o último IP utilizável por um host na sub-rede.
    

### **Broadcast**

- Exemplo: `172.16.0.255`
    
- Usado para enviar mensagens para todos os hosts da rede.
    
- Em binário: `10101100.00010000.00000000.11111111`
    

### **Hosts/Net (Número de Hosts na Sub-rede)**

- Exemplo: `254`
    
- Calculado como `2^(32 - bits da máscara) - 2` (o `-2` é porque os endereços de rede e broadcast não são usáveis por hosts comuns).
    

### **Classe e Tipo da Rede**

- Exemplo: `Class B, Private Internet`
    
- Indica a classe do IP. O endereço `172.16.0.0` pertence à Classe B.
    
- Também informa se a rede é privada ou pública.
    

![[Pasted image 20250402112053.png]]
