### **Permissões de Arquivos e Grupos**

A combinação de **usuários** e **grupos** é usada para gerenciar permissões de acesso a arquivos e diretórios no Linux. As permissões são configuradas para o **dono do arquivo**, o **grupo do arquivo** e **outros**.

#### **Permissões de Arquivo**

As permissões são configuradas em três níveis:

- **Leitura (r)**: Permite ler o conteúdo do arquivo.
- **Gravação (w)**: Permite modificar o conteúdo do arquivo.
- **Execução (x)**: Permite executar o arquivo como um programa.

As permissões de arquivo podem ser visualizadas com o comando `ls -l`:
	`-rwxr-xr-x 1 usuario grupo  1024 Nov 27 12:00 arquivo.txt`

- O primeiro caractere indica o tipo de arquivo (`-` para arquivo regular, `d` para diretório).
- As três próximas colunas são as permissões do **dono**, **grupo** e **outros**, respectivamente.

#### **Alterar Permissões**

As permissões podem ser alteradas com o comando `chmod` (change mode). Exemplo:
	`chmod u+x arquivo.txt`
- Isso adiciona permissão de execução (`x`) para o **usuário** (`u`).

#### **Alterar Proprietário e Grupo**

O comando `chown` é usado para alterar o proprietário ou grupo de um arquivo:
	`chown usuario:grupo arquivo.txt`

### **Comandos Relacionados a Usuários e Grupos**

- **`useradd`**: Adiciona um novo usuário ao sistema.
- **`usermod`**: Modifica as configurações de um usuário existente.
- **`groupadd`**: Cria um novo grupo.
- **`groupdel`**: Remove um grupo.
- **`passwd`**: Altera a senha de um usuário.
- **`id`**: Exibe as informações do usuário (UID, GID, grupos).
- **`whoami`**: Exibe o nome do usuário atual.

### **Resumo:**

- **Usuários**: Representam indivíduos ou entidades que interagem com o sistema. Cada um tem um UID e permissões associadas.
- **Grupos**: Coleções de usuários que compartilham permissões. Um usuário pode pertencer a vários grupos.
- **Arquivos de configuração**: `/etc/passwd` (informações sobre usuários) e `/etc/group` (informações sobre grupos).
- **Permissões**: Definem quem pode ler, escrever ou executar arquivos, com base no usuário e no grupo.