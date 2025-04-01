### **Estrutura de Diretórios**

Uma estrutura de diretórios bem organizada é essencial para manter seus arquivos de configuração do Ansible gerenciáveis. Aqui está um exemplo de estrutura comum:

```sh
ansible-project/
├── inventory/
│   ├── production
│   ├── staging
│   └── group_vars/
│       ├── all
│       ├── group1
│       └── group2
├── roles/
│   ├── common/
│   │   ├── tasks/
│   │   ├── handlers/
│   │   ├── templates/
│   │   ├── files/
│   │   ├── vars/
│   │   └── meta/
│   └── webserver/
│       ├── tasks/
│       ├── handlers/
│       ├── templates/
│       ├── files/
│       ├── vars/
│       └── meta/
├── playbooks/
│   ├── site.yml
│   ├── webserver.yml
│   └── database.yml
├── ansible.cfg
└── requirements.yml
```

- **inventory/**: Contém os arquivos de inventário para diferentes ambientes (produção, staging, etc.).
    
- **group_vars/**: Variáveis específicas para grupos de hosts.
    
- **roles/**: Roles são unidades reutilizáveis de configuração. Cada role pode conter tasks, handlers, templates, etc.
    
- **playbooks/**: Playbooks principais que orquestram a execução das roles.
    
- **ansible.cfg**: Arquivo de configuração do Ansible.
    
- **requirements.yml**: Lista de roles externas necessárias para o projeto.

### **Inventários Dinâmicos**

Para ambientes dinâmicos, como clouds, você pode usar inventários dinâmicos que geram a lista de hosts em tempo de execução. Isso pode ser feito usando scripts ou plugins específicos para AWS, Azure, Google Cloud, etc.

### 3. **Uso de Variáveis**

- **group_vars/**: Variáveis específicas para grupos de hosts.
    
- **host_vars/**: Variáveis específicas para hosts individuais.
    
- **defaults/**: Variáveis padrão dentro de uma role.
    
- **vars/**: Variáveis específicas dentro de uma role.

Exemplo de `group_vars/all`:

```sh
http_port: 80
max_clients: 200
```

### 4. **Roles**

Roles permitem que você modularize e reutilize configurações. Cada role deve ser auto-contida e focada em uma tarefa específica, como configurar um servidor web ou um banco de dados.

Exemplo de estrutura de uma role:

```Sh
roles/
└── common/
    ├── tasks/
    │   └── main.yml
    ├── handlers/
    │   └── main.yml
    ├── templates/
    │   └── nginx.conf.j2
    ├── files/
    ├── vars/
    │   └── main.yml
    └── meta/
        └── main.yml
```


### **Playbooks**

Playbooks são usados para orquestrar a execução de roles e tasks. Eles devem ser claros e concisos, referenciando roles e variáveis de forma organizada.

Exemplo de `playbooks/site.yml`:

```sh
- hosts: webservers
  roles:
    - common
    - webserver
```

###  **Ansible Vault**

Para gerenciar informações sensíveis, como senhas e chaves, use o Ansible Vault. Ele permite criptografar arquivos e variáveis.

Exemplo de uso:

```Sh
ansible-vault create secrets.yml
ansible-vault edit secrets.yml
```

Para usar um arquivo criptografado em um playbook:

```sh 
- hosts: all
  vars_files:
    - secrets.yml
  tasks:
    - name: Ensure the secret is present
      debug:
        msg: "{{ secret_key }}"
```

### **Versionamento**

Use um sistema de controle de versão, como Git, para gerenciar seus arquivos de configuração do Ansible. Isso permite rastrear mudanças, colaborar com outros desenvolvedores e reverter alterações, se necessário.

### 8. **Documentação**

Mantenha uma documentação clara e atualizada sobre a estrutura do projeto, como os arquivos estão organizados e como executar os playbooks. Isso é especialmente útil para novos membros da equipe.

### 9. **Testes**

Use ferramentas como `molecule` para testar suas roles e playbooks em diferentes cenários e ambientes. Isso ajuda a garantir que suas configurações funcionem conforme o esperado.

### 10. **Integração Contínua**

Integre seus playbooks em um pipeline de CI/CD para automatizar a execução de testes e deploy em diferentes ambientes.

### Exemplo de Execução

Para executar um playbook:

```sh 
ansible-playbook -i inventory/production playbooks/site.yml
```

Para executar um playbook com um arquivo criptografado:

```sh
ansible-playbook -i inventory/production playbooks/site.yml --ask-vault-pass
```

