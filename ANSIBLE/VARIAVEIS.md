### **O que são variáveis no Ansible?**

Variáveis são valores que podem ser reutilizados em diferentes partes de um playbook. Elas ajudam a tornar os playbooks mais dinâmicos e fáceis de manter.

---

### **Passo 1: Definindo Variáveis no Playbook**

Você pode definir variáveis diretamente no playbook usando a seção `vars`.

#### Exemplo:
```SH
- hosts: all
  vars:
    http_port: 80
    http_conf: /etc/httpd/conf/httpd.conf
  tasks:
    - name: Print the HTTP port
      debug:
        msg: "The HTTP port is {{ http_port }}"
```

- Aqui, `http_port` e `http_conf` são variáveis definidas no playbook.
    
- Para usar uma variável, coloque-a entre `{{ }}`.

### **Passo 2: Usando Variáveis de Arquivos Externos**

Para organizar melhor, você pode definir variáveis em arquivos separados e incluí-los no playbook.

1. Crie um arquivo chamado `vars.yml`:
```sh
http_port: 80
http_conf: /etc/httpd/conf/httpd.conf
```
No playbook, use a diretiva `vars_files` para incluir o arquivo:

```sh
- hosts: all
  vars_files:
    - vars.yml
  tasks:
    - name: Print the HTTP port
      debug:
        msg: "The HTTP port is {{ http_port }}"
```

### **Passo 3: Variáveis no Inventário**

Você pode definir variáveis diretamente no arquivo de inventário, seja para hosts específicos ou grupos de hosts.

1. Crie um arquivo de inventário `inventory.ini`:

```sh
[webservers]
host1.example.com http_port=80
host2.example.com http_port=8080

[webservers:vars]
http_conf=/etc/httpd/conf/httpd.conf
```

No playbook, você pode acessar essas variáveis:

```sh
- hosts: webservers
  tasks:
    - name: Print the HTTP port
      debug:
        msg: "The HTTP port is {{ http_port }}"
```

### **Passo 4: Variáveis de Fato (Facts)**

O Ansible coleta automaticamente informações sobre os hosts, chamadas de "facts". Essas informações podem ser usadas como variáveis.

#### Exemplo:
```sh
- hosts: all
  tasks:
    - name: Print the OS family
      debug:
        msg: "The OS family is {{ ansible_os_family }}"
```

- Aqui, `ansible_os_family` é uma variável de fato que contém o sistema operacional do host.

### **Passo 5: Variáveis de Registro (Register)**

Você pode capturar a saída de uma tarefa e armazená-la em uma variável usando `register`.

#### Exemplo:
```sh 
- hosts: all
  tasks:
    - name: Capture the output of a command
      command: echo "Hello, World!"
      register: command_output

    - name: Print the output
      debug:
        msg: "{{ command_output.stdout }}"
```

- Aqui, `command_output` é uma variável que armazena a saída do comando `echo`.

### **Passo 6: Variáveis de Prompt**

Você pode solicitar que o usuário insira valores durante a execução do playbook usando `vars_prompt`.

#### Exemplo:
```sh
- hosts: all
  vars_prompt:
    - name: http_port
      prompt: "Enter the HTTP port"
      private: no
  tasks:
    - name: Print the HTTP port
      debug:
        msg: "The HTTP port is {{ http_port }}"
```

Quando você executar o playbook, o Ansible vai pedir para você inserir o valor de `http_port`.

### **Passo 7: Variáveis de Ambiente**

Você pode definir variáveis de ambiente para tarefas específicas.

#### Exemplo:
```sh 
- hosts: all
  tasks:
    - name: Run a script with environment variables
      shell: echo $MY_VAR
      environment:
        MY_VAR: "Hello, World!"
```

### **asso 8: Executando o Playbook**

1. Salve o playbook em um arquivo, por exemplo, `playbook.yml`.
    
2. Execute o playbook com o comando:

```sh
ansible-playbook -i inventory.ini playbook.yml
```

### **Resumo das Formas de Usar Variáveis**

|**Tipo de Variável**|**Como Usar**|
|---|---|
|**No Playbook**|Use a seção `vars`.|
|**Arquivo Externo**|Use `vars_files` para incluir um arquivo YAML com variáveis.|
|**Inventário**|Defina variáveis no arquivo de inventário.|
|**Facts**|Use variáveis coletadas automaticamente, como `ansible_os_family`.|
|**Registro (Register)**|Capture a saída de uma tarefa com `register`.|
|**Prompt**|Solicite entrada do usuário com `vars_prompt`.|
|**Ambiente**|Defina variáveis de ambiente para tarefas específicas.|