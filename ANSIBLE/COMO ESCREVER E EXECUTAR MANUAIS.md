
### Passo 1: **Estrutura Básica de um Playbook**

Um playbook do Ansible é um arquivo YAML que descreve as tarefas a serem executadas em seus hosts. Aqui está um exemplo básico:

```sh
---
- name: Exemplo de Playbook
  hosts: all  # Executa em todos os hosts do inventário
  become: yes  # Executa tarefas com privilégios elevados (sudo)
  tasks:
    - name: Instalar o Apache
      apt:
        name: apache2
        state: present
        update_cache: yes

    - name: Garantir que o Apache está em execução
      service:
        name: apache2
        state: started
        enabled: yes
```

#### Explicação:

- **`name`**: Descrição do playbook ou tarefa.
    
- **`hosts`**: Define em quais hosts o playbook será executado (por exemplo, `all`, `web`, `db`).
    
- **`become`**: Executa as tarefas com privilégios elevados (usando `sudo`).
    
- **`tasks`**: Lista de tarefas a serem executadas.
    
- **Módulos**: `apt` (para instalar pacotes no Debian/Ubuntu) e `service` (para gerenciar serviços).

### Passo 2: **Criar o Arquivo do Playbook**

1. Crie um arquivo YAML, por exemplo, `meu_playbook.yml`.
    
2. Cole o conteúdo do playbook no arquivo.
    
3. Salve o arquivo.


### Passo 3: **Criar um Inventário**

O inventário é um arquivo que lista os hosts onde o playbook será executado. Crie um arquivo chamado `inventario.ini`:

```sh
[web]
192.168.1.10
192.168.1.11

[db]
192.168.1.20
```
#### Explicação

- **`[web]` e `[db]`**: Grupos de hosts.
    
- **IPs ou nomes de hosts**: Lista de hosts em cada grupo.


### Passo 4: **Executar o Playbook**

Use o comando `ansible-playbook` para executar o playbook. Aqui está o comando básico:

```sh
ansible-playbook -i inventario.ini meu_playbook.yml
```

#### Opções Adicionais:

- **`-i inventario.ini`**: Especifica o arquivo de inventário.
    
- **`-l web`**: Executa apenas nos hosts do grupo `web`.
    
- **`--ask-become-pass`**: Solicita a senha do `sudo`.

### Passo 5: **Verificar a Execução**

Durante a execução, o Ansible exibe o progresso e o resultado de cada tarefa. Se tudo correr bem, você verá uma mensagem como:

```sh
PLAY RECAP **********************************************
192.168.1.10              : ok=3    changed=2    unreachable=0    failed=0
192.168.1.11              : ok=3    changed=2    unreachable=0    failed=0
```
#### Explicação:

- **`ok`**: Tarefas concluídas com sucesso.
    
- **`changed`**: Tarefas que alteraram o estado do sistema.
    
- **`failed`**: Tarefas que falharam (precisa ser corrigido).


### Passo 6: **Depuração e Testes**

1. **Verificar Sintaxe**:  
    Use o comando `--syntax-check` para validar a sintaxe do playbook:

```sh
ansible-playbook --syntax-check meu_playbook.yml
```

**Modo de Simulação (Dry Run)**:  
	Use o comando `--check` para simular a execução sem fazer alterações:

```sh
ansible-playbook -i inventario.ini meu_playbook.yml --check
```

**Verbose Mode**:  
Use a opção `-v` (ou `-vv`, `-vvv`, `-vvvv`) para obter mais detalhes durante a execução:

```sh
ansible-playbook -i inventario.ini meu_playbook.yml -v
```

| Opção   | Descrição                                                                                                                                                                |
| :------ | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-v`    | Exibe os resultados da tarefa.                                                                                                                                           |
| `-vv`   | Exibe os resultados e a configuração das tarefas.                                                                                                                        |
| `-vvv`  | Exibe informações extras sobre conexões com hosts gerenciados.                                                                                                           |
| `-vvvv` | Adiciona opções extras de verbosidade aos plug-ins de conexão, incluindo usuários usados ​​nos hosts gerenciados para executar scripts e quais scripts foram executados. |
