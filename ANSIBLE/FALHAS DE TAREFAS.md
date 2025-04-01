

#### **Introdução**

No Ansible, as tarefas são executadas sequencialmente, e se uma tarefa falhar, o playbook pode parar de executar. No entanto, há várias maneiras de **lidar com falhas** para garantir que seu playbook seja robusto e continue funcionando mesmo quando algo dá errado.

---

### **1. O que Acontece Quando uma Tarefa Falha?**

- Por padrão, se uma tarefa falha, o Ansible **interrompe a execução** do playbook.
    
- Isso pode não ser o comportamento desejado, especialmente se você quiser tentar recuperar o erro ou continuar com outras tarefas.
    

---

### **2. Estratégias para Lidar com Falhas**

#### **2.1. Ignorar Falhas com `ignore_errors`**

A opção `ignore_errors` permite que o playbook continue mesmo se uma tarefa falhar.

**Exemplo:**

```sh
- name: Tentar instalar um pacote
  ansible.builtin.yum:
    name: pacote_inexistente
    state: present
  ignore_errors: yes  # Ignora a falha e continua
```

**Quando usar?**
- Quando a falha não é crítica e você quer continuar a execução.

---

#### **2.2. Verificar Condições com `when`**

A diretiva `when` permite que uma tarefa seja executada apenas se uma condição for atendida. Isso pode evitar falhas desnecessárias.

**Exemplo:**

```sh
- name: Instalar pacote apenas se o sistema for CentOS
  ansible.builtin.yum:
    name: httpd
    state: present
  when: ansible_os_family == "RedHat"  # Só executa em sistemas Red Hat
```
**Quando usar?**
- Quando você quer evitar a execução de uma tarefa em cenários onde ela pode falhar.

___
#### **2.3. Tentar Novamente com `retries` e `until`**

Se você espera que uma tarefa possa falhar temporariamente (por exemplo, esperando um serviço ficar online), pode usar `retries` e `until` para tentar novamente.

**Exemplo:**

```sh
- name: Esperar até que o serviço esteja ativo
  ansible.builtin.command: systemctl is-active meu_servico
  register: result
  until: result.rc == 0  # Repete até que o comando retorne 0 (sucesso)
  retries: 5  # Número máximo de tentativas
  delay: 10  # Intervalo entre tentativas (em segundos)
```
**Quando usar?**
- Quando você espera que uma tarefa possa falhar temporariamente e quer tentar novamente.

___

#### **2.4. Blocos de Resgate com `block` e `rescue`**

Os blocos `block` e `rescue` permitem que você defina um conjunto de tarefas para tentar (`block`) e um conjunto de tarefas para executar se algo der errado (`rescue`).

**Exemplo:**
```sh
- name: Tentar executar tarefas críticas
  block:
    - name: Instalar pacote crítico
      ansible.builtin.yum:
        name: pacote_critico
        state: present

    - name: Iniciar serviço crítico
      ansible.builtin.service:
        name: servico_critico
        state: started

  rescue:
    - name: Lidar com falha
      ansible.builtin.debug:
        msg: "Falha ao executar tarefas críticas. Executando plano de recuperação."

    - name: Notificar administrador
      ansible.builtin.mail:
        subject: "Falha no playbook"
        body: "Ocorreu uma falha durante a execução do playbook."
        to: admin@example.com
```
**Quando usar?**
- Quando você tem tarefas críticas e quer garantir que haja um plano de recuperação em caso de falha.

___

#### **2.5. Forçar Handlers com `--force-handlers`**

Se uma tarefa falhar, os handlers notificados podem não ser executados. Use a opção `--force-handlers` para garantir que os handlers sejam executados mesmo em caso de falha.

**Exemplo:**

```sh
ansible-playbook playbook.yml --force-handlers
```
**Quando usar?**
- Quando você quer garantir que os handlers sejam executados, independentemente de falhas.

___

#### **2.6. Usar `failed_when` para Definir Falhas Personalizadas**

A diretiva `failed_when` permite que você defina condições personalizadas para considerar uma tarefa como falha.

**Exemplo:**

```sh
- name: Verificar status do serviço
  ansible.builtin.command: systemctl is-active meu_servico
  register: result
  failed_when: result.rc != 0  # Considera falha se o comando retornar código diferente de 0
```

**Quando usar?**
- Quando você quer definir critérios específicos para falhas.

--- 
#### **2.7. Usar `changed_when` para Controlar o Status de "Alterado"**

A diretiva `changed_when` permite que você defina quando uma tarefa deve ser considerada como "alterada".

**Exemplo:**

```sh
- name: Verificar status do serviço
  ansible.builtin.command: systemctl is-active meu_servico
  register: result
  changed_when: false  # Nunca considera a tarefa como "alterada"
```
**Quando usar?**
- Quando você quer evitar que uma tarefa seja considerada como "alterada" mesmo que seja executada.

___
### **3. Exemplo Completo**

Aqui está um exemplo completo de um playbook que usa várias estratégias para lidar com falhas:

```sh
- name: Playbook robusto com tratamento de falhas
  hosts: all
  tasks:
    - name: Tentar instalar um pacote
      ansible.builtin.yum:
        name: pacote_inexistente
        state: present
      ignore_errors: yes  # Ignora a falha e continua

    - name: Instalar pacote apenas se o sistema for CentOS
      ansible.builtin.yum:
        name: httpd
        state: present
      when: ansible_os_family == "RedHat"  # Só executa em sistemas Red Hat

    - name: Esperar até que o serviço esteja ativo
      ansible.builtin.command: systemctl is-active meu_servico
      register: result
      until: result.rc == 0  # Repete até que o comando retorne 0 (sucesso)
      retries: 5  # Número máximo de tentativas
      delay: 10  # Intervalo entre tentativas (em segundos)

    - name: Tentar executar tarefas críticas
      block:
        - name: Instalar pacote crítico
          ansible.builtin.yum:
            name: pacote_critico
            state: present

        - name: Iniciar serviço crítico
          ansible.builtin.service:
            name: servico_critico
            state: started

      rescue:
        - name: Lidar com falha
          ansible.builtin.debug:
            msg: "Falha ao executar tarefas críticas. Executando plano de recuperação."

        - name: Notificar administrador
          ansible.builtin.mail:
            subject: "Falha no playbook"
            body: "Ocorreu uma falha durante a execução do playbook."
            to: admin@example.com
```

### **4. Resumo**

- **`ignore_errors`**: Ignora falhas e continua a execução.
    
- **`when`**: Executa tarefas apenas se uma condição for atendida.
    
- **`retries` e `until`**: Tenta novamente até que uma condição seja atendida.
    
- **`block` e `rescue`**: Define um bloco de tarefas e um plano de recuperação em caso de falha.
    
- **`failed_when`**: Define condições personalizadas para falhas.
    
- **`changed_when`**: Controla quando uma tarefa é considerada "alterada".