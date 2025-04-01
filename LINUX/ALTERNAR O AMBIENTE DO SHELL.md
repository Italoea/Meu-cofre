### **Variáveis de Ambiente**

As variáveis de ambiente são usadas para configurar aspectos do shell e de programas que você executa. Elas podem ser definidas e alteradas tanto temporariamente quanto permanentemente.

#### **Ver as Variáveis de Ambiente Atuais**

- Você pode ver todas as variáveis de ambiente definidas com o comando:
	`printenv`

- Ou apenas uma variável específica:
	`echo $NOME_VARIAVEL`

- Exemplo:
- `echo $HOME`


#### **Definir ou Alterar Variáveis de Ambiente Temporárias**

- Para definir uma variável de ambiente temporariamente (válida apenas para a sessão atual):
	`export NOME_VARIAVEL=valor`

- Exemplo:
	`export PATH=$PATH:/novo/caminho`
- Aqui, estamos adicionando `/novo/caminho` ao `PATH`, que é a variável que define os diretórios onde o sistema procura por executáveis.


#### **Definir ou Alterar Variáveis de Ambiente Permanentemente**

- Para definir variáveis permanentemente, você deve adicionar o comando `export` ao seu arquivo de inicialização de shell, como `~/.bashrc` (para o Bash) ou `~/.zshrc` (para o Zsh).

- Edite o arquivo:
	`nano ~/.bashrc`

- Adicione a linha:
	`export NOME_VARIAVEL=valor`

- Depois, recarregue o arquivo para que as alterações tenham efeito:
	`source ~/.bashrc`


### **Arquivos de Inicialização do Shell**

Os arquivos de inicialização são scripts que o shell executa automaticamente quando você abre um terminal. Eles definem o comportamento do ambiente do shell.

#### **Arquivos Comuns de Inicialização do Shell (Bash)**

- **`~/.bash_profile`** ou **`~/.profile`**: Executado no login interativo, quando você entra no sistema.
- **`~/.bashrc`**: Executado em cada novo terminal interativo não-login (como uma nova aba ou janela no terminal).
- **`/etc/profile`**: Configurações globais para todos os usuários, executado no login.
- **`/etc/bash.bashrc`**: Arquivo de configuração global para Bash (geralmente em sistemas baseados em Debian).


#### **Exemplo - Personalizar o Prompt (PS1)**

O prompt do shell é configurado pela variável de ambiente `PS1`. Você pode personalizá-lo para exibir informações úteis, como o diretório atual, o nome de usuário, o host, etc.

Adicione a linha seguinte no seu `~/.bashrc`:
	`export PS1="\u@\h:\w\$ "`

Aqui está o que os elementos do `PS1` significam:
- **`\u`**: Nome do usuário.
- **`\h`**: Nome do host.
- **`\w`**: Diretório de trabalho atual.
- **`\$`**: Exibe `#` para root e `$` para usuários comuns.


### **Configuração do PATH**
O `PATH` é uma variável de ambiente importante que define onde o sistema procura por programas executáveis. Para adicionar novos diretórios ao `PATH`:

-  **Adicionar um diretório ao `PATH`:**
    `export PATH=$PATH:/novo/diretorio`
- Isso adiciona `/novo/diretorio` ao final do `PATH`.


- **Adicionar permanentemente ao `PATH`:** Adicione a linha `export PATH=$PATH:/novo/diretorio` ao seu arquivo `~/.bashrc` ou `~/.profile` e, em seguida, recarregue o arquivo:

    `source ~/.bashrc`



### **Modificar o Ambiente para Scripts**

Quando você executa scripts, pode ser necessário alterar o ambiente de maneira específica para aquele script. Você pode definir variáveis dentro do próprio script ou alterá-las antes de executá-lo.

#### **Exemplo de script que altera o ambiente:**
	`#!/bin/bash export 
	VARIAVEL="novo_valor" echo "Valor de VARIAVEL: $VARIAVEL"`

- Aqui, a variável `VARIAVEL` é definida dentro do script e usada durante sua execução.


### **Alterar o Shell Padrão**

Você pode alterar o shell que está sendo usado pelo usuário, como de `bash` para `zsh`, `fish`, entre outros.

#### **Alterar o shell temporariamente (somente para a sessão atual):**
	`zsh`
- Isso iniciará uma nova instância do shell `zsh`.

#### **Alterar o shell de login padrão:**

Para alterar o shell de login padrão, use o comando `chsh` (change shell). Por exemplo, para mudar para o `zsh`:
	`chsh -s /bin/zsh`

- Depois de executar esse comando, você precisará sair e entrar novamente ou reiniciar a sessão para que a mudança tenha efeito.



### **Personalizar o Comportamento de Comandos e Aliases**

Você pode criar alias para comandos e até personalizar o comportamento de comandos no shell.

#### **Criar um alias para um comando:**
	`alias ll='ls -l'`

- Isso cria um atalho para o comando `ls -l`, fazendo com que `ll` seja um comando válido.

#### **Definir aliases permanentes:**

Adicione alias ao arquivo de configuração como `~/.bashrc` e depois execute:
	`source ~/.bashrc`


### **Alterar a Localização do Diretório de Trabalho Inicial**

Você pode definir o diretório em que o terminal deve começar cada vez que for aberto. Para isso, edite o arquivo de configuração, como `~/.bashrc`, e adicione:
	`cd /caminho/para/diretorio`

- Isso fará com que, ao abrir uma nova sessão, o terminal vá automaticamente para o diretório especificado.




### **Resumo: Como Alterar o Ambiente do Shell**

- **Variáveis de ambiente**: Defina e altere com `export`.
- **Arquivos de configuração**: Personalize o shell editando `~/.bashrc`, `~/.profile`, etc.
- **Personalização do `PATH`**: Adicione novos diretórios ao `PATH`.
- **Modificação do shell padrão**: Use `chsh` para mudar o shell.
- **Alias**: Crie atalhos para comandos comuns no shell.
- **Alteração do diretório de trabalho inicial**: Defina `cd` no arquivo de configuração.