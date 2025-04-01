
### 1. Introdução

A administração de sistemas Linux envolve tarefas como:

- Gerenciar serviços (iniciar, parar, reiniciar, habilitar, desabilitar).
    
- Agendar tarefas com `cron` e `systemd`.
    
- Reinicializar hosts e controlar o destino de inicialização padrão.
    

O Ansible permite automatizar essas tarefas, garantindo consistência e eficiência em todos os hosts gerenciados.

---

### 2. Gerenciamento de Serviços com Systemd

O `systemd` é o sistema de inicialização padrão na maioria das distribuições Linux modernas. Vamos aprender a gerenciar serviços com o módulo `systemd` do Ansible.

#### Tarefa 1: Iniciar e Habilitar um Serviço

Vamos iniciar e habilitar o serviço `nginx` para que ele seja executado automaticamente na inicialização.

**playbook_manage_service.yml:**

```sh
- hosts: webservers
  become: yes  # Executar como superusuário
  tasks:
    - name: Iniciar e habilitar o serviço Nginx
      systemd:
        name: nginx
        state: started
        enabled: yes
```

**Executar o playbook:**

```sh
ansible-playbook -i inventory playbook_manage_service.yml
```

**Explicação:**

- `name`: Nome do serviço.
    
- `state: started`: Garante que o serviço esteja em execução.
    
- `enabled: yes`: Habilita o serviço para iniciar automaticamente na inicialização.

---

#### Tarefa 2: Parar e Desabilitar um Serviço

Vamos parar e desabilitar o serviço `nginx`.

**playbook_stop_service.yml:**

```
- hosts: webservers
  become: yes
  tasks:
    - name: Parar e desabilitar o serviço Nginx
      systemd:
        name: nginx
        state: stopped
        enabled: no
```

**Executar o playbook:**

```sh
ansible-playbook -i inventory playbook_stop_service.yml
```

**Explicação:**

- `state: stopped`: Garante que o serviço esteja parado.
    
- `enabled: no`: Desabilita o serviço para não iniciar automaticamente na inicialização.

---

### 3. Agendamento de Processos com Cron

O `cron` é uma ferramenta para agendar tarefas recorrentes. Vamos aprender a gerenciar tarefas agendadas com o módulo `cron` do Ansible.

#### Tarefa 3: Adicionar uma Tarefa Cron

Vamos agendar uma tarefa para fazer backup de um diretório a cada dia às 2h.

**playbook_add_cron_job.yml:**

```sh
- hosts: all
  become: yes
  tasks:
    - name: Agendar backup diário
      cron:
        name: "Backup diário"
        minute: "0"
        hour: "2"
        job: "tar -czf /backup/backup.tar.gz /dados"
```

**Executar o playbook:**

```sh
ansible-playbook -i inventory playbook_add_cron_job.yml
```

**Explicação:**

- `name`: Nome descritivo da tarefa.
    
- `minute` e `hour`: Define o horário da tarefa.
    
- `job`: Comando a ser executado.

----

#### Tarefa 4: Remover uma Tarefa Cron

Vamos remover a tarefa de backup agendada.

**playbook_remove_cron_job.yml:**

```sh
- hosts: all
  become: yes
  tasks:
    - name: Remover tarefa de backup
      cron:
        name: "Backup diário"
        state: absent
```

**Executar o playbook:**

```sh
ansible-playbook -i inventory playbook_remove_cron_job.yml
```

**Explicação:**

- `state: absent`: Remove a tarefa agendada.

---

### 4. Reinicialização de Hosts Gerenciados

Reinicializar hosts é uma tarefa comum após atualizações ou mudanças de configuração.

#### Tarefa 5: Reinicializar Hosts

Vamos reinicializar todos os hosts gerenciados.

**playbook_reboot_hosts.yml:**

```sh
- hosts: all
  become: yes
  tasks:
    - name: Reinicializar hosts
      reboot:
        reboot_timeout: 600  # Tempo máximo de espera (em segundos)
```

**Executar o playbook:**

```sh
ansible-playbook -i inventory playbook_reboot_hosts.yml
```

**Explicação:**

- `reboot_timeout`: Define o tempo máximo de espera para a reinicialização.

----

### 5. Controle do Destino de Inicialização Padrão

O destino de inicialização padrão (`default target`) define o estado inicial do sistema após a inicialização. Vamos aprender a configurá-lo.

#### Tarefa 6: Definir o Destino de Inicialização Padrão

Vamos definir o destino de inicialização padrão como `multi-user.target` (modo sem interface gráfica).

**playbook_set_default_target.yml:**

```sh
- hosts: all
  become: yes
  tasks:
    - name: Definir destino de inicialização padrão
      systemd:
        name: multi-user.target
        enabled: yes
        state: started
```

**Executar o playbook:**

```sh
ansible-playbook -i inventory playbook_set_default_target.yml
```

**Explicação:**

- `name`: Nome do destino de inicialização.
    
- `enabled: yes`: Define o destino como padrão.
    
- `state: started`: Garante que o destino esteja ativo.

---

### 6. Documentação das Tarefas

Documentar as tarefas automatizadas é essencial para a manutenção e o entendimento do sistema.

**Exemplo de Documentação:**

**Manual de Gerenciamento de Serviços, Cron e Reinicialização**

1. **Gerenciamento de Serviços**
    
    - Playbook: `playbook_manage_service.yml`
        
    - Tarefas:
        
        - Iniciar e habilitar o serviço `nginx`.
            
2. **Agendamento de Tarefas com Cron**
    
    - Playbook: `playbook_add_cron_job.yml`
        
    - Tarefas:
        
        - Agendar backup diário.
            
3. **Reinicialização de Hosts**
    
    - Playbook: `playbook_reboot_hosts.yml`
        
    - Tarefas:
        
        - Reinicializar todos os hosts.
            
4. **Controle do Destino de Inicialização**
    
    - Playbook: `playbook_set_default_target.yml`
        
    - Tarefas:
        
        - Definir o destino de inicialização padrão como `multi-user.target`.
            

---

### 7. Boas Práticas

- **Testes**: Sempre teste os playbooks em um ambiente de desenvolvimento antes de aplicá-los em produção.
    
- **Documentação**: Documente todas as tarefas e configurações.
    
- **Segurança**: Use o `cron` e o `systemd` com cuidado para evitar execuções indesejadas.
    

---

### 8. Conclusão

Nesta aula, aprendemos a:

- Gerenciar serviços com `systemd`.
    
- Agendar tarefas com `cron`.
    
- Reinicializar hosts gerenciados.
    
- Controlar o destino de inicialização padrão.
    

Com essas técnicas, você pode automatizar a administração de serviços, agendamento de tarefas e reinicialização de hosts com o Ansible, garantindo consistência e eficiência.