
#### 1. Introdução

Durante a execução de um playbook no Ansible, é possível encontrar falhas em hosts gerenciados. Essas falhas podem ser causadas por diversos fatores, como problemas de conectividade, configurações incorretas, permissões inadequadas, entre outros. Nesta aula, vamos aprender a identificar essas falhas, solucioná-las e garantir que o playbook seja executado com sucesso.

---
#### 2. Identificação de Falhas

O Ansible fornece feedback detalhado sobre a execução de playbooks, incluindo informações sobre falhas. Ao executar um playbook, você pode identificar falhas observando a saída do comando `ansible-playbook`.

**Exemplo de Saída com Falha:**

```sh
TASK [Install Nginx] ***********************************************************
fatal: [host1]: FAILED! => {"changed": false, "msg": "No package matching 'nginx' is available"}
```

**Explicação:**

- **TASK [Install Nginx]**: A tarefa que falhou.
    
- **fatal: [host1]**: O host onde a falha ocorreu.
    
- **FAILED!**: Indica que a tarefa falhou.
    
- **msg**: Mensagem de erro detalhada.
    

---
#### 3. Solução de Problemas Comuns

Vamos abordar alguns problemas comuns e como solucioná-los.

**Problema 1: Falha na Instalação de Pacotes**

- **Mensagem de Erro**: `No package matching 'nginx' is available`
    
- **Causa**: O pacote não está disponível nos repositórios configurados.
    
- **Solução**: Atualizar a lista de pacotes ou adicionar repositórios adicionais.
    

**Exemplo de Correção:**

```sh
- name: Atualizar lista de pacotes
  apt:
    update_cache: yes

- name: Instalar Nginx
  apt:
    name: nginx
    state: present
```

---
**Problema 2: Falha na Conexão com o Host**

- **Mensagem de Erro**: `Failed to connect to the host via ssh: Connection timed out`
    
- **Causa**: Problemas de conectividade SSH.
    
- **Solução**: Verificar a conectividade com o host, credenciais SSH e configurações de firewall.
    

**Exemplo de Verificação:**

```sh
ssh user@host1
```

---
**Problema 3: Permissões Insuficientes**

- **Mensagem de Erro**: `Permission denied`
    
- **Causa**: O usuário não tem permissões suficientes para executar a tarefa.
    
- **Solução**: Utilizar `become: yes` para elevar privilégios.
    

**Exemplo de Correção:**

```sh
- name: Reiniciar o serviço Nginx
  become: yes
  service:
    name: nginx
    state: restarted
```
---

#### 4. Utilizando Blocos de Resgate (Rescue Blocks)

O Ansible permite o uso de blocos de resgate (`rescue`) para lidar com falhas durante a execução de tarefas. Isso é útil para tentar uma ação alternativa ou realizar uma limpeza em caso de falha.

**Exemplo de Uso de Blocos de Resgate:**

```sh
- hosts: all
  tasks:
    - block:
        - name: Tentar instalar o Nginx
          apt:
            name: nginx
            state: present
      rescue:
        - name: Instalar Nginx a partir de um pacote local
          apt:
            deb: /tmp/nginx.deb
      always:
        - name: Verificar se o Nginx está instalado
          command: nginx -v
          register: nginx_version
          ignore_errors: yes

        - debug:
            msg: "Versão do Nginx: {{ nginx_version.stdout }}"
```

**Explicação:**

- **block**: Tarefas que serão executadas normalmente.
    
- **rescue**: Tarefas que serão executadas em caso de falha no bloco.
    
- **always**: Tarefas que serão executadas independentemente de falhas.
    

--- 
#### 5. Verificando e Corrigindo Falhas em Hosts Específicos

Se um playbook falhar em um host específico, você pode reexecutar o playbook apenas para esse host.

**Exemplo de Reexecução para um Host Específico:**

```sh
ansible-playbook -i inventory playbook.yml --limit host1
```
**Explicação:**

- **--limit host1**: Limita a execução do playbook ao host `host1`.

#### 6. Documentando a Solução de Problemas

Ao solucionar problemas de falhas em hosts gerenciados, é importante documentar as falhas encontradas e as correções aplicadas.

**Exemplo de Documentação:**

**Manual de Solução de Problemas**

1. **Falha na Instalação de Pacotes**
    
    - **Problema**: `No package matching 'nginx' is available`
        
    - **Solução**: Atualizar a lista de pacotes antes da instalação.
        
2. **Falha na Conexão com o Host**
    
    - **Problema**: `Failed to connect to the host via ssh: Connection timed out`
        
    - **Solução**: Verificar conectividade SSH e configurações de firewall.
        
3. **Permissões Insuficientes**
    
    - **Problema**: `Permission denied`
        
    - **Solução**: Utilizar `become: yes` para elevar privilégios.
        

#### 7. Boas Práticas

- **Testes**: Sempre teste o playbook em um ambiente de desenvolvimento antes de aplicá-lo em produção.
    
- **Documentação**: Documente todas as falhas e correções aplicadas.
    
- **Monitoramento**: Monitore a execução dos playbooks para identificar e solucionar falhas rapidamente.
    

#### 8. Conclusão

Solucionar problemas de falhas em hosts gerenciados ao executar um playbook no Ansible é uma prática essencial para garantir a continuidade e a confiabilidade das operações. Com essas técnicas, você pode identificar, solucionar e documentar falhas de forma eficiente.