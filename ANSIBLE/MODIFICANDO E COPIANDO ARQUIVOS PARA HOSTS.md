
### **1. Copiando Arquivos com o Módulo `copy`**

O módulo `copy` é usado para copiar arquivos do **nó de controle** (onde o Ansible está sendo executado) para os **hosts remotos**.

#### **Exemplo: Copiar um Arquivo Simples**

```sh
- name: Copiar arquivo para o host remoto
  ansible.builtin.copy:
    src: /caminho/local/arquivo.txt
    dest: /caminho/remoto/arquivo.txt
    owner: root
    group: root
    mode: '0644'
```

**O que isso faz?**

- Copia o arquivo `arquivo.txt` do nó de controle para o caminho `/caminho/remoto/arquivo.txt` no host remoto.
    
- Define o proprietário (`owner`) e o grupo (`group`) como `root`.
    
- Define as permissões do arquivo (`mode`) como `0644`.

--- 
#### **Exemplo: Copiar um Arquivo com Permissões Específicas**

```sh
- name: Copiar arquivo com permissões específicas
  ansible.builtin.copy:
    src: /caminho/local/script.sh
    dest: /usr/local/bin/script.sh
    mode: '0755'  # Permissões de execução
```
**O que isso faz?**

- Copia o arquivo `script.sh` e define permissões de execução (`0755`).

--- 
### **2. Usando o Módulo `template` para Copiar e Modificar Arquivos**

O módulo `template` é semelhante ao `copy`, mas permite que você use **templates Jinja2** para criar arquivos dinâmicos com base em variáveis.

#### **Exemplo: Criar um Arquivo de Configuração Dinâmico**

Suponha que você tenha um arquivo de template chamado `config.conf.j2`:

```sh
# config.conf.j2
server_name {{ server_name }};
port {{ port }};
```

No playbook, você pode usar o módulo `template` para gerar o arquivo final:

```sh
- name: Criar arquivo de configuração dinâmico
  ansible.builtin.template:
    src: /caminho/local/config.conf.j2
    dest: /etc/meu_app/config.conf
    owner: root
    group: root
    mode: '0644'
  vars:
    server_name: "meu_servidor"
    port: 8080
```
**O que isso faz?**

- Cria o arquivo `/etc/meu_app/config.conf` no host remoto, substituindo as variáveis `server_name` e `port` no template.
--- 

### **3. Modificando Linhas Específicas com `lineinfile`**

O módulo `lineinfile` é usado para **adicionar, modificar ou remover linhas específicas** em um arquivo.

#### **Exemplo: Adicionar uma Linha a um Arquivo**

```sh
- name: Adicionar uma linha ao arquivo de configuração
  ansible.builtin.lineinfile:
    path: /etc/meu_app/config.conf
    line: "nova_linha=valor"
    state: present
```

**O que isso faz?**

- Adiciona a linha `nova_linha=valor` ao arquivo `/etc/meu_app/config.conf`.

--- 

#### **Exemplo: Substituir uma Linha Existente**

```sh
- name: Substituir uma linha no arquivo de configuração
  ansible.builtin.lineinfile:
    path: /etc/meu_app/config.conf
    regexp: "^port="
    line: "port=8080"
    state: present
```

**O que isso faz?**

- Procura por uma linha que comece com `port=` e a substitui por `port=8080`.
--- 
#### **Exemplo: Remover uma Linha**

```sh
- name: Remover uma linha do arquivo de configuração
  ansible.builtin.lineinfile:
    path: /etc/meu_app/config.conf
    regexp: "^linha_para_remover="
    state: absent
```

**O que isso faz?**

- Remove a linha que começa com `linha_para_remover=`.
---
### **4. Modificando Blocos de Texto com `blockinfile`**

O módulo `blockinfile` é usado para **adicionar, modificar ou remover blocos de texto** em um arquivo.

#### **Exemplo: Adicionar um Bloco de Texto**

```sh
- name: Adicionar um bloco de texto ao arquivo
  ansible.builtin.blockinfile:
    path: /etc/meu_app/config.conf
    block: |
      [novo_bloco]
      opcao1=valor1
      opcao2=valor2
    marker: "# {mark} ANSIBLE MANAGED BLOCK"
```
**O que isso faz?**

- Adiciona um bloco de texto ao arquivo `/etc/meu_app/config.conf`, delimitado por marcadores (`# BEGIN ANSIBLE MANAGED BLOCK` e `# END ANSIBLE MANAGED BLOCK`).
--- 
#### **Exemplo: Remover um Bloco de Texto**

```sh
- name: Remover um bloco de texto do arquivo
  ansible.builtin.blockinfile:
    path: /etc/meu_app/config.conf
    marker: "# {mark} ANSIBLE MANAGED BLOCK"
    state: absent
```
**O que isso faz?**

- Remove o bloco de texto delimitado pelos marcadores.
--- 
### **5. Exemplo Completo de Playbook**

Aqui está um exemplo completo de um playbook que copia, modifica e gerencia arquivos em hosts remotos:

```sh
- name: Gerenciar arquivos em hosts remotos
  hosts: all
  tasks:
    - name: Copiar arquivo simples
      ansible.builtin.copy:
        src: /caminho/local/arquivo.txt
        dest: /caminho/remoto/arquivo.txt
        owner: root
        group: root
        mode: '0644'

    - name: Criar arquivo de configuração dinâmico
      ansible.builtin.template:
        src: /caminho/local/config.conf.j2
        dest: /etc/meu_app/config.conf
        owner: root
        group: root
        mode: '0644'
      vars:
        server_name: "meu_servidor"
        port: 8080

    - name: Adicionar uma linha ao arquivo de configuração
      ansible.builtin.lineinfile:
        path: /etc/meu_app/config.conf
        line: "nova_linha=valor"
        state: present

    - name: Adicionar um bloco de texto ao arquivo
      ansible.builtin.blockinfile:
        path: /etc/meu_app/config.conf
        block: |
          [novo_bloco]
          opcao1=valor1
          opcao2=valor2
        marker: "# {mark} ANSIBLE MANAGED BLOCK"
```

### **6. Resumo**

- **`copy`**: Copia arquivos do nó de controle para os hosts remotos.
    
- **`template`**: Copia e modifica arquivos usando templates Jinja2.
    
- **`lineinfile`**: Modifica linhas específicas em um arquivo.
    
- **`blockinfile`**: Adiciona, modifica ou remove blocos de texto em um arquivo.

