### Exemplo Completo com Mais Detalhes



Aqui está um exemplo mais completo, com variáveis e handlers:

```sh
---
- name: Configurar servidores web
  hosts: webservers
  become: yes
  vars:
    apache_package: apache2
    apache_service: apache2
    document_root: /var/www/html

  tasks:
    - name: Instalar o Apache
      apt:
        name: "{{ apache_package }}"
        state: present

    - name: Criar arquivo de configuração personalizado
      copy:
        content: |
          <VirtualHost *:80>
              DocumentRoot {{ document_root }}
              <Directory {{ document_root }}>
                  AllowOverride All
              </Directory>
          </VirtualHost>
        dest: /etc/apache2/sites-available/custom.conf
      notify: Reiniciar Apache

    - name: Habilitar site personalizado
      file:
        src: /etc/apache2/sites-available/custom.conf
        dest: /etc/apache2/sites-enabled/custom.conf
        state: link
      notify: Reiniciar Apache

  handlers:
    - name: Reiniciar Apache
      service:
        name: "{{ apache_service }}"
        state: restarted
```

### Explicação dos Novos Itens

#### 1. **`vars:`**

- **O que é**: Define variáveis para o play.
    
- **Para que serve**: Permite reutilizar valores em várias tarefas, facilitando a manutenção.
    

#### 2. **`copy:`**

- **O que é**: Módulo para copiar arquivos ou criar arquivos com conteúdo específico.
    
- **Para que serve**: No exemplo, ele cria um arquivo de configuração personalizado para o Apache.
    

#### 3. **`notify:`**

- **O que é**: Aciona um **handler** após a tarefa ser concluída.
    
- **Para que serve**: No exemplo, ele aciona o handler para reiniciar o Apache após alterações na configuração.
    

#### 4. **`handlers:`**

- **O que é**: Tarefas que são executadas apenas quando notificadas.
    
- **Para que serve**: Útil para ações que devem ser executadas apenas após mudanças, como reiniciar um serviço.
    

---

### Resumo

Um playbook no Ansible é composto por:

- **Plays**: Definem os hosts e as tarefas a serem executadas.
    
- **Tasks**: Ações específicas a serem realizadas.
    
- **Variáveis**: Permitem personalizar e reutilizar valores.
    
- **Handlers**: Tarefas que são executadas apenas quando notificadas.
    

Com essa estrutura, você pode automatizar desde tarefas simples até configurações complexas de infraestrutura.