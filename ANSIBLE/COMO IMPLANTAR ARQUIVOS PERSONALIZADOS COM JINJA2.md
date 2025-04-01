

### **1. O que é Jinja2?**

- **Jinja2** é um mecanismo de templates em Python.
    
- Ele permite criar arquivos de texto (como arquivos de configuração) com placeholders que são substituídos por valores reais durante a execução do playbook.
    
- No Ansible, o módulo `template` é usado para processar templates Jinja2.
    

---

### **2. Criando um Template Jinja2**

Um template Jinja2 é um arquivo de texto com placeholders (variáveis) que serão substituídos por valores durante a execução do playbook.

#### **Exemplo de Template: `config.conf.j2`**

```sh
# config.conf.j2
server_name {{ server_name }};
port {{ port }};

# Lista de IPs permitidos
{% for ip in allowed_ips %}
allow {{ ip }};
{% endfor %}
```
**O que isso faz?**

- `{{ server_name }}` e `{{ port }}` são variáveis que serão substituídas por valores.
    
- O loop `{% for ip in allowed_ips %}` gera uma lista de IPs permitidos.

--- 
### **3. Usando o Módulo `template`**

O módulo `template` processa o template Jinja2 e cria um arquivo no host remoto com os valores substituídos.

#### **Exemplo de Playbook**

```sh
- name: Implantar arquivo de configuração personalizado
  hosts: all
  vars:
    server_name: "meu_servidor"
    port: 8080
    allowed_ips:
      - 192.168.1.1
      - 192.168.1.2
      - 192.168.1.3
  tasks:
    - name: Criar arquivo de configuração dinâmico
      ansible.builtin.template:
        src: /caminho/local/config.conf.j2
        dest: /etc/meu_app/config.conf
        owner: root
        group: root
        mode: '0644'
```

**O que isso faz?**

- Processa o template `config.conf.j2` e cria o arquivo `/etc/meu_app/config.conf` no host remoto.
    
- Substitui as variáveis `server_name`, `port` e `allowed_ips` pelos valores definidos no playbook.

--- 

### **4. Estrutura do Template Jinja2**

#### **4.1. Variáveis**

As variáveis são substituídas por valores usando `{{ variavel }}`.

**Exemplo:**
```sh
server_name {{ server_name }};
```

#### **4.2. Condicionais (`if`)**

Você pode usar condicionais para incluir ou excluir partes do template com base em condições.

**Exemplo:**
```sh
{% if enable_logging %}
log_level debug;
{% endif %}
```

#### **4.3. Loops (`for`)**

Loops permitem gerar listas ou blocos repetidos.

**Exemplo:**
```sh
{% for ip in allowed_ips %}
allow {{ ip }};
{% endfor %}
```

#### **4.4. Comentários**

Comentários em Jinja2 são ignorados durante o processamento.

**Exemplo:**
```sh
{# Este é um comentário #}
```
--- 
### **5. Exemplo Completo de Playbook com Template**

Aqui está um exemplo completo de um playbook que usa um template Jinja2 para criar um arquivo de configuração personalizado:

```sh
- name: Implantar arquivo de configuração personalizado
  hosts: all
  vars:
    server_name: "meu_servidor"
    port: 8080
    enable_logging: true
    allowed_ips:
      - 192.168.1.1
      - 192.168.1.2
      - 192.168.1.3
  tasks:
    - name: Criar arquivo de configuração dinâmico
      ansible.builtin.template:
        src: /caminho/local/config.conf.j2
        dest: /etc/meu_app/config.conf
        owner: root
        group: root
        mode: '0644'
```

**Template: `config.conf.j2`**

```sh
# config.conf.j2
server_name {{ server_name }};
port {{ port }};

{% if enable_logging %}
log_level debug;
{% endif %}

# Lista de IPs permitidos
{% for ip in allowed_ips %}
allow {{ ip }};
{% endfor %}
```

**Arquivo Gerado: `/etc/meu_app/config.conf`**

```sh
server_name meu_servidor;
port 8080;

log_level debug;

# Lista de IPs permitidos
allow 192.168.1.1;
allow 192.168.1.2;
allow 192.168.1.3;
```

----

### **6. Dicas Avançadas**

#### **6.1. Usando Filtros**

Jinja2 suporta filtros para manipular variáveis. Por exemplo, você pode converter uma string para maiúsculas:

```sh
server_name {{ server_name | upper }};
```
#### **6.2. Incluindo Outros Templates**

Você pode incluir outros templates dentro de um template usando `{% include 'outro_template.j2' %}`.

#### **6.3. Definindo Variáveis no Template**

Você pode definir variáveis diretamente no template:

```sh
{% set timeout = 60 %}
timeout {{ timeout }};
```
---
### **7. Resumo**

- **Jinja2** é uma ferramenta poderosa para criar arquivos de configuração dinâmicos.
    
- Use o módulo `template` para processar templates e criar arquivos personalizados.
    
- Variáveis, condicionais e loops permitem criar templates flexíveis e reutilizáveis.