### **Conceito de Usuário no Linux**

No Linux, um **usuário** representa uma pessoa ou entidade que pode interagir com o sistema, executar processos, acessar arquivos e recursos, e configurar suas próprias preferências. Cada usuário tem um conjunto de permissões que determina o que ele pode ou não fazer.

#### **Identificação de um Usuário**

Cada usuário é identificado por um **nome de usuário** e possui um **ID único de usuário** (UID - User Identifier). Quando você cria um novo usuário, o sistema cria uma entrada no arquivo `/etc/passwd` que contém informações como o nome de usuário, UID, GID (ID do grupo primário), diretório home e o shell que o usuário usará.

- **UID**: Cada usuário possui um número de identificação único. O UID 0 é reservado para o **root** (superusuário).
- **GID**: O ID do grupo primário, que representa o grupo principal associado ao usuário.

#### **Exemplo - Criação de um Usuário**

Você pode criar um novo usuário usando o comando `useradd` ou `adduser` (dependendo da distribuição):
	`sudo useradd nome_do_usuario`

- Isso cria um novo usuário chamado `nome_do_usuario` no sistema.

#### **Informações sobre o Usuário**

Você pode obter informações sobre o usuário usando o comando `id`:
	`id nome_do_usuario`

- Isso exibe o UID, GID e os grupos aos quais o usuário pertence.

