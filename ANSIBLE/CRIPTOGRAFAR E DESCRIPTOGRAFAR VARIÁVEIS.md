### 1. Criptografando uma Variável com Ansible Vault

Para criptografar uma variável, você pode criar ou editar um arquivo YAML e criptografá-lo com o Ansible Vault.

#### Criar um arquivo criptografado:

```sh
ansible-vault create arquivo_secreto.yml
```


Isso abrirá um editor de texto onde você pode adicionar suas variáveis sensíveis. Por exemplo:

```sh
senha_banco: senha_segura123
api_key: chave_api_secreta
```
Salve e feche o editor. O arquivo será criptografado automaticamente.

#### Criptografar um arquivo existente:

Se você já tem um arquivo YAML com variáveis e deseja criptografá-lo:

``` sh
ansible-vault encrypt arquivo_existente.yml
```

### 2. Descriptografando uma Variável com Ansible Vault

Para editar ou visualizar um arquivo criptografado, você pode descriptografá-lo temporariamente:

#### Editar um arquivo criptografado:

``` sh
ansible-vault edit arquivo_secreto.yml
```
Isso abrirá o arquivo criptografado em um editor de texto, permitindo que você faça alterações.

#### Visualizar um arquivo criptografado:

```sh
ansible-vault view arquivo_secreto.yml
```
Isso exibirá o conteúdo descriptografado sem permitir edições.

#### Descriptografar permanentemente um arquivo:

Se você deseja remover a criptografia de um arquivo permanentemente:

```sh
ansible-vault decrypt arquivo_secreto.yml
```

### 3. Usando Arquivos Criptografados em Playbooks

Para usar variáveis criptografadas em seus playbooks, você pode incluir o arquivo criptografado como um `vars_file`:

```sh
- hosts: all
  vars_files:
    - arquivo_secreto.yml
  tasks:
    - name: Exibir senha do banco
      debug:
        msg: "A senha do banco é {{ senha_banco }}"
```

### 4. Executando Playbooks com Arquivos Criptografados

Ao executar um playbook que usa arquivos criptografados, você precisará fornecer a senha do Vault. Você pode fazer isso de várias maneiras:

#### Fornecer a senha interativamente:

```sh
ansible-playbook playbook.yml --ask-vault-pass
```

#### Usar um arquivo de senha:

Crie um arquivo de texto com a senha do Vault e use o seguinte comando:

```sh
ansible-playbook playbook.yml --vault-password-file caminho/para/senha.txt
```

#### Usar variáveis de ambiente:

Você pode armazenar a senha em uma variável de ambiente e usar:

```sh
ANSIBLE_VAULT_PASSWORD_FILE=caminho/para/senha.txt ansible-playbook playbook.yml
```

### 5. Gerenciando Senhas do Vault

Se você precisar alterar a senha de um arquivo criptografado:

```sh
ansible-vault rekey arquivo_secreto.yml
```
