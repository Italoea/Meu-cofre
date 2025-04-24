
# Guia Completo sobre NetworkManager no Linux

## Introdução

O NetworkManager é uma ferramenta de gerenciamento de rede amplamente usada em distribuições Linux modernas, como Debian, Ubuntu, Fedora, CentOS e outras. Ele fornece uma maneira simplificada de configurar e gerenciar conexões de rede, incluindo Ethernet, Wi-Fi, VPN, e redes móveis. O NetworkManager é especialmente útil para ambientes dinâmicos, como laptops que se conectam a diferentes redes Wi-Fi, mas também pode ser usado em servidores para configurações estáticas.

Este guia cobre a instalação, configuração e uso do NetworkManager, com foco em suas principais ferramentas: `nmcli` (interface de linha de comando) e `nmtui` (interface de usuário baseada em texto). Também inclui exemplos práticos e solução de problemas comuns.

---

## O que é o NetworkManager?

O NetworkManager é um daemon (serviço em segundo plano) que gerencia configurações de rede no Linux. Ele foi projetado para:

- Simplificar a configuração de redes, especialmente em ambientes dinâmicos.
- Suportar vários tipos de conexões: Ethernet, Wi-Fi, VPN, PPPoE, redes móveis (3G/4G), etc.
- Integrar-se bem com ambientes de desktop (como GNOME e KDE) e servidores.
- Fornecer ferramentas de configuração, como `nmcli` (CLI), `nmtui` (TUI), e interfaces gráficas (como `nm-applet`).

### Componentes Principais

- **NetworkManager Daemon**: O serviço principal (`NetworkManager.service`) que gerencia as conexões.
- **nmcli**: Ferramenta de linha de comando para gerenciar redes.
- **nmtui**: Interface de usuário baseada em texto (TUI) para configuração interativa.
- **nm-applet**: Interface gráfica para ambientes de desktop (como GNOME ou KDE).
- **Configurações**: Armazenadas em `/etc/NetworkManager/` e em arquivos de configuração de conexão (geralmente em `/etc/NetworkManager/system-connections/`).

---

## Pré-requisitos

- Um sistema Linux com suporte ao NetworkManager (Debian, Ubuntu, Fedora, CentOS, etc.).
- Acesso de administrador (usuário `root` ou privilégios `sudo`).
- Conhecimento básico de redes (endereços IP, máscaras de sub-rede, gateways, DNS, etc.).
- (Opcional) Uma interface de rede configurável (Ethernet ou Wi-Fi).

---

## 1. Instalação do NetworkManager

### 1.1 Verificar se o NetworkManager Está Instalado

A maioria das distribuições Linux modernas já vem com o NetworkManager instalado por padrão. Para verificar:

#### Em Distribuições Baseadas em Debian/Ubuntu:

```
dpkg -l | grep network-manager
```

Exemplo de saída:

```
ii  network-manager  1.30.0-2  amd64  network management framework (daemon and userspace tools)
```

- Se não estiver instalado, você verá uma saída vazia.

#### Em Distribuições Baseadas em Red Hat/CentOS:

```
rpm -qa | grep NetworkManager
```

Exemplo de saída:

```
NetworkManager-1.36.0-2.el9.x86_64
```

### 1.2 Instalar o NetworkManager

Se o NetworkManager não estiver instalado, você pode instalá-lo usando o gerenciador de pacotes da sua distribuição.

#### Debian/Ubuntu:

1. Atualize a lista de pacotes:
    
    ```
    sudo apt update
    ```
    
2. Instale o NetworkManager:
    
    ```
    sudo apt install network-manager
    ```
    
    - Isso instala o daemon principal e ferramentas como `nmcli` e `nmtui`.

#### CentOS/RHEL:

1. Instale o NetworkManager:
    
    ```
    sudo yum install NetworkManager
    ```
    
    Ou, se estiver usando `dnf` (em versões mais recentes):
    
    ```
    sudo dnf install NetworkManager
    ```
    

### 1.3 Iniciar e Habilitar o Serviço

Após a instalação, certifique-se de que o serviço NetworkManager está ativo e habilitado para iniciar automaticamente no boot.

1. Inicie o serviço:
    
    ```
    sudo systemctl start NetworkManager
    ```
    
2. Habilite o serviço para iniciar no boot:
    
    ```
    sudo systemctl enable NetworkManager
    ```
    
3. Verifique o status do serviço:
    
    ```
    systemctl status NetworkManager
    ```
    
    Exemplo de saída (indicando que o serviço está ativo):
    
    ```
    ● NetworkManager.service - Network Manager
       Loaded: loaded (/lib/systemd/system/NetworkManager.service; enabled; vendor preset: enabled)
       Active: active (running) since Mon 2025-04-24 10:00:00 UTC; 1h ago
    ```
    

---

## 2. Ferramentas do NetworkManager

O NetworkManager oferece várias ferramentas para gerenciar redes. As duas mais comuns para uso em servidores ou ambientes sem interface gráfica são `nmcli` e `nmtui`.

### 2.1 `nmcli` - Interface de Linha de Comando

O `nmcli` é uma ferramenta poderosa para gerenciar redes diretamente na linha de comando. É ideal para automação (scripts) e para administradores que preferem trabalhar no terminal.

#### Verificar a Versão do NetworkManager:

```
nmcli --version
```

Exemplo de saída:

```
nmcli tool, version 1.30.0
```

#### Listar Todas as Conexões:

```
nmcli connection show
```

Exemplo de saída:

```
NAME   UUID                                  TYPE      DEVICE
eth0   5fb06bd0-0bb0-7ffb-45f1-d6edd65f3e03  ethernet  eth0
wlan0  9c92fad9-6d71-4e6a-9b6d-4d4e6e6d6e6d  wifi      --
```

#### Listar Dispositivos de Rede:

```
nmcli device status
```

Exemplo de saída:

```
DEVICE  TYPE      STATE        CONNECTION
eth0    ethernet  connected    eth0
wlan0   wifi      disconnected --
lo      loopback  unmanaged    --
```

#### Criar uma Nova Conexão Ethernet (IP Estático):

Para configurar uma interface Ethernet (`eth0`) com um IP estático:

```
sudo nmcli connection add type ethernet ifname eth0 con-name "minha-conexao" ipv4.method manual ipv4.addresses 192.168.1.100/24 ipv4.gateway 192.168.1.1 ipv4.dns 8.8.8.8
```

- `type ethernet`: Tipo de conexão.
- `ifname eth0`: Interface de rede.
- `con-name "minha-conexao"`: Nome da conexão.
- `ipv4.method manual`: Define configuração manual (estática).
- `ipv4.addresses 192.168.1.100/24`: Endereço IP e máscara de sub-rede.
- `ipv4.gateway 192.168.1.1`: Gateway.
- `ipv4.dns 8.8.8.8`: Servidor DNS.

#### Ativar uma Conexão:

```
sudo nmcli connection up minha-conexao
```

#### Conectar a uma Rede Wi-Fi:

Para se conectar a uma rede Wi-Fi chamada "MinhaRede" com senha "MinhaSenha123":

```
sudo nmcli device wifi connect MinhaRede password MinhaSenha123
```

#### Desativar uma Conexão:

```
sudo nmcli connection down minha-conexao
```

#### Deletar uma Conexão:

```
sudo nmcli connection delete minha-conexao
```

### 2.2 `nmtui` - Interface de Usuário Baseada em Texto

O `nmtui` é uma ferramenta interativa baseada em texto, ideal para usuários que preferem uma interface visual no terminal, mas não têm um ambiente gráfico.

#### Iniciar o `nmtui`:

```
nmtui
```

- Isso abrirá uma interface com as seguintes opções:
    - **Edit a connection**: Editar uma conexão existente ou criar uma nova.
    - **Activate a connection**: Ativar uma conexão de rede.
    - **Set system hostname**: Configurar o nome do host do sistema.

#### Exemplo: Criar uma Nova Conexão Ethernet com IP Estático:

1. Execute `nmtui`.
2. Selecione **Edit a connection** e pressione `Enter`.
3. Selecione **Add** para criar uma nova conexão.
4. Escolha o tipo **Ethernet** e pressione `Enter`.
5. Preencha os detalhes:
    - **Profile name**: Nome da conexão (ex.: "minha-conexao").
    - **Device**: Interface (ex.: `eth0`).
    - **IPv4 CONFIGURATION**: Mude para **Manual**.
    - **Addresses**: Adicione o IP e a máscara (ex.: `192.168.1.100/24`).
    - **Gateway**: Adicione o gateway (ex.: `192.168.1.1`).
    - **DNS servers**: Adicione o DNS (ex.: `8.8.8.8`).
6. Selecione **OK** e saia.

#### Ativar a Conexão com `nmtui`:

1. No menu principal do `nmtui`, selecione **Activate a connection**.
2. Escolha a conexão ("minha-conexao") e pressione `Enter` para ativá-la.
3. Saia com **Quit**.

#### Nota sobre `--version` no `nmtui`:

O `nmtui` não suporta a opção `--version`. Para verificar a versão, use `nmcli --version`, como mencionado anteriormente.

---

## 3. Configurações Avançadas

### 3.1 Configurar uma Rede Wi-Fi com Segurança

Para configurar uma rede Wi-Fi com WPA2 e IP estático usando `nmcli`:

```
sudo nmcli connection add type wifi ifname wlan0 con-name "minha-wifi" ssid "MinhaRede" wifi-sec.key-mgmt wpa-psk wifi-sec.psk "MinhaSenha123" ipv4.method manual ipv4.addresses 192.168.1.101/24 ipv4.gateway 192.168.1.1 ipv4.dns 8.8.8.8
```

