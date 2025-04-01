### Criar um **playbook** no Ansible é a principal maneira de automatizar tarefas em seus servidores ou infraestrutura. Um playbook é um arquivo YAML que descreve as tarefas a serem executadas, os hosts onde elas serão aplicadas e outras configurações. Vou explicar passo a passo como criar um playbook e para que serve cada item.

---

### Estrutura Básica de um Playbook

Um playbook é composto por uma ou mais **plays**, e cada play contém uma lista de **tasks** (tarefas). Aqui está um exemplo básico:

```sh
---
- name: Instalar e configurar o Apache
  hosts: webservers
  become: yes
  tasks:
    - name: Instalar o Apache
      apt:
        name: apache2
        state: present

    - name: Iniciar e habilitar o serviço Apache
      service:
        name: apache2
        state: started
        enabled: yes
```


### Explicação de Cada Item

#### 1. **`---`**

- **O que é**: Indica o início de um documento YAML.
    
- **Para que serve**: É uma convenção para indicar que o arquivo é um YAML válido. Não é estritamente necessário, mas é uma boa prática.
    

---

#### 2. **`- name: Instalar e configurar o Apache`**

- **O que é**: O nome do **play**.
    
- **Para que serve**: Descreve o propósito do play. É opcional, mas ajuda na documentação e na legibilidade do playbook.
    

---

#### 3. **`hosts: webservers`**

- **O que é**: Especifica os hosts ou grupos de hosts onde o play será executado.
    
- **Para que serve**: Define em quais máquinas as tarefas serão aplicadas. No exemplo, o play será executado no grupo `webservers`, que deve ser definido no arquivo de inventário do Ansible.
    

---

#### 4. **`become: yes`**

- **O que é**: Indica que as tarefas serão executadas com privilégios elevados (como root).
    
- **Para que serve**: Permite que tarefas que exigem permissões de superusuário sejam executadas. Equivale a usar `sudo`.
    

---

#### 5. **`tasks:`**

- **O que é**: Lista de tarefas a serem executadas.
    
- **Para que serve**: Define as ações que o Ansible realizará nos hosts especificados.
    

---

#### 6. **`- name: Instalar o Apache`**

- **O que é**: O nome da tarefa.
    
- **Para que serve**: Descreve o propósito da tarefa. É opcional, mas ajuda na documentação e na legibilidade.
    

---

#### 7. **`apt:`**

- **O que é**: Módulo do Ansible para gerenciar pacotes em sistemas baseados em Debian/Ubuntu.
    
- **Para que serve**: Instala, remove ou atualiza pacotes. No exemplo, ele instala o pacote `apache2`.
    

---

#### 8. **`name: apache2`**

- **O que é**: Nome do pacote a ser gerenciado.
    
- **Para que serve**: Especifica qual pacote será instalado, removido ou atualizado.
    

---

#### 9. **`state: present`**

- **O que é**: Estado desejado do pacote.
    
- **Para que serve**: Define que o pacote deve estar instalado. Outros valores possíveis são `absent` (remover) e `latest` (atualizar para a versão mais recente).
    

---

#### 10. **`service:`**

- **O que é**: Módulo do Ansible para gerenciar serviços.
    
- **Para que serve**: Inicia, para, reinicia ou habilita serviços no sistema.
    

---

#### 11. **`name: apache2`**

- **O que é**: Nome do serviço a ser gerenciado.
    
- **Para que serve**: Especifica qual serviço será manipulado.
    

---

#### 12. **`state: started`**

- **O que é**: Estado desejado do serviço.
    
- **Para que serve**: Define que o serviço deve estar em execução. Outros valores possíveis são `stopped` (parado) e `restarted` (reiniciado).
    

---

#### 13. **`enabled: yes`**

- **O que é**: Define se o serviço deve ser habilitado para iniciar automaticamente na inicialização do sistema.
    
- **Para que serve**: Garante que o serviço seja iniciado automaticamente após reinicializações.
    

---



### Passos para Criar e Executar um Playbook

1. **Crie o arquivo YAML**:
    
    - Salve o conteúdo do playbook em um arquivo com extensão `.yml`, por exemplo, `playbook.yml`.
        
2. **Defina o inventário**:
    
    - Crie ou edite o arquivo de inventário (`/etc/ansible/hosts` ou um arquivo personalizado) para incluir o grupo `webservers`:

```sh
[webservers]
servidor1.example.com
servidor2.example.com
```

**Execute o playbook**:

- Use o comando `ansible-playbook` para executar o playbook:

```sh
ansible-playbook -i inventario.ini playbook.yml
```



