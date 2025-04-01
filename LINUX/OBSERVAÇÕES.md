

#### Em muitas distribuições Linux, incluindo a usada em nossas máquinas virtuais, o comando ls usa cores para distinguir por tipo de arquivo. Por exemplo, diretórios podem ser exibidos em azul, arquivos executáveis ​​podem ser exibidos em verde e links simbólicos podem ser exibidos em ciano.

| **Tipo**                     | **Descrição**                                                       |
| ---------------------------- | ------------------------------------------------------------------- |
| **d - diretório**            | Um arquivo usado para armazenar outros arquivos.                    |
| **-**                        | Inclui arquivos legíveis, imagens, binários e arquivos compactados. |
| **l - link simbólico**       | Aponta para outro arquivo.                                          |
| **s - socket**               | Permite a comunicação entre processos.                              |
| **p - pipe**                 | Permite a comunicação entre processos.                              |
| **b - arquivo de bloco**     | Usado para se comunicar com hardware.                               |
| **c - arquivo de caractere** | Usado para se comunicar com hardware.                               |

**-rw-r--r-- 1 root root 15322 Dec 10 21:33 alternatives.log **

| **Parte**         | **Descrição**                          | **Exemplo**        |
| ----------------- | -------------------------------------- | ------------------ |
| Tipo e Permissões | Tipo (`-`) e permissões (`rw-r--r--`). | `-rw-r--r--`       |
| Links             | Quantidade de links físicos.           | `1`                |
| Proprietário      | Usuário que possui o arquivo.          | `root`             |
| Grupo             | Grupo proprietário do arquivo.         | `root`             |
| Tamanho           | Tamanho do arquivo em bytes.           | `15322`            |
| Data e Hora       | Última modificação do arquivo.         | `Dec 10 21:33`     |
| Nome do Arquivo   | Nome do arquivo listado.               | `alternatives.log` |
### 1. **`-rw-r--r--`** (Permissões)

- **`-`**: Indica o tipo de arquivo. Aqui, o `-` significa que é um **arquivo regular**.
    - Outros tipos possíveis incluem:
        - `d` para diretório.
        - `l` para link simbólico.
        - `b` para arquivo de bloco.
        - `c` para arquivo de caractere.
- **`rw-`**: Permissões para o **proprietário** (neste caso, o usuário `root`).
    - `r`: leitura (read).
    - `w`: escrita (write).
    - `-`: sem permissão de execução.
- **`r--`**: Permissões para o **grupo**.
    - `r`: apenas leitura.
    - `--`: sem permissão de escrita ou execução.
- **`r--`**: Permissões para **outros usuários** (não proprietários nem membros do grupo).
    - `r`: apenas leitura.

### 2. **`1`** (Número de links)

- Indica o número de **links físicos** apontando para este arquivo (normalmente 1 para arquivos regulares).

### 3. **`root`** (Proprietário)

- O nome do **usuário** que é o proprietário do arquivo. Aqui, o proprietário é `root`.

### 4. **`root`** (Grupo)

- O nome do **grupo** que tem permissões sobre o arquivo. Neste caso, o grupo também é `root`.

### 5. **`15322`** (Tamanho do arquivo)

- O tamanho do arquivo em **bytes**. Este arquivo tem 15.322 bytes.

### 6. **`Dec 10 21:33`** (Data e hora da última modificação)

- **`Dec`**: Mês da última modificação (dezembro).
- **`10`**: Dia da última modificação.
- **`21:33`**: Hora e minuto da última modificação.

### 7. **`alternatives.log`** (Nome do arquivo)

- O nome do arquivo listado. Neste caso, é `alternatives.log`.





| **Tecla/Opção**   | **Função**                                                                                                        |
| ----------------- | ----------------------------------------------------------------------------------------------------------------- |
| **`-t`**          | Classifica os arquivos com base no horário de modificação, listando os mais recentemente modificados primeiro.    |
| **`-l`**          | Exibe detalhes completos dos arquivos, como permissões, proprietário, grupo, tamanho, e data/hora de modificação. |
| **`-h`**          | Mostra tamanhos de arquivo em um formato legível por humanos (e.g., KB, MB, GB).                                  |
| **`--full-time`** | Exibe o registro completo de data e hora (incluindo horas, minutos e segundos).                                   |
| **`-r`**          | Realiza uma ordenação reversa (e.g., do maior para o menor ou do mais antigo para o mais recente).                |
| **`-S`**          | Ordena os arquivos pelo tamanho, do maior para                                                                    |
### Exemplos de uso:

1. **`ls -lt`**  
    Lista os arquivos em ordem decrescente de modificação com detalhes completos.
    
2. **`ls -lh`**  
    Lista os arquivos com detalhes e tamanhos em formato legível por humanos.
    
3. **`ls -ltr`**  
    Lista os arquivos em ordem crescente de modificação, com detalhes completos.
    
4. **`ls -lh --full-time`**  
    Lista os arquivos com tamanhos legíveis por humanos e exibe o registro completo de data e hora.
    
5. **`ls -Sr`**  
    Ordena os arquivos por tamanho, do menor para o maior.
    


| **Cor**          | **Tipo de Arquivo**                                   |
| ---------------- | ----------------------------------------------------- |
| **Preto/Branco** | Arquivo regular                                       |
| **Azul**         | Arquivo de diretório                                  |
| **Ciano**        | Arquivo de link simbólico (aponta para outro arquivo) |
| **Verde**        | Arquivo executável (um programa)                      |