### 1. **O que são Fatos no Ansible?**

Fatos são variáveis automáticas que o Ansible coleta dos hosts gerenciados. Eles são gerados pelo módulo `setup`, que é executado automaticamente no início de um playbook, a menos que seja desativado.

Exemplos de fatos:

- `ansible_facts['os_family']`: Família do sistema operacional (ex: "RedHat", "Debian").
    
- `ansible_facts['hostname']`: Nome do host.
    
- `ansible_facts['memory']['total']`: Memória total do sistema.
    
- `ansible_facts['interfaces']`: Lista de interfaces de rede.


### 2. **Como os Fatos são Coletados?**

O Ansible usa o módulo `setup` para coletar fatos. Esse módulo é executado automaticamente no início de um playbook, a menos que você desative essa funcionalidade.

- **Coleta automática de fatos**:
    
    - Quando você executa um playbook, o Ansible coleta fatos de todos os hosts antes de executar as tarefas.
        
    - Exemplo de playbook:

```sh
- hosts: all
  tasks:
    - name: Exibir o nome do host
      debug:
        msg: "O nome do host é {{ ansible_facts['hostname'] }}"
```

**Coleta manual de fatos**:

- Você pode coletar fatos manualmente usando o módulo `setup`:

```sh
- hosts: all
  tasks:
    - name: Coletar fatos manualmente
      setup:
```

### 3. **Desativar a Coleta Automática de Fatos**

Se você não precisa dos fatos e deseja melhorar o desempenho, pode desativar a coleta automática de fatos no playbook:

```sh
- hosts: all
  gather_facts: no
  tasks:
    - name: Tarefa sem coleta de fatos
      debug:
        msg: "Fatos não coletados"
```

**Usando variáveis diretas** (legado):

- Em versões mais antigas ou em alguns casos, os fatos podem ser acessados diretamente como variáveis.
    
- Exemplo:

```sh
- name: Exibir o nome do host
  debug:
    msg: "O nome do host é {{ ansible_hostname }}"
```

###  **Fatos Personalizados (Custom Facts)**

Você pode criar fatos personalizados para seus hosts. Esses fatos são definidos em arquivos `.fact` no diretório `/etc/ansible/facts.d/` do host remoto.

- **Exemplo de fato personalizado**:
    
    - No host remoto, crie um arquivo `/etc/ansible/facts.d/custom.fact`:


```sh
{
  "app_version": "1.2.3",
  "environment": "production"
}
```

No playbook, você pode acessar esses fatos personalizados:

```sh
- name: Exibir fato personalizado
  debug:
    msg: "A versão do app é {{ ansible_facts['local']['custom']['app_version'] }}"
```

### **Cache de Fatos**

Para melhorar o desempenho em ambientes grandes, você pode habilitar o cache de fatos. Isso armazena os fatos coletados em um local central (como um banco de dados ou arquivo JSON) para reutilização.

- **Exemplo de configuração de cache**:
    
    - No arquivo `ansible.cfg`, adicione:

```sh
[defaults]
gathering = smart
fact_caching = jsonfile
fact_caching_connection = /tmp/ansible_facts
```

### 7. **Fatos Especiais**

Além dos fatos coletados pelo módulo `setup`, o Ansible também fornece fatos especiais, como:

- `ansible_play_hosts`: Lista de hosts no play atual.
    
- `ansible_version`: Versão do Ansible em execução.


### 8. **Exemplo Completo de Playbook com Fatos**

Aqui está um exemplo de playbook que usa fatos para tomar decisões:

```sh
- hosts: all
  gather_facts: yes
  tasks:
    - name: Exibir informações do sistema
      debug:
        msg: |
          Host: {{ ansible_facts['hostname'] }}
          OS: {{ ansible_facts['os_family'] }}
          Memória Total: {{ ansible_facts['memory']['total'] }}

    - name: Instalar pacote específico para RedHat
      yum:
        name: httpd
        state: present
      when: ansible_facts['os_family'] == "RedHat"

    - name: Instalar pacote específico para Debian
      apt:
        name: apache2
        state: present
      when: ansible_facts['os_family'] == "Debian"
```