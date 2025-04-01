O **inventário** no Ansible é um componente fundamental que define os hosts e grupos de hosts onde as playbooks e comandos ad-hoc serão executados. Ele serve como uma lista de máquinas (servidores, dispositivos, etc.) que o Ansible gerencia, permitindo a organização e categorização desses recursos.

#### Tipos de Inventário

1. **Inventário Estático**: Um arquivo de texto (geralmente em formato INI ou YAML) que lista os hosts e grupos manualmente.
    
    - Exemplo em formato INI:

```sh
"[webservers]
web1.example.com
web2.example.com

[dbservers]
db1.example.com
db2.example.com"
```

Exemplo em formato YAML:

```sh
  "all:
  hosts:
    web1.example.com:
    web2.example.com:
  children:
    webservers:
      hosts:
        web1.example.com:
        web2.example.com:
    dbservers:
      hosts:
        db1.example.com:
        db2.example.com:"

```

1. **Inventário Dinâmico**: Um script ou programa que gera a lista de hosts em tempo de execução, geralmente integrado com sistemas de cloud (AWS, Azure, GCP) ou outras fontes dinâmicas.
    
    - Exemplo: Um script em Python que consulta a API da AWS para listar instâncias EC2.
        

#### Estrutura do Inventário

- **Hosts**: Máquinas individuais, identificadas por IP ou nome de domínio.
    
- **Grupos**: Coleções de hosts que podem ser referenciados como uma unidade. Por exemplo, `webservers` ou `dbservers`.
    
- **Variáveis**: Podem ser atribuídas a hosts ou grupos para personalizar o comportamento das playbooks.
    
    - Exemplo:
```sh
'[webservers]
web1.example.com ansible_user=admin
web2.example.com ansible_user=deploy'

```


#### Funcionamento

1. **Leitura do Inventário**: O Ansible lê o arquivo de inventário (ou executa o script dinâmico) para obter a lista de hosts e grupos.
    
2. **Execução de Playbooks**: As playbooks são aplicadas aos hosts ou grupos definidos no inventário.
    
3. **Uso de Variáveis**: As variáveis definidas no inventário podem ser usadas para personalizar tarefas, como credenciais de acesso, caminhos de arquivos, etc.
    
4. **Gerenciamento de Hosts**: O Ansible usa o inventário para se conectar aos hosts via SSH 
5. (ou outros métodos) e executar as tarefas.

6. Comando para listar hosts em um grupo:

```sh
ansible-inventory -i inventario.ini --list
```

Executar uma playbook em um grupo específico:
```sh
ansible-playbook -i inventario.ini playbook.yml -l webservers
```
