
#### 1. Introdução

No Ansible, **funções (roles)** são uma maneira de organizar e reutilizar código. Muitas vezes, em vez de criar tudo do zero, podemos aproveitar funções já existentes disponíveis em repositórios Git ou na Galáxia Ansible. Isso acelera o desenvolvimento e garante que estamos utilizando soluções testadas e aprovadas pela comunidade.

___

#### 2. Selecionando Funções da Galáxia Ansible

A **Galáxia Ansible** é um repositório centralizado onde você pode encontrar e compartilhar funções criadas pela comunidade. Para selecionar uma função da Galáxia:

1. **Acesse o site da Galáxia Ansible**: [https://galaxy.ansible.com](https://galaxy.ansible.com/)
    
2. **Pesquise por uma função**: Por exemplo, se você precisa de uma função para instalar o Nginx, pesquise por "nginx".
    
3. **Escolha uma função**: Analise a descrição, avaliações e documentação da função para garantir que ela atenda às suas necessidades.
    

**Exemplo Prático:**

Suponha que você encontrou a função `geerlingguy.nginx` na Galáxia Ansible e deseja utilizá-la.

___

#### 3. Recuperando Funções da Galáxia Ansible

Para utilizar uma função da Galáxia Ansible, você precisa instalá-la em seu projeto. Isso pode ser feito usando o comando `ansible-galaxy`.

**Instalando uma Função:**

```sh
ansible-galaxy install geerlingguy.nginx
```

Isso baixará a função para o diretório `roles` do seu projeto.

**Estrutura do Projeto Após Instalação:**

```sh
meu_projeto/
├── roles/
│   └── geerlingguy.nginx/
├── playbook.yml
└── inventory
```
____

#### 4. Utilizando Funções em Seus Manuais

Após instalar a função, você pode referenciá-la em seus playbooks.

**Exemplo de Playbook:**

```sh
- hosts: webservers
  roles:
    - role: geerlingguy.nginx
```
**Explicação:**

- `hosts`: Define os servidores onde o playbook será executado.
    
- `roles`: Lista as funções que serão aplicadas. Neste caso, a função `geerlingguy.nginx`.
___

#### 5. Selecionando Funções de Repositórios Git

Além da Galáxia Ansible, você também pode utilizar funções disponíveis em repositórios Git. Isso é útil quando você precisa de uma função específica que não está disponível na Galáxia.

**Exemplo Prático:**

Suponha que você encontrou uma função no GitHub: `https://github.com/exemplo/ansible-role-nginx.git`.
___

#### 6. Recuperando Funções de Repositórios Git

Para instalar uma função diretamente de um repositório Git, você pode usar o comando `ansible-galaxy` com a opção `install` e o URL do repositório.

**Instalando uma Função do Git:**

```sh
ansible-galaxy install git+https://github.com/exemplo/ansible-role-nginx.git
```

Isso baixará a função para o diretório `roles` do seu projeto.

**Estrutura do Projeto Após Instalação:**

```sh
meu_projeto/
├── roles/
│   └── ansible-role-nginx/
├── playbook.yml
└── inventory
```

___

#### 7. Utilizando Funções de Repositórios Git em Seus Manuais

Assim como com funções da Galáxia, você pode referenciar a função instalada do Git em seus playbooks.

**Exemplo de Playbook:**

```sh
- hosts: webservers
  roles:
    - role: ansible-role-nginx
```

**Explicação:**

- `hosts`: Define os servidores onde o playbook será executado.
    
- `roles`: Lista as funções que serão aplicadas. Neste caso, a função `ansible-role-nginx`.
    

#### 8. Documentando o Uso de Funções em Manuais Técnicos

Ao utilizar funções de fontes externas, é importante documentar no manual técnico quais funções estão sendo utilizadas, de onde foram obtidas e como estão sendo configuradas.

**Exemplo de Documentação:**

**Manual de Configuração do Servidor Web**

1. **Instalação do Nginx**
    
    - Função: `geerlingguy.nginx`
        
    - Fonte: Galáxia Ansible
        
    - Configurações:
        
        - `nginx_conf_path: /etc/nginx/nginx.conf`
            
        - `nginx_vhosts: []`
            
2. **Configuração do Virtual Host**
    
    - Função: `ansible-role-nginx`
        
    - Fonte: Repositório Git `https://github.com/exemplo/ansible-role-nginx.git`
        
    - Configurações:
        
        - `vhost_name: meu_site`
            
        - `vhost_root: /var/www/meu_site`
            

#### 9. Boas Práticas

- **Verificação**: Sempre verifique a qualidade e a confiabilidade das funções antes de utilizá-las.
    
- **Documentação**: Documente todas as funções utilizadas, incluindo suas fontes e configurações.
    
- **Versionamento**: Utilize versionamento para controlar as mudanças nas funções e garantir a consistência do ambiente.