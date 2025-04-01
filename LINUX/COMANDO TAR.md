| **Comando**                               | **Função**                          | **Descrição**                                                        |
| ----------------------------------------- | ----------------------------------- | -------------------------------------------------------------------- |
| `tar -cf arquivo.tar pasta/`              | Criar um arquivo TAR                | Empacota o conteúdo de `pasta/` no arquivo `arquivo.tar`.            |
| `tar -xf arquivo.tar`                     | Extrair arquivo TAR                 | Extrai o conteúdo de `arquivo.tar` no diretório atual.               |
| `tar -czf arquivo.tar.gz pasta/`          | Criar e comprimir (gzip)            | Empacota e comprime `pasta/` no arquivo `arquivo.tar.gz`.            |
| `tar -xzf arquivo.tar.gz`                 | Extrair arquivo compactado          | Extrai o conteúdo de um arquivo TAR compactado com gzip (`.tar.gz`). |
| `tar -tvf arquivo.tar`                    | Listar conteúdo do arquivo TAR      | Mostra os arquivos e diretórios contidos em `arquivo.tar`.           |
| `tar -rvf arquivo.tar novo_arquivo`       | Adicionar arquivos ao TAR existente | Adiciona `novo_arquivo` ao arquivo `arquivo.tar` sem reempacotar.    |
| `tar -cf - pasta/`                        | gzip > arquivo.tar.gz`              | Empacotar e comprimir com redirecionamento                           |
| `tar -xvf arquivo.tar --directory pasta/` | Extrair para um local específico    | Extrai o conteúdo de `arquivo.tar` diretamente na pasta `pasta/`.    |

### **Opções Comuns**

- `-c`: Criar um arquivo.
- `-x`: Extrair um arquivo.
- `-z`: Comprimir ou descomprimir com **gzip**.
- `-j`: Comprimir ou descomprimir com **bzip2**.
- `-f`: Especifica o nome do arquivo TAR.
- `-v`: Modo verbose, mostra os arquivos sendo processados.
- `-t`: Lista o conteúdo do arquivo TAR.

### **Exemplos Práticos**

- Criar um backup de diretórios:
	`tar -czvf backup.tar.gz /home/usuario/`

	- Isso cria um arquivo compactado com o conteúdo do diretório `/home/usuario/`.

- Extrair um backup:
`tar -xzvf backup.tar.gz -C /restaurar/`

- Extrai o conteúdo em `/restaurar/`.