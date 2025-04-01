
#### 1. Introdução

Em ambientes gerenciados pelo Ansible, é comum encontrar problemas genéricos que podem ser resolvidos de forma automatizada. Esses problemas podem incluir configurações incorretas, serviços parados, permissões de arquivos inadequadas, entre outros. Nesta aula, vamos aprender a identificar esses problemas, criar um playbook para solucioná-los e aplicar as correções.

---

#### 2. Identificação de Problemas Genéricos

Antes de criar um playbook, é importante identificar os problemas genéricos que precisam ser resolvidos. Alguns exemplos comuns incluem:

- **Serviços parados**: Serviços essenciais que devem estar em execução.
    
- **Configurações incorretas**: Arquivos de configuração com valores inadequados.
    
- **Permissões de arquivos**: Arquivos com permissões inadequadas.
    
- **Pacotes desatualizados**: Pacotes que precisam ser atualizados.
    

**Exemplo Prático:**

Suponha que identificamos os seguintes problemas em nossos servidores:

1. O serviço Nginx está parado.
    
2. O arquivo de configuração do Nginx tem permissões inadequadas.
    
3. O pacote Nginx está desatualizado.
    

---
#### 3. Criando um Playbook para Solucionar Problemas

Vamos criar um playbook para solucionar os problemas identificados.

**Passo 1: Definir o Playbook**  
Crie um arquivo chamado `solucionar_problemas.yml`.

**solucionar_problemas.yml:**

```sh
- hosts: all
  become: yes
  tasks:
    - name: Verificar e iniciar o serviço Nginx
      service:
        name: nginx
        state: started
      when: ansible_facts.services['nginx.state'] == 'stopped'

    - name: Corrigir permissões do arquivo de configuração do Nginx
      file:
        path: /etc/nginx/nginx.conf
        owner: root
        group: root
        mode: '0644'
      when: ansible_facts.stat['/etc/nginx/nginx.conf'].mode != '0644'

    - name: Atualizar o pacote Nginx
      apt:
        name: nginx
        state: latest
        update_cache: yes
      when: ansible_facts.packages['nginx'][0].version != '1.18.0'
```

**Explicação:**

- **Verificar e iniciar o serviço Nginx**: Verifica se o serviço Nginx está parado e, se estiver, inicia-o.
    
- **Corrigir permissões do arquivo de configuração do Nginx**: Verifica se as permissões do arquivo de configuração estão incorretas e as corrige.
    
- **Atualizar o pacote Nginx**: Verifica se o pacote Nginx está desatualizado e o atualiza.

--- 

**Passo 2: Executar o Playbook**  
Execute o playbook para aplicar as correções.

```sh
ansible-playbook -i inventory solucionar_problemas.yml
```

#### 3. Verificando a Aplicação das Correções

Após executar o playbook, é importante verificar se as correções foram aplicadas corretamente.

**Exemplo de Verificação:**

```sh
ansible all -i inventory -m shell -a "systemctl status nginx"
ansible all -i inventory -m shell -a "ls -l /etc/nginx/nginx.conf"
ansible all -i inventory -m shell -a "apt list --installed | grep nginx"
```

___

**Explicação:**

- **systemctl status nginx**: Verifica o status do serviço Nginx.
    
- **ls -l /etc/nginx/nginx.conf**: Verifica as permissões do arquivo de configuração do Nginx.
    
- **apt list --installed | grep nginx**: Verifica a versão instalada do pacote Nginx.
    

#### 5. Documentando o Playbook de Solução de Problemas

Ao criar um playbook para solucionar problemas, é importante documentar no manual técnico quais problemas estão sendo resolvidos e como o playbook faz isso.

**Exemplo de Documentação:**

**Manual de Solução de Problemas**

1. **Serviço Nginx Parado**
    
    - Tarefa: Verificar e iniciar o serviço Nginx.
        
    - Condição: Quando o serviço Nginx estiver parado.
        
2. **Permissões Incorretas do Arquivo de Configuração do Nginx**
    
    - Tarefa: Corrigir permissões do arquivo de configuração do Nginx.
        
    - Condição: Quando as permissões do arquivo estiverem incorretas.
        
3. **Pacote Nginx Desatualizado**
    
    - Tarefa: Atualizar o pacote Nginx.
        
    - Condição: Quando a versão do pacote Nginx estiver desatualizada.
        

#### 6. Boas Práticas

- **Testes**: Sempre teste o playbook em um ambiente de desenvolvimento antes de aplicá-lo em produção.
    
- **Documentação**: Documente todas as tarefas e condições do playbook.
    
- **Versionamento**: Utilize versionamento para controlar as mudanças no playbook.
    

#### 7. Conclusão

Criar playbooks para solucionar problemas genéricos no Ansible é uma prática essencial para manter a saúde e a segurança dos ambientes gerenciados. Com essas técnicas, você pode identificar e corrigir problemas de forma automatizada, garantindo a consistência e a confiabilidade do ambiente.