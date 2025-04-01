
### 1. Introdução

A administração de sistemas Linux envolve tarefas como:

- Criar, modificar e remover usuários e grupos.
    
- Configurar o SSH para acesso remoto seguro.
    
- Gerenciar permissões de superusuário com o `sudo`.
    

O Ansible permite automatizar essas tarefas, garantindo consistência e segurança em todos os hosts gerenciados.

---

### 2. Gerenciamento de Usuários e Grupos

O Ansible oferece módulos para gerenciar usuários e grupos de forma simples.

#### Tarefa 1: Criar um Usuário

Vamos criar um usuário chamado `joao` e adicioná-lo ao grupo `sudo`.

**playbook_create_user.yml:**

```sh
- hosts: all
  become: yes  # Executar como superusuário
  tasks:
    - name: Criar o usuário joao
      user:
        name: joao
        comment: "João Silva"
        groups: sudo
        append: yes  # Adiciona ao grupo sem remover outros grupos
        shell: /bin/bash
        password: "{{ 'senha_segura' | password_hash('sha512') }}"
```

**Executar o playbook:**

```sh
ansible-playbook -i inventory playbook_create_user.yml
```

**Explicação:**

- `name`: Nome do usuário.
    
- `groups`: Grupos aos quais o usuário pertence.
    
- `append: yes`: Adiciona o usuário ao grupo sem remover outros grupos.
    
- `password`: Define a senha do usuário (criptografada com SHA-512).

---

#### Tarefa 2: Criar um Grupo

Vamos criar um grupo chamado `desenvolvedores`.

**playbook_create_group.yml:**

```sh
- hosts: all
  become: yes
  tasks:
    - name: Criar o grupo desenvolvedores
      group:
        name: desenvolvedores
        state: present
```

**Executar o playbook:**

```sh
ansible-playbook -i inventory playbook_create_group.yml
```

**Explicação:**

- `name`: Nome do grupo.
    
- `state: present`: Garante que o grupo exista.

---

#### Tarefa 3: Adicionar um Usuário a um Grupo

Vamos adicionar o usuário `joao` ao grupo `desenvolvedores`.

**playbook_add_user_to_group.yml:**

```sh
- hosts: all
  become: yes
  tasks:
    - name: Adicionar usuário joao ao grupo desenvolvedores
      user:
        name: joao
        groups: desenvolvedores
        append: yes
```

**Executar o playbook:**

```sh
ansible-playbook -i inventory playbook_add_user_to_group.yml
```
**Explicação:**

- `append: yes`: Adiciona o usuário ao grupo sem remover outros grupos.

---

---

### 3. Configuração do SSH

O SSH é essencial para o acesso remoto seguro. Vamos configurar o SSH para permitir apenas autenticação por chave pública.

#### Tarefa 4: Configurar o SSH

Vamos configurar o SSH para desativar a autenticação por senha e permitir apenas chaves públicas.

**playbook_configure_ssh.yml:**

```sh
- hosts: all
  become: yes
  tasks:
    - name: Configurar o SSH para permitir apenas chaves públicas
      lineinfile:
        path: /etc/ssh/sshd_config
        regexp: "^PasswordAuthentication"
        line: "PasswordAuthentication no"
        state: present

    - name: Reiniciar o serviço SSH
      service:
        name: sshd
        state: restarted
```

**Executar o playbook:**

```sh
ansible-playbook -i inventory playbook_configure_ssh.yml
```

**Explicação:**

- `lineinfile`: Edita o arquivo de configuração do SSH.
    
- `regexp`: Localiza a linha que contém `PasswordAuthentication`.
    
- `line`: Define o valor como `no` para desativar a autenticação por senha.
    
- `service`: Reinicia o serviço SSH para aplicar as mudanças.
----
### 4. Configuração do Sudo

O `sudo` permite que usuários executem comandos como superusuário. Vamos configurar o `sudo` para permitir que o grupo `desenvolvedores` execute comandos sem senha.

#### Tarefa 5: Configurar o Sudo

Vamos adicionar uma regra ao arquivo `/etc/sudoers` para permitir que o grupo `desenvolvedores` execute comandos sem senha.

**playbook_configure_sudo.yml:**

```sh
- hosts: all
  become: yes
  tasks:
    - name: Configurar o sudo para o grupo desenvolvedores
      lineinfile:
        path: /etc/sudoers
        line: "%desenvolvedores ALL=(ALL) NOPASSWD: ALL"
        validate: "visudo -cf %s"  # Valida a sintaxe do arquivo sudoers
        state: present
```

**Executar o playbook:**

```sh
ansible-playbook -i inventory playbook_configure_sudo.yml
```

**Explicação:**

- `lineinfile`: Adiciona uma linha ao arquivo `/etc/sudoers`.
    
- `validate`: Valida a sintaxe do arquivo antes de salvar.
    
- `state: present`: Garante que a linha esteja presente.

---

### 5. Documentação das Tarefas

Documentar as tarefas automatizadas é essencial para a manutenção e o entendimento do sistema.

**Exemplo de Documentação:**

**Manual de Gerenciamento de Usuários, SSH e Sudo**

1. **Criação de Usuários e Grupos**
    
    - Playbook: `playbook_create_user.yml`
        
    - Tarefas:
        
        - Criar o usuário `joao`.
            
        - Adicionar o usuário ao grupo `sudo`.
            
2. **Configuração do SSH**
    
    - Playbook: `playbook_configure_ssh.yml`
        
    - Tarefas:
        
        - Desativar a autenticação por senha.
            
        - Reiniciar o serviço SSH.
            
3. **Configuração do Sudo**
    
    - Playbook: `playbook_configure_sudo.yml`
        
    - Tarefas:
        
        - Permitir que o grupo `desenvolvedores` execute comandos sem senha.
            

---

### 6. Boas Práticas

- **Testes**: Sempre teste os playbooks em um ambiente de desenvolvimento antes de aplicá-los em produção.
    
- **Documentação**: Documente todas as tarefas e configurações.
    
- **Segurança**: Use chaves SSH e configure o `sudo` com cuidado para evitar vulnerabilidades.
    

---

### 7. Conclusão

Nesta aula, aprendemos a:

- Gerenciar usuários e grupos.
    
- Configurar o SSH para acesso remoto seguro.
    
- Modificar as configurações do `sudo` para gerenciar permissões de superusuário.
    

Com essas técnicas, você pode automatizar a administração de usuários, SSH e `sudo` em seus hosts gerenciados pelo Ansible, garantindo consistência e segurança.