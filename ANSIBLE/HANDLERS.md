### **1. O que são Handlers?**

- **Handlers** são como tarefas normais, mas com uma diferença importante: eles só são executados quando são **notificados**.
    
- Eles são definidos em um bloco separado chamado `handlers`.
    
- São úteis para evitar ações desnecessárias. Por exemplo, você não quer reiniciar um serviço se nada mudou.
    

---

### **2. Como Funcionam os Handlers?**

1. **Definição do Handler**: Você define o handler no bloco `handlers` do playbook.
    
2. **Notificação**: Em uma tarefa normal, você usa a diretiva `notify` para acionar o handler.
    
3. **Execução**: O handler só é executado no **final do playbook**, e apenas se for notificado.
    

---

### **3. Exemplo Prático**

Vamos criar um exemplo simples: configurar um serviço e reiniciá-lo apenas se a configuração for alterada.

#### **Playbook Completo**

```sh
- name: Configurar e reiniciar serviço
  hosts: all
  tasks:
    - name: Copiar arquivo de configuração
      template:
        src: /caminho/para/template.conf.j2
        dest: /etc/meu_servico.conf
      notify: Reiniciar serviço  # Notifica o handler

  handlers:
    - name: Reiniciar serviço
      service:
        name: meu_servico
        state: restarted
```


### **4. Passo a Passo**

#### **Passo 1: Definindo o Handler**

No bloco `handlers`, você define o que o handler deve fazer. No nosso exemplo, o handler reinicia o serviço `meu_servico`:

```sh
handlers:
  - name: Reiniciar serviço
    service:
      name: meu_servico
      state: restarted
```

#### **Passo 2: Notificando o Handler**

Na tarefa que pode causar uma mudança (como copiar um arquivo de configuração), você usa a diretiva `notify` para acionar o handler:

```sh
tasks:
  - name: Copiar arquivo de configuração
    template:
      src: /caminho/para/template.conf.j2
      dest: /etc/meu_servico.conf
    notify: Reiniciar serviço  # Notifica o handler
```

#### **Passo 3: Execução do Handler**

- O handler **não é executado imediatamente** quando é notificado.
    
- Ele é agendado para ser executado no **final do playbook**.
    
- Se o handler for notificado várias vezes, ele só será executado **uma vez**.
    

---

### **5. Quando Usar Handlers?**

Handlers são ideais para:

- Reiniciar serviços após mudanças de configuração.
    
- Recarregar configurações (por exemplo, `nginx -s reload`).
    
- Qualquer ação que só deve ser executada se algo mudar.
    

---

### **6. Exemplo Completo com Múltiplos Handlers**

Aqui está um exemplo com dois handlers: um para reiniciar um serviço e outro para recarregar outro serviço.

```sh 
- name: Configurar serviços
  hosts: all
  tasks:
    - name: Copiar configuração do serviço A
      template:
        src: /caminho/para/servico_a.conf.j2
        dest: /etc/servico_a.conf
      notify: Reiniciar serviço A

    - name: Copiar configuração do serviço B
      template:
        src: /caminho/para/servico_b.conf.j2
        dest: /etc/servico_b.conf
      notify: Recarregar serviço B

  handlers:
    - name: Reiniciar serviço A
      service:
        name: servico_a
        state: restarted

    - name: Recarregar serviço B
      service:
        name: servico_b
        state: reloaded
```

### **7. Dicas Importantes**

1. **Nomes Únicos**: Certifique-se de que os nomes dos handlers são únicos e consistentes.
    
2. **Ordem de Execução**: Handlers são executados na ordem em que são notificados, mas apenas uma vez.
    
3. **Escopo**: Handlers são globais para o playbook. Se você notificar um handler em uma tarefa, ele será executado no final do playbook, mesmo que a notificação venha de uma tarefa em um bloco diferente.
    

---

### **8. Erros Comuns**

4. **Handler Não Encontrado**: O erro que você mencionou (`The requested handler was not found`) ocorre quando o handler não está definido ou o nome está incorreto.
    
    - Solução: Verifique se o nome no `notify` está exatamente igual ao nome do handler.
        
5. **Handler Não Executado**: Se o handler não for executado, pode ser porque a tarefa que o notifica não foi executada ou não causou mudanças.
    
    - Solução: Use a opção `--force-handlers` para forçar a execução dos handlers, mesmo que uma tarefa falhe.