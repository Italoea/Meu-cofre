ens

**

Introdução

Bem-vindo ao Módulo A!

Para concluir com êxito este módulo, leia as seguintes instruções com cuidado!

A competição tem um horário de início e final fixo. Cabe a você alocar seu tempo com sabedoria.

Login

A menos que especificado de outra forma neste documento, use as seguintes informações para todos os servidores e serviços:

Usuário: root / user

Senha: Skill39@Shangai

Configuração do sistema

Locale: English US (UTF-8)

Key Map: English US

Importante: Avaliação

A maioria das avaliações realizadas são de marcação funcional. Você tem permissão para escolher qualquer pacote de sua preferência para a conclusão da tarefa, como Apache ou NGINX. No entanto, se um pacote específico for indicado, certifique-se de instalar esse.

Por favor, note que não modificaremos suas configurações nem reiniciaremos quaisquer serviços ou máquinas virtuais, a menos que seja especificamente indicado. 

Portanto, certifique-se de que eles permaneçam operacionais em execução até o final da competição. Serviços que não estiverem funcionando ao término da competição, mesmo que quase totalmente configurados, não renderão pontos.

Pode haver várias maneiras de concluir uma tarefa específica.

Networking e SSH

A menos que especificado de outra forma, todos os serviços devem ser acessíveis por IPv4 e IPv6 (Dual Stack).

Descrição do projeto e tarefas

IMPORTANTE!!

Após configurar as máquinas virtuais para receberem configurações via ansible, gere uma snapshot para a correção, caso contrário, as tarefas de ansible não serão pontuadas.

Introdução

A startup de TI ClearSky (sem nuvens) contratou você para configurar sua nova infraestrutura de TI. Após o CFO ver a última fatura da nuvem, a empresa decidiu abandonar a computação em nuvem e migrar sua TI de volta para o hardware local.

**





![[Pasted image 20250325084017.png]]




**

Tarefas

# DEV-MACHINE

## Ansible

Instale o ansible nessa maquina.

Crie uma pasta em /data/ansible e guarde nela todos os playbooks.

Guarde as informações de inventário no arquivo /data/ansible/hosts

Crie um playbook nomeado “1-hostname.yaml” com as seguintes funções:

- Ao executar, o playbook deve configurar o hostname de todos os servidores em “SHANGHAI” de acordo com a tabela 1.
    

Crie um playbook nomeado “2-monitoramento.yaml” com as seguintes funções:

- Instalar e configurar o serviço Grafana no servidor “SHANGHAI-DC-3”.
    

- Ao executar, o playbook deve configurar todos os servidores em “SHANGHAI” para enviar métricas para o servidor “SHANGHAI-DC-3”.
    
- Utilize como localização “SHANGHAI”.
    

# ISP-ROUTER

## Roteamento

Todas as redes internas devem se comunicar!

## DHCP

Os clientes da rede BRAZIL devem receber informações de configuração de rede dinamicamente usando as seguintes informações:

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
    

# BRAZIL-CLIENT

## LDAP Client

Apenas membros da OU “Visitantes” podem fazer login nessa máquina.

## EMAIL Client

Esse cliente deve conseguir enviar e receber email através do programa ThunderBird.

**



**

# BRAZIL-SRV

## LDAP Server

Crie um domínio LDAP as seguintes especificações abaixo:

![[Pasted image 20250325085524.png]]
# SHANGHAI-DC-1

## WEB

Habilite o protocolo HTTPS para todos os VirtualHosts.

Crie os seguintes VirtualHosts:

“login.worldskillsbrasil.com.br”:

- Habilite autenticação básica.
    
- Apenas usuários da OU “Colaboradores” devem conseguir realizar o login.
    

“ca.worldskillsbrasil.com.br”:

- Publique a lista de certificados revogados e o certificado da CA nesse site.
    

## EMAIL

Utilize SMTP e IMAP4 para configurar um servidor de email operacional na rede local.

Utilize os usuários do dominio LDAP “worldskillsbrasil.com.br”.

Apenas os usuários da OU “Colaboradores” devem ter acesso ao email.

# SHANGHAI-DC-2

## DNS

Esse servidor deve servir Serviços de Resolução de Nome de Domínio para todos os servidores.

Configure as entradas para garantir o correto funcionamento dos serviços da topologia.

## CA

Utilize o openssl para configurar uma autoridade certificadora para atender todos os serviços que necessitam de certificados.

Publique o certificado da CA em https://ca.worldskillsbrasil.com.br/SHANGHAI-DC-2.crt

Publique a lista de certificados revogados em https://ca.worldskillsbrasil.com.br/SHANGHAI-DC-2.crl

**


**

# SHANGHAI-DC-3

## FILE SHARE

Configure esse servidor como FTP Server utilizando o ProFTP.

Usuários devem ficar presos em sua própria pasta home.

  
**

![[Pasted image 20250325083937.png]]



![[Pasted image 20250325114538.png]]![[Pasted image 20250325084017.png]]