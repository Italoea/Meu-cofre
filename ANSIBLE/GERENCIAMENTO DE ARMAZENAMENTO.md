
### 1. Introdução

O gerenciamento de armazenamento é uma tarefa crítica na administração de sistemas Linux. Isso inclui:

- Particionamento de discos.
    
- Configuração de LVM para gerenciamento flexível de volumes.
    
- Formatação de partições ou volumes lógicos.
    
- Montagem de sistemas de arquivos.
    
- Adição de espaços de troca (swap).
    

O Ansible oferece módulos para automatizar essas tarefas, garantindo consistência e eficiência em todos os hosts gerenciados.

---

### 2. Particionamento de Discos

O Ansible pode ser usado para criar partições em discos utilizando o módulo `parted`.

#### Tarefa 1: Criar uma Partição

Vamos criar uma partição de 10 GB no dispositivo `/dev/sdb`.

**playbook_create_partition.yml:**

```sh
- hosts: all
  become: yes  # Executar como superusuário
  tasks:
    - name: Criar partição de 10 GB no /dev/sdb
      parted:
        device: /dev/sdb
        number: 1
        state: present
        part_start: 1MiB
        part_end: 10GiB
```

**Executar o playbook:**

```sh
ansible-playbook -i inventory playbook_create_partition.yml
```

**Explicação:**

- `device`: Dispositivo onde a partição será criada.
    
- `number`: Número da partição.
    
- `state: present`: Garante que a partição exista.
    
- `part_start` e `part_end`: Define o tamanho da partição.

---

### 3. Configuração de LVM (Logical Volume Manager)

O LVM permite gerenciar volumes lógicos de forma flexível. Vamos aprender a configurar LVM com o Ansible.

#### Tarefa 2: Criar um Volume Físico (PV)

Vamos criar um volume físico no dispositivo `/dev/sdb1`.

**playbook_create_pv.yml:**

```sh
- hosts: all
  become: yes
  tasks:
    - name: Criar volume físico no /dev/sdb1
      lvol:
        vg: vg_data
        pv: /dev/sdb1
        state: present
```

**Executar o playbook:**

```sh
ansible-playbook -i inventory playbook_create_pv.yml
```

**Explicação:**

- `pv`: Dispositivo que será usado como volume físico.
    
- `vg`: Nome do grupo de volumes.
    
- `state: present`: Garante que o volume físico exista.
---

#### Tarefa 3: Criar um Grupo de Volumes (VG)

Vamos criar um grupo de volumes chamado `vg_data`.

**playbook_create_vg.yml:**

```sh
- hosts: all
  become: yes
  tasks:
    - name: Criar grupo de volumes vg_data
      lvg:
        vg: vg_data
        pvs: /dev/sdb1
        state: present
```

**Executar o playbook:**

```sh
ansible-playbook -i inventory playbook_create_vg.yml
```

**Explicação:**

- `vg`: Nome do grupo de volumes.
    
- `pvs`: Lista de volumes físicos que compõem o grupo.
    
- `state: present`: Garante que o grupo de volumes exista.

---

#### Tarefa 4: Criar um Volume Lógico (LV)

Vamos criar um volume lógico de 5 GB no grupo de volumes `vg_data`.

**playbook_create_lv.yml:**

```sh
- hosts: all
  become: yes
  tasks:
    - name: Criar volume lógico lv_data de 5 GB
      lvol:
        vg: vg_data
        lv: lv_data
        size: 5G
        state: present
```

**Executar o playbook:**

```sh
ansible-playbook -i inventory playbook_create_lv.yml
```

**Explicação:**

- `vg`: Nome do grupo de volumes.
    
- `lv`: Nome do volume lógico.
    
- `size`: Tamanho do volume lógico.
    
- `state: present`: Garante que o volume lógico exista.

---

### 4. Formatação de Partições ou Volumes Lógicos

Após criar partições ou volumes lógicos, é necessário formatá-los com um sistema de arquivos.

#### Tarefa 5: Formatar um Volume Lógico com ext4

Vamos formatar o volume lógico `lv_data` com o sistema de arquivos `ext4`.

**playbook_format_lv.yml:**

```sh
- hosts: all
  become: yes
  tasks:
    - name: Formatar lv_data com ext4
      filesystem:
        fstype: ext4
        dev: /dev/vg_data/lv_data
```

**Executar o playbook:**

```sh
ansible-playbook -i inventory playbook_format_lv.yml
```

**Explicação:**

- `fstype`: Tipo de sistema de arquivos.
    
- `dev`: Dispositivo ou volume lógico a ser formatado.

---

### 5. Montagem de Sistemas de Arquivos

Após formatar, é necessário montar o sistema de arquivos em um diretório.

#### Tarefa 6: Montar um Volume Lógico

Vamos montar o volume lógico `lv_data` no diretório `/mnt/data`.

**playbook_mount_lv.yml:**

```sh
- hosts: all
  become: yes
  tasks:
    - name: Montar lv_data em /mnt/data
      mount:
        path: /mnt/data
        src: /dev/vg_data/lv_data
        fstype: ext4
        state: mounted
```

**Executar o playbook:**

```sh
ansible-playbook -i inventory playbook_mount_lv.yml
```
**Explicação:**

- `path`: Diretório de montagem.
    
- `src`: Dispositivo ou volume lógico a ser montado.
    
- `fstype`: Tipo de sistema de arquivos.
    
- `state: mounted`: Garante que o sistema de arquivos esteja montado.

---

### 6. Adição de Espaço de Troca (Swap)

O espaço de troca (swap) é usado para aumentar a memória virtual do sistema. Vamos aprender a adicionar swap.

#### Tarefa 7: Adicionar um Arquivo de Swap

Vamos criar um arquivo de swap de 1 GB.

**playbook_add_swap.yml:**

```sh
- hosts: all
  become: yes
  tasks:
    - name: Criar arquivo de swap de 1 GB
      command: dd if=/dev/zero of=/swapfile bs=1M count=1024
      args:
        creates: /swapfile  # Executa apenas se o arquivo não existir

    - name: Configurar permissões do arquivo de swap
      file:
        path: /swapfile
        mode: '0600'

    - name: Ativar o arquivo de swap
      command: mkswap /swapfile
      args:
        creates: /swapfile  # Executa apenas se o arquivo não estiver ativado

    - name: Adicionar o arquivo de swap ao fstab
      mount:
        path: none
        src: /swapfile
        fstype: swap
        opts: defaults
        state: present

    - name: Ativar o swap
      command: swapon -a
```

**Executar o playbook:**

```sh
ansible-playbook -i inventory playbook_add_swap.yml
```

**Explicação:**

- `dd`: Cria um arquivo de 1 GB.
    
- `mkswap`: Configura o arquivo como swap.
    
- `swapon -a`: Ativa o swap.

---

### 7. Documentação das Tarefas

Documentar as tarefas automatizadas é essencial para a manutenção e o entendimento do sistema.

**Exemplo de Documentação:**

**Manual de Gerenciamento de Armazenamento**

1. **Particionamento de Discos**
    
    - Playbook: `playbook_create_partition.yml`
        
    - Tarefas:
        
        - Criar partição de 10 GB no `/dev/sdb`.
            
2. **Configuração de LVM**
    
    - Playbook: `playbook_create_lv.yml`
        
    - Tarefas:
        
        - Criar volume lógico `lv_data` de 5 GB.
            
3. **Formatação e Montagem**
    
    - Playbook: `playbook_mount_lv.yml`
        
    - Tarefas:
        
        - Montar `lv_data` em `/mnt/data`.
            
4. **Adição de Swap**
    
    - Playbook: `playbook_add_swap.yml`
        
    - Tarefas:
        
        - Criar e ativar um arquivo de swap de 1 GB.
            

---

### 8. Boas Práticas

- **Testes**: Sempre teste os playbooks em um ambiente de desenvolvimento antes de aplicá-los em produção.
    
- **Backup**: Faça backup dos dados antes de manipular partições ou volumes.
    
- **Documentação**: Documente todas as tarefas e configurações.
    

---

### 9. Conclusão

Nesta aula, aprendemos a:

- Particionar discos.
    
- Configurar LVM (volumes físicos, grupos de volumes e volumes lógicos).
    
- Formatar e montar sistemas de arquivos.
    
- Adicionar espaço de troca (swap).
    

Com essas técnicas, você pode automatizar o gerenciamento de armazenamento com o Ansible, garantindo consistência e eficiência.