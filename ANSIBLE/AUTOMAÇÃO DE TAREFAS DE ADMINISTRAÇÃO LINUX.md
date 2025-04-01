
#### 1. Introdução

A administração de sistemas Linux envolve uma série de tarefas repetitivas e complexas, como instalação de pacotes, configuração de serviços, gerenciamento de usuários e monitoramento de sistemas. O Ansible é uma ferramenta poderosa que permite automatizar essas tarefas, aumentando a eficiência e reduzindo erros humanos.

---
#### 2. Configuração Inicial do Ansible

Antes de começar a automatizar tarefas, é necessário configurar o Ansible para gerenciar seus hosts.

**Passo 1: Instalar o Ansible**

```sh
sudo apt-get update
sudo apt-get install ansible
```

**Passo 2: Configurar o Inventário**  
Crie um arquivo de inventário (`inventory`) para listar os hosts gerenciados.

**inventory:**

```sh
[webservers]
host1 ansible_host=192.168.1.101
host2 ansible_host=192.168.1.102

[dbservers]
host3 ansible_host=192.168.1.103
```

**Passo 3: Configurar a Conectividade SSH**  
Certifique-se de que você pode se conectar aos hosts via SSH sem senha.

```sh
ssh-copy-id user@host1
ssh-copy-id user@host2
ssh-copy-id user@host3
```

---

#### 3. Automação de Tarefas Comuns

Vamos automatizar algumas tarefas comuns de administração de sistemas Linux.

**Tarefa 1: Instalação de Pacotes**  
Instalar pacotes é uma tarefa comum. Vamos automatizar a instalação do Nginx.

**playbook_install_nginx.yml:**

```
- hosts: webservers
  become: yes
  tasks:
    - name: Atualizar lista de pacotes
      apt:
        update_cache: yes

    - name: Instalar Nginx
      apt:
        name: nginx
        state: present
```

**Executar o Playbook:**

```sh
ansible-playbook -i inventory playbook_install_nginx.yml
```

**Tarefa 2: Configuração de Serviços**  
Configurar e garantir que um serviço esteja em execução.

**playbook_config_nginx.yml:**

```sh
- hosts: webservers
  become: yes
  tasks:
    - name: Configurar Nginx
      template:
        src: nginx.conf.j2
        dest: /etc/nginx/nginx.conf
      notify: Reiniciar Nginx

    - name: Iniciar e habilitar o serviço Nginx
      service:
        name: nginx
        state: started
        enabled: yes

  handlers:
    - name: Reiniciar Nginx
      service:
        name: nginx
        state: restarted
```

**Executar o Playbook:**

```sh
ansible-playbook -i inventory playbook_config_nginx.yml
```

**Tarefa 3: Gerenciamento de Usuários**  
Criar e gerenciar usuários.

**playbook_manage_users.yml:**

```sh
- hosts: all
  become: yes
  tasks:
    - name: Criar usuário
      user:
        name: joao
        comment: "Joao Silva"
        groups: sudo
        append: yes
        password: "{{ 'senha_segura' | password_hash('sha512') }}"

    - name: Adicionar chave SSH do usuário
      authorized_key:
        user: joao
        key: "{{ lookup('file', '/home/user/.ssh/id_rsa.pub') }}"
```

**Executar o Playbook:**

```sh
ansible-playbook -i inventory playbook_manage_users.yml
```

**Tarefa 4: Monitoramento de Sistemas**  
Configurar o monitoramento de sistemas com o `cron`.

**playbook_monitor_system.yml:**

```sh
- hosts: all
  become: yes
  tasks:
    - name: Adicionar tarefa cron para monitoramento
      cron:
        name: "Monitorar uso de disco"
        minute: "*/5"
        job: "df -h >> /var/log/disk_usage.log"
```

**Executar o Playbook:**

```
ansible-playbook -i inventory playbook_monitor_system.yml
```

#### 4. Utilizando Variáveis e Templates

Variáveis e templates permitem personalizar playbooks para diferentes ambientes.

**Exemplo de Uso de Variáveis:**

```
- hosts: webservers
  become: yes
  vars:
    nginx_port: 8080
  tasks:
    - name: Configurar Nginx com porta personalizada
      template:
        src: nginx.conf.j2
        dest: /etc/nginx/nginx.conf
      notify: Reiniciar Nginx
```

**nginx.conf.j2:**

```sh
server {
    listen {{ nginx_port }};
    server_name localhost;

    location / {
        root /var/www/html;
        index index.html;
    }
}
```



**Manual de Automação de Tarefas**

1. **Instalação de Pacotes**
    
    - Playbook: `playbook_install_nginx.yml`
        
    - Tarefas:
        
        - Atualizar lista de pacotes.
            
        - Instalar Nginx.
            
2. **Configuração de Serviços**
    
    - Playbook: `playbook_config_nginx.yml`
        
    - Tarefas:
        
        - Configurar Nginx.
            
        - Iniciar e habilitar o serviço Nginx.
            
3. **Gerenciamento de Usuários**
    
    - Playbook: `playbook_manage_users.yml`
        
    - Tarefas:
        
        - Criar usuário.
            
        - Adicionar chave SSH do usuário.
            
4. **Monitoramento de Sistemas**
    
    - Playbook: `playbook_monitor_system.yml`
        
    - Tarefas:
        
        - Adicionar tarefa cron para monitoramento.
            

#### 6. Boas Práticas

- **Modularização**: Divida as tarefas em playbooks e roles para facilitar a reutilização.
    
- **Documentação**: Documente todas as tarefas automatizadas e suas configurações.
    
- **Testes**: Sempre teste os playbooks em um ambiente de desenvolvimento antes de aplicá-los em produção.
    

#### 7. Conclusão

Automatizar tarefas de administração de sistemas Linux com o Ansible é uma prática essencial para aumentar a eficiência e reduzir erros. Com essas técnicas, você pode gerenciar servidores de forma mais eficiente e confiável.