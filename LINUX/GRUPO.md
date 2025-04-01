### **Conceito de Grupo no Linux**

Um **grupo** no Linux é uma coleção de usuários que compartilham permissões para acessar arquivos e recursos específicos no sistema. Grupos permitem que você administre permissões de forma mais eficiente, em vez de definir permissões para cada usuário individualmente.

#### **Identificação de um Grupo**

Cada grupo tem um nome e um **ID único de grupo** (GID). O GID é registrado no arquivo `/etc/group`. O grupo principal de um usuário é o grupo listado no campo GID de sua entrada no arquivo `/etc/passwd`.

#### **Exemplo - Criação de um Grupo**

Você pode criar um grupo usando o comando `groupadd`:
	`sudo groupadd nome_do_grupo`

- Isso cria um novo grupo chamado `nome_do_grupo`.

#### **Adicionar Usuários a um Grupo**

Usuários podem ser adicionados a grupos usando o comando `usermod`:
	`sudo usermod -aG nome_do_grupo nome_do_usuario`

- Aqui, `-aG` adiciona o usuário ao grupo sem removê-lo de outros grupos aos quais ele já pertence.

#### **Grupos Primários e Secundários**

- **Grupo primário**: Cada usuário tem um grupo primário, que é o grupo associado ao UID do usuário.
- **Grupos secundários**: Um usuário pode pertencer a vários grupos, além do seu grupo primário. Esses são os grupos secundários.



### **Arquivos de Configuração de Usuário e Grupo**


#### **/etc/passwd**

O arquivo `/etc/passwd` contém informações sobre os usuários do sistema. Cada linha deste arquivo representa um usuário e contém os seguintes campos:
	`nome_de_usuario:x:UID:GID:informacoes_de_usuario:/diretorio/home:/shell`


- **nome_de_usuario**: Nome do usuário.
- **x**: Indicador de senha (geralmente criptografada, mas a senha real fica no `/etc/shadow`).
- **UID**: ID do usuário.
- **GID**: ID do grupo primário do usuário.
- **informacoes_de_usuario**: Informações extras, como o nome completo.
- **/diretorio/home**: Caminho para o diretório home do usuário.
- **/shell**: Shell padrão do usuário.



#### **/etc/group**
O arquivo `/etc/group` contém informações sobre os grupos do sistema. Cada linha representa um grupo e tem o seguinte formato:
	`nome_do_grupo:x:GID:usuarios_do_grupo`

- **nome_do_grupo**: Nome do grupo.
- **x**: Indicador de senha (grupos podem ter senhas, mas normalmente não é usado).
- **GID**: ID do grupo.
- **usuarios_do_grupo**: Lista de usuários pertencentes a esse grupo.