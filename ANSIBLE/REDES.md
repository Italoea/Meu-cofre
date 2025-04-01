
### **1. Introdução ao Ansible e Rede**

O Ansible é uma ferramenta de automação que permite gerenciar configurações, implantar software e automatizar tarefas em vários hosts. Para gerenciar configurações de rede, o Ansible usa módulos específicos, como `nmcli` (para gerenciar NetworkManager) ou edição direta de arquivos de configuração, como `/etc/network/interfaces` ou `/etc/sysconfig/network-scripts/`.

---

### **2. Definindo Configurações de Rede**

Para configurar a rede em hosts gerenciados, você pode usar módulos do Ansible, como `nmcli` ou `lineinfile` para editar arquivos de configuração manualmente.

#### Exemplo: Configurando um IP estático usando o módulo `nmcli`

```sh
- name: Configurar IP estático no host gerenciado
  hosts: all
  become: yes
  tasks:
    - name: Definir IP estático
      nmcli:
        type: ethernet
        conn_name: eth0
        ip4: 192.168.1.100/24
        gw4: 192.168.1.1
        dns4:
          - 8.8.8.8
          - 8.8.4.4
        state: present
```

#### Explicação:

- **`nmcli`**: Módulo para gerenciar conexões de rede via NetworkManager.
    
- **`conn_name`**: Nome da conexão de rede (ex: `eth0`).
    
- **`ip4`**: Endereço IP e máscara de rede.
    
- **`gw4`**: Gateway padrão.
    
- **`dns4`**: Servidores DNS.

---
### **3. Configurando Resolução de Nomes (DNS)**

Para configurar a resolução de nomes, você pode editar o arquivo `/etc/resolv.conf` ou usar o módulo `nmcli` para definir servidores DNS.

#### Exemplo: Configurando DNS usando `lineinfile`

```sh
- name: Configurar servidores DNS
  hosts: all
  become: yes
  tasks:
    - name: Adicionar servidores DNS ao /etc/resolv.conf
      lineinfile:
        path: /etc/resolv.conf
        line: "nameserver {{ item }}"
        create: yes
      loop:
        - 8.8.8.8
        - 8.8.4.4
```

#### Explicação:

- **`lineinfile`**: Módulo para editar linhas específicas em um arquivo.
    
- **`loop`**: Adiciona múltiplos servidores DNS.

---
### **4. Coletando Fatos Relacionados à Rede**

O Ansible coleta automaticamente fatos sobre os hosts gerenciados, incluindo informações de rede. Você pode acessar esses fatos usando a variável `ansible_facts`.

#### Exemplo: Coletando e exibindo fatos de rede

```sh
- name: Coletar e exibir fatos de rede
  hosts: all
  tasks:
    - name: Exibir informações de rede
      debug:
        msg: >
          Endereço IP: {{ ansible_default_ipv4.address }},
          Gateway: {{ ansible_default_ipv4.gateway }},
          DNS: {{ ansible_dns.nameservers }}
```

#### Explicação:

- **`ansible_default_ipv4`**: Contém informações sobre o IPv4 padrão.
    
- **`ansible_dns`**: Contém informações sobre servidores DNS.

----
### **5. Prática: Playbook Completo**

Aqui está um exemplo de playbook que configura a rede e coleta fatos:

```sh
- name: Configurar rede e coletar fatos
  hosts: all
  become: yes
  tasks:
    - name: Definir IP estático
      nmcli:
        type: ethernet
        conn_name: eth0
        ip4: 192.168.1.100/24
        gw4: 192.168.1.1
        dns4:
          - 8.8.8.8
          - 8.8.4.4
        state: present

    - name: Exibir informações de rede
      debug:
        msg: >
          Endereço IP: {{ ansible_default_ipv4.address }},
          Gateway: {{ ansible_default_ipv4.gateway }},
          DNS: {{ ansible_dns.nameservers }}
```

---
### **6. Executando o Playbook**

Salve o playbook em um arquivo YAML (ex: `rede.yml`) e execute-o com o comando:

```sh
ansible-playbook -i inventario.ini rede.yml
```
- **`inventario.ini`**: Arquivo de inventário com os hosts gerenciados.
---
### **7. Dicas e Boas Práticas**

1. **Teste em um ambiente de desenvolvimento antes de aplicar em produção.**
    
2. Use o módulo `check_mode` para simular alterações sem aplicá-las:

```sh
ansible-playbook -i inventario.ini rede.yml --check
```

1. Documente suas playbooks para facilitar a manutenção.

---

