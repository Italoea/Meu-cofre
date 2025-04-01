


### ***Executar um Comando Simples
Digite um comando e pressione **Enter** para executá-lo:

- Exemplo:
	`ls`

Esse comando lista os arquivos no diretório atual.


### **Usar Comandos com Opções e Argumentos**

Muitos comandos aceitam **opções** (que alteram o comportamento do comando) e **argumentos** (dados que o comando processa):

Exemplo:
	``ls -l /home

- `ls`: Lista arquivos.
- `-l`: Mostra detalhes como permissões e tamanhos.
- `/home`: Especifica o diretório a ser listado.


### **Criar e Navegar Entre Diretórios**

Comandos básicos para gerenciar pastas e arquivos:

**Criar um diretório:**
	`mkdir nome_da_pasta`

**Entrar em um diretório:**
	`cd nome_da_pasta

**Voltar ao diretório anterior:**
		`cd ..`

### **Redirecionar Saída e Usar Pipes**

Você pode redirecionar a saída de um comando para arquivos ou outro comando:

**Salvar saída em um arquivo:**

	ls > lista_de_arquivos.txt


**Encadear comandos com pipes (`|`):**

	ls | grep .txt

Aqui, a saída de `ls` é filtrada pelo comando `grep` para mostrar apenas arquivos `.txt`.

### **Executar Scripts Bash**

Para rodar um arquivo de script no Bash:

Crie um arquivo, por exemplo, `script.sh`:

	echo "echo 'Olá, Mundo!'" > script.sh

Torne-o executável:
	chmod +x script.sh

Execute-o:
	./script.sh


### ***Usar Variáveis e Alias

**Definir e usar uma variável:**

	nome="Mundo"
	echo "Olá, $nome!"


**Criar um alias para comandos frequentes:**

	alias ll="ls -la"
