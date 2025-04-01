

### **`nano` - Editor de Texto Simples**

O `nano` é um editor de texto fácil de usar e está disponível por padrão na maioria das distribuições Linux. Ele é ótimo para iniciantes.

- **Abrir um arquivo para edição:**
    `nano arquivo.txt`

- **Comandos úteis no `nano`:**
    
    - **Ctrl + O**: Salva o arquivo (você será solicitado a confirmar o nome do arquivo).
    - **Ctrl + X**: Sai do `nano` (se houver mudanças não salvas, ele perguntará se deseja salvar).
    - **Ctrl + K**: Corta uma linha.
    - **Ctrl + U**: Cola o conteúdo cortado.
    - **Ctrl + W**: Pesquisa no arquivo.

### **`vi` ou `vim` - Editores Avançados**

O `vi` (e sua versão melhorada, `vim`) é um editor de texto muito poderoso, mas pode ter uma curva de aprendizado maior. Ele é altamente configurável e disponível na maioria das distribuições Linux.

#### **Abrir o arquivo com `vi` ou `vim`:**
	`vi arquivo.txt`

#### **Modos do `vi`:**

1. **Modo de comando**: O `vi` inicia no modo de comando. No modo de comando, você pode mover o cursor, copiar, colar, apagar, etc.
2. **Modo de inserção**: Para editar o conteúdo do arquivo, você precisa entrar no modo de inserção.
    - Pressione `i` para entrar no modo de inserção e começar a digitar.
3. **Modo de comando novamente**: Para voltar ao modo de comando (e salvar ou sair), pressione `Esc`.

#### **Comandos úteis no `vi`/`vim`:**

- **i**: Modo de inserção (começa a digitar no arquivo).
- **Esc**: Volta para o modo de comando.
- **:w**: Salva o arquivo.
- **:w nome_arquivo**: Salva o arquivo com um nome diferente.
- **:q**: Sai do `vi`.
- **:q!**: Sai do `vi` sem salvar.
- **:wq** ou **ZZ**: Salva e sai.
- **/palavra**: Pesquisa por uma palavra no arquivo.
- **dd**: Exclui uma linha.
- **yy**: Copia uma linha.
- **p**: Cola a linha copiada.
- **u**: Desfaz a última alteração.




### **`sed` - Editor de Fluxo de Texto**

O `sed` é um editor de fluxo de texto que permite editar arquivos diretamente a partir do terminal usando comandos de substituição, inserção, exclusão, etc. É útil para edições em massa.

#### **Substituir texto em um arquivo com `sed`:**
	`sed -i 's/antigo/novo/g' arquivo.txt`

- **Explicação**:
    - `-i`: Modifica o arquivo diretamente (in-place).
    - `'s/antigo/novo/g'`: Substitui todas as ocorrências de "antigo" por "novo".
    - `g`: Substitui globalmente todas as ocorrências (não apenas a primeira).

#### **Exemplo - Deletar uma linha do arquivo:**
`sed -i '3d' arquivo.txt`

- **Explicação**: Remove a 3ª linha do arquivo.




### **`echo` - Adicionar Texto ao Final de um Arquivo**

Você pode usar o comando `echo` para adicionar texto ao final de um arquivo. Essa não é uma edição interativa, mas útil para pequenas alterações.

#### **Adicionar texto ao final de um arquivo:**

	`echo "Novo texto a ser adicionado" >> arquivo.txt`

#### **Adicionar várias linhas:**

	`echo -e "Primeira linha\nSegunda linha" >> arquivo.txt`

- O `-e` permite usar a sintaxe de escape, como `\n` para criar novas linhas.




### **`awk` - Processador de Texto e Edição**

O `awk` é uma ferramenta poderosa para processamento de texto e pode ser usada para editar arquivos, especialmente quando você precisa realizar transformações mais complexas.

#### **Exemplo - Substituir texto com `awk`:**
	`awk '{gsub(/antigo/, "novo"); print}' arquivo.txt > arquivo_modificado.txt`

- **Explicação**: O `awk` substitui todas as ocorrências de "antigo" por "novo" e escreve a saída em um novo arquivo.




### **`emacs` - Editor Completo**

O `emacs` é outro editor de texto poderoso, que possui uma interface mais robusta, oferecendo várias funcionalidades além da edição de texto.

- **Abrir um arquivo com o `emacs`:**
    `emacs arquivo.txt`

- **Comandos úteis no `emacs`:**
    
    - **Ctrl + x, Ctrl + s**: Salva o arquivo.
    - **Ctrl + x, Ctrl + c**: Sai do `emacs`.
    - **Ctrl + s**: Pesquisa no arquivo.
    - **Ctrl + k**: Apaga o texto da posição atual até o final da linha.
    - **Ctrl + y**: Cola o texto copiado.


### **Comparação entre os Editores:**

| Editor     | Facilidade de uso | Recursos | Para quem é indicado     |
| ---------- | ----------------- | -------- | ------------------------ |
| **nano**   | Fácil             | Básico   | Iniciantes               |
| **vi/vim** | Médio             | Avançado | Usuários experientes     |
| **emacs**  | Médio a Difícil   | Avançado | Usuários avançados       |
| **sed**    | Médio             | Avançado | Processamento em massa   |
| **awk**    | Médio             | Avançado | Transformações complexas |
