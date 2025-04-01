
### **Aula: Como Funcionam os Loops no Ansible**

#### **Introdução**

No Ansible, os **loops** são usados para repetir uma tarefa várias vezes, mas com valores diferentes a cada iteração. Isso é muito útil quando você precisa executar a mesma ação para vários itens, como criar vários usuários, instalar vários pacotes ou configurar vários arquivos.

Imagine que você tem uma lista de tarefas repetitivas. Em vez de escrever a mesma tarefa várias vezes no playbook, você pode usar um loop para simplificar o código.

---

### **1. O Básico: O que é um Loop?**

Um loop é uma estrutura que repete uma tarefa para cada item em uma lista. No Ansible, a forma mais comum de criar um loop é usando a diretiva **`loop`**.

#### **Exemplo Prático: Criando Vários Usuários**

Suponha que você queira criar três usuários em um servidor. Em vez de escrever três tarefas separadas, você pode usar um loop:
```sh
- name: Criar usuários
  hosts: all
  tasks:
    - name: Adicionar usuário
      user:
        name: "{{ item }}"  # O valor de 'item' muda a cada iteração
        state: present
      loop:
        - usuario1
        - usuario2
        - usuario3
```

**O que acontece aqui?**

1. A tarefa `user` é executada três vezes.
    
2. A cada iteração, o valor de `{{ item }}` muda:
    
    - Na primeira iteração, `item = usuario1`.
        
    - Na segunda iteração, `item = usuario2`.
        
    - Na terceira iteração, `item = usuario3`.


### **2. Loops com Listas de Dicionários**

Às vezes, você precisa passar mais de um valor para cada iteração. Por exemplo, ao criar usuários, você pode querer definir um nome e um UID (ID do usuário). Para isso, usamos uma **lista de dicionários**.

#### **Exemplo: Criando Usuários com Nome e UID**

```sh
- name: Criar usuários com UID específico
  hosts: all
  tasks:
    - name: Adicionar usuário
      user:
        name: "{{ item.name }}"
        uid: "{{ item.uid }}"
        state: present
      loop:
        - { name: 'usuario1', uid: 1001 }
        - { name: 'usuario2', uid: 1002 }
        - { name: 'usuario3', uid: 1003 }
```

**Como funciona?**

1. Cada item no loop é um dicionário com duas chaves: `name` e `uid`.
    
2. Na primeira iteração:
    
    - `item.name = usuario1`
        
    - `item.uid = 1001`
        
3. Na segunda iteração:
    
    - `item.name = usuario2`
        
    - `item.uid = 1002`
        
4. E assim por diante.


### **Loops com `with_items` (Forma Antiga)**

Antes do Ansible 2.5, a forma mais comum de criar loops era usando **`with_items`**. Ainda funciona, mas a recomendação atual é usar **`loop`**.

#### **Exemplo: Criando Usuários com `with_items`**

```sh
- name: Criar usuários (usando with_items)
  hosts: all
  tasks:
    - name: Adicionar usuário
      user:
        name: "{{ item }}"
        state: present
      with_items:
        - usuario1
        - usuario2
        - usuario3
```

**Diferença entre `loop` e `with_items`:**

- `loop` é mais moderno e recomendado.
    
- `with_items` é legado, mas ainda funciona.


### **4. Loops com Condições (`until`)**

Às vezes, você quer repetir uma tarefa até que uma condição seja atendida. Para isso, usamos **`until`**.

#### **Exemplo: Esperar até que um Serviço Esteja Ativo**

```sh
- name: Esperar até que o serviço esteja ativo
  hosts: all
  tasks:
    - name: Verificar status do serviço
      shell: systemctl is-active meu_servico
      register: result  # Armazena o resultado do comando
      until: result.rc == 0  # Repete até que o comando retorne 0 (sucesso)
      retries: 5  # Número máximo de tentativas
      delay: 10  # Intervalo entre tentativas (em segundos)
```

**O que acontece aqui?**

1. O comando `systemctl is-active meu_servico` é executado.
    
2. Se o comando falhar (retorno diferente de 0), a tarefa é repetida.
    
3. O loop para quando o comando retornar 0 (sucesso) ou após 5 tentativas.


### **5. Loops com `with_dict` (Iterando sobre Dicionários)**

Se você tem um dicionário e quer iterar sobre suas chaves e valores, use **`with_dict`**.

#### **Exemplo: Configurar Variáveis de Ambiente**

```sh
- name: Configurar variáveis de ambiente
  hosts: all
  tasks:
    - name: Definir variáveis
      lineinfile:
        path: /etc/environment
        line: "{{ item.key }}={{ item.value }}"
      with_dict:
        VAR1: valor1
        VAR2: valor2
        VAR3: valor3
```

**Como funciona?**

1. Cada item no loop tem duas partes: `item.key` e `item.value`.
    
2. Na primeira iteração:
    
    - `item.key = VAR1`
        
    - `item.value = valor1`
        
3. Na segunda iteração:
    
    - `item.key = VAR2`
        
    - `item.value = valor2`
        
4. E assim por diante.


### **6. Loops com `with_sequence` (Iterando sobre Números)**

Se você precisa iterar sobre uma sequência numérica, use **`with_sequence`**.

#### **Exemplo: Criar Diretórios Numerados**

```sh
- name: Criar diretórios numerados
  hosts: all
  tasks:
    - name: Criar diretório
      file:
        path: "/tmp/dir{{ item }}"
        state: directory
      with_sequence: start=1 end=5
```

**O que acontece?**

1. O loop cria diretórios de `/tmp/dir1` até `/tmp/dir5`.
    
2. `item` assume os valores 1, 2, 3, 4 e 5.

### **7. Loops com `with_nested` (Produto Cartesiano)**

Se você precisa combinar duas listas, use **`with_nested`**.

#### **Exemplo: Criar Combinações de Usuários e Grupos**

```sh
- name: Criar combinações de usuários e grupos
  hosts: all
  tasks:
    - name: Associar usuários a grupos
      debug:
        msg: "Usuário {{ item.0 }} no grupo {{ item.1 }}"
      with_nested:
        - [usuario1, usuario2]
        - [grupo1, grupo2]
```

**O que acontece?**

1. O loop cria todas as combinações possíveis:
    
    - `usuario1` no `grupo1`
        
    - `usuario1` no `grupo2`
        
    - `usuario2` no `grupo1`
        
    - `usuario2` no `grupo2`

### **Resumo**

- **`loop`**: Forma moderna e recomendada para loops.
    
- **`with_items`**: Forma antiga, mas ainda funcional.
    
- **`with_dict`**: Para iterar sobre dicionários.
    
- **`with_sequence`**: Para iterar sobre números.
    
- **`with_nested`**: Para combinar duas listas.
    
- **`until`**: Para repetir uma tarefa até que uma condição seja atendida.