- `type wifi`: Tipo de conexão.
- `ifname wlan0`: Interface Wi-Fi.
- `con-name "minha-wifi"`: Nome da conexão.
- `ssid "MinhaRede"`: Nome da rede Wi-Fi.
- `wifi-sec.key-mgmt wpa-psk`: Tipo de segurança.
- `wifi-sec.psk "MinhaSenha123"`: Senha da rede.
- `ipv4.method manual`: IP estático.
- `ipv4.addresses`, `ipv4.gateway`, `ipv4.dns`: Configurações de IP, gateway e DNS.

Ative a conexão:

```
sudo nmcli connection up minha-wifi
```

### 3.2 Configurar um Servidor DNS Personalizado

Para adicionar servidores DNS a uma conexão existente:

```
sudo nmcli connection modify minha-conexao ipv4.dns "8.8.8.8 8.8.4.4"
sudo nmcli connection down minha-conexao
sudo nmcli connection up minha-conexao
```

### 3.3 Gerenciar Conexões VPN

O NetworkManager suporta VPNs (como OpenVPN, PPTP, etc.), mas você precisa instalar os plugins correspondentes.

#### Instalar o Plugin OpenVPN (Debian/Ubuntu):

```
sudo apt install network-manager-openvpn
```

#### Configurar uma Conexão VPN com `nmcli`:

```
sudo nmcli connection add type vpn vpn-type openvpn con-name "minha-vpn" vpn.data "remote=vpn.exemplo.com,port=1194,ca=/caminho/para/ca.crt,cert=/caminho/para/client.crt,key=/caminho/para/client.key"
```

- Ajuste os valores de `remote`, `port`, e caminhos dos arquivos de certificado conforme necessário.

#### Ativar a VPN:

```
sudo nmcli connection up minha-vpn
```

---

## 4. Solução de Problemas

### 4.1 Verificar o Status do Serviço

Se o NetworkManager não estiver funcionando:

```
systemctl status NetworkManager
```

- Se não estiver ativo, inicie-o:
    
    ```
    sudo systemctl start NetworkManager
    ```
    

### 4.2 Conexão Não Ativa

Se uma conexão não estiver funcionando:

1. Verifique o status do dispositivo:
    
    ```
    nmcli device status
    ```
    
2. Tente reativar a conexão:
    
    ```
    sudo nmcli connection up minha-conexao
    ```
    
3. Verifique os logs do NetworkManager:
    
    ```
    journalctl -u NetworkManager
    ```
    

### 4.3 Problemas com Wi-Fi

- Liste redes Wi-Fi disponíveis:
    
    ```
    nmcli device wifi list
    ```
    
- Se a rede não aparecer, verifique se o adaptador Wi-Fi está ativo:
    
    ```
    rfkill list
    ```
    
    - Se estiver bloqueado, desbloqueie:
        
        ```
        rfkill unblock wifi
        ```
        

### 4.4 Conflitos com Outras Ferramentas de Rede

Ferramentas como `ifupdown` (usada pelo `/etc/network/interfaces`) podem entrar em conflito com o NetworkManager. Para evitar isso:

1. Verifique se o NetworkManager está gerenciando as interfaces:
    
    ```
    nmcli device
    ```
    
    - Se uma interface estiver como "unmanaged", edite `/etc/NetworkManager/NetworkManager.conf`:
        
        ```
        [ifupdown]
        managed=true
        ```
        
2. Reinicie o serviço:
    
    ```
    sudo systemctl restart NetworkManager
    ```
    

---

## 5. Comandos Úteis do NetworkManager

- Mostrar status geral:
    
    ```
    nmcli general status
    ```
    
- Mostrar todas as propriedades de uma conexão:
    
    ```
    nmcli connection show minha-conexao
    ```
    
- Reiniciar o NetworkManager:
    
    ```
    sudo systemctl restart NetworkManager
    ```
    
- Desativar o NetworkManager (se necessário):
    
    ```
    sudo systemctl stop NetworkManager
    sudo systemctl disable NetworkManager
    ```
    

---

## 6. Considerações Finais

- **Vantagens do NetworkManager**:
    - Fácil de usar, especialmente para usuários finais.
    - Suporta uma ampla gama de tipos de conexão.
    - Integração com ambientes de desktop.
- **Desvantagens**:
    - Pode ser considerado "pesado" para servidores simples.
    - Pode entrar em conflito com configurações manuais tradicionais (como `/etc/network/interfaces`).
- **Alternativas**:
    - `ifupdown` (tradicional, baseado em `/etc/network/interfaces`).
    - `systemd-networkd` (leve, para servidores).
    - Configurações manuais com `ip` e `iw`.
