

### **Especificar um arquivo diretamente**

Basta mencionar o caminho do arquivo e o nome no comando:
	`cat arquivo.txt`

Isso exibe o conteúdo do arquivo chamado `arquivo.txt`.


### **Especificar usando caminhos**

- **Caminho Absoluto:** Começa na raiz (`/`), especificando todo o caminho até o arquivo.
	`cat /home/usuario/documentos/arquivo.txt`

- **Caminho Relativo:** Baseia-se no diretório atual.
	`cat documentos/arquivo.txt`

Use o comando `pwd` para verificar seu diretório atual.


### **Usar curingas (wildcards)**

Os curingas permitem selecionar vários arquivos de uma vez:

- **Asterisco (`*`):** Substitui zero ou mais caracteres.
    `ls *.txt`
 
Lista todos os arquivos com a extensão `.txt`.

   
- **Interrogação (`?`):** Substitui exatamente um caractere.
    `ls arquivo?.txt`

Lista arquivos como `arquivo1.txt`, `arquivo2.txt`, etc.


- **Colchetes (`[]`):** Especifica um conjunto de caracteres.
    `ls arquivo[1-3].txt`

Lista arquivos `arquivo1.txt`, `arquivo2.txt` e `arquivo3.txt`.


### **Usar caracteres de escape**

Se o nome do arquivo contiver espaços, caracteres especiais ou letras maiúsculas/minúsculas, você pode:

- Usar aspas simples ou duplas:
    `cat "arquivo com espaços.txt"`


- Usar uma barra invertida (`\`) antes de cada caractere especial:
    `cat arquivo\ com\ espaços.txt`


### **Ignorar diferenças de maiúsculas/minúsculas**

Por padrão, o Linux diferencia maiúsculas e minúsculas. Use `find` ou `ls` com a opção `-iname`:

`find . -iname "arquivo.txt"`

Isso encontrará arquivos chamados `arquivo.txt`, `ARQUIVO.txt`, etc.


### **Combinar com comandos como `find`**

Para localizar arquivos pelo nome em qualquer lugar do sistema:

- Procure em um diretório específico:
    `find /home/usuario -name "arquivo.txt"`
    

- Pesquise ignorando diferenças de maiúsculas/minúsculas:
    `find /home/usuario -iname "*.txt"`


### **Usar filtros com `grep`**

Para buscar arquivos específicos dentro de uma lista:
	`ls | grep "arquivo"`

Isso lista apenas arquivos que contêm "arquivo" no nome.


### **Manipular arquivos pelo nome**

Depois de especificar o arquivo, você pode usá-lo com outros comandos:

- Mover:
    `mv arquivo.txt nova_pasta/`


- Copiar:
    `cp arquivo.txt backup.txt`


- Excluir:
    `rm arquivo.txt`
