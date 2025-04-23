# Configuração do VTP (VLAN Trunking Protocol) em Switches Cisco

## Introdução

O **VLAN Trunking Protocol (VTP)** é um protocolo proprietário da Cisco que permite a sincronização automática de configurações de VLANs entre switches no mesmo domínio VTP. Ele reduz o esforço de gerenciamento ao propagar criações, modificações e exclusões de VLANs a partir de um switch configurado como servidor para outros switches no domínio. Esta documentação descreve como configurar o VTP, incluindo os modos de operação, configuração do servidor primário (para VTP versão 3), melhores práticas e verificação.

## Pré-requisitos

- Acesso administrativo a um switch Cisco (via console, SSH ou Telnet).
- Switch Cisco com suporte a VTP (ex.: Catalyst 2950, 3560, 3750, 4500, 6500).
- Conhecimento básico da CLI (Command Line Interface) do Cisco IOS.
- Interfaces configuradas como trunk para propagação de mensagens VTP.
- Verificação de compatibilidade com a versão do VTP desejada (1, 2 ou 3).

## Modos de Operação do VTP

O VTP suporta três modos de operação:

- **Server**: Pode criar, modificar e excluir VLANs, propagando essas alterações para outros switches no mesmo domínio. Na versão 3, apenas o **servidor primário** pode realizar essas alterações.
- **Client**: Recebe e propaga atualizações de VLANs do servidor, mas não pode criar ou modificar VLANs localmente.
- **Transparent**: Não participa do VTP, mas encaminha mensagens VTP recebidas. As VLANs são configuradas localmente e não são sincronizadas com o domínio.

## Versões do VTP

- **VTP Versão 1**: Suporta VLANs padrão (1–1005), mas com funcionalidades limitadas.
- **VTP Versão 2**: Adiciona suporte a Token Ring e verificação de consistência.
- **VTP Versão 3**: Suporta VLANs estendidas (1–4094), servidor primário, e maior segurança. Recomendado para redes modernas.

## Passos para Configuração do VTP

### 1. Acessar o Modo de Configuração Global

Conecte-se ao switch e entre no modo EXEC privilegiado, depois no modo de configuração global:

```
enable
configure terminal
```

### 2. Configurar o Nome do Domínio VTP

Defina o nome do domínio VTP. Todos os switches no mesmo domínio devem ter o mesmo nome. Exemplo:

```
vtp domain empresa
```

### 3. Configurar o Modo VTP

Escolha o modo de operação do switch:

- Para modo servidor:
    
    ```
    vtp mode server
    ```
    
- Para modo cliente:
    
    ```
    vtp mode client
    ```
    
- Para modo transparente:
    
    ```
    vtp mode transparent
    ```
    

### 4. (Opcional) Configurar a Versão do VTP

Configure a versão do VTP, se necessário. Para VTP versão 3:

```
vtp version 3
```

**Nota**: Certifique-se de que todos os switches no domínio suportam a versão configurada.

### 5. (Opcional) Configurar uma Senha VTP

Adicione uma senha para maior segurança. Todos os switches no domínio devem usar a mesma senha:

```
vtp password sua_senha
```

### 6. (VTP Versão 3) Promover o Switch a Servidor Primário

Na versão 3, apenas o servidor primário pode modificar VLANs. Para promover o switch a servidor primário, saia do modo de configuração global e execute:

```
vtp primary vlan
```

Se houver uma senha VTP, ela será solicitada. Para forçar a promoção (com cuidado):

```
vtp primary vlan force
```

### 7. Configurar Portas Trunk

Para que o VTP propague atualizações, as portas entre switches devem estar configuradas como trunk. Exemplo:

```
interface gigabitEthernet0/1
switchport mode trunk
exit
```

### 8. Verificar a Configuração

Verifique o status do VTP:

```
show vtp status
```

Exemplo de saída:

```
VTP Version                     : 3
VTP Operating Mode              : Server
VTP Domain Name                 : empresa
Configuration Revision          : 5
Primary ID                      : 0012.3456.7890
Primary Description             : Switch1
```

Verifique também a senha VTP (se configurada):

```
show vtp password
```

### 9. Salvar a Configuração

Salve as alterações para persistirem após reinicializações:

```
write memory
```

## Exemplo Completo de Configuração (Servidor Primário VTP v3)

```
enable
configure terminal
vtp domain empresa
vtp mode server
vtp version 3
vtp password senha123
interface gigabitEthernet0/1
switchport mode trunk
exit
exit
vtp primary vlan
show vtp status
write memory
```

## Melhores Práticas

- **Use VTP Versão 3**: Oferece maior segurança e suporte a VLANs estendidas.
- **Configure uma Senha VTP**: Protege contra alterações não autorizadas no domínio.
- **Controle o Servidor Primário**: Documente qual switch é o servidor primário (VTP v3) e evite múltiplos servidores primários.
- **Gerencie o Número de Revisão**: Antes de adicionar um novo switch ao domínio, configure-o como transparente para evitar que um número de revisão mais alto sobrescreva as configurações:
    
    ```
    vtp mode transparent
    vtp mode server
    ```
    
- **Desative o VTP em Redes Sensíveis**: Se a sincronização de VLANs não for necessária, use o modo transparente para maior controle.
- **Verifique Conexões Trunk**: As mensagens VTP são propagadas apenas por links trunk.

## Resolução de Problemas

- **VLANs não propagadas**:
    - Verifique o nome do domínio VTP (`show vtp status`).
    - Confirme que a senha VTP é a mesma em todos os switches.
    - Assegure que as portas estão em modo trunk (`show interfaces trunk`).
    - Verifique o número de revisão para evitar conflitos.
- **Erro: "VTP VLAN configuration not allowed"** (VTP v3):
    - O switch não é o servidor primário. Promova-o com `vtp primary vlan`.
- **Conflitos de versão**:
    - Confirme que todos os switches usam a mesma versão do VTP.

## Considerações de Segurança

- **Desative o DTP em Portas Não Confiáveis**: Para evitar negociações indesejadas de trunk, configure `switchport nonegotiate` em portas conectadas a dispositivos não confiáveis.
- **Monitore o Domínio VTP**: Um switch com um número de revisão mais alto pode sobrescrever configurações de VLANs. Sempre verifique novos switches antes de integrá-los.
- **Use Modo Transparente em Redes Pequenas**: Para redes com poucos switches, o modo transparente elimina riscos associados ao VTP.

