| **Opção** | **Função**                                                                                                                                                                     | **Exemplo**                                                         |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------- |
| `-t:`     | Especifica o delimitador de campo. Útil quando os campos do arquivo ou entrada são separados por caracteres diferentes de espaço, como vírgulas ou dois-pontos.                | `sort -t: -k3 mypasswd` (Usa `:` como delimitador entre campos).    |
| `-k3`     | Define o número do campo para realizar a ordenação. O argumento indica o campo que será usado, começando em 1 para o primeiro campo.                                           | `sort -t: -k3 mypasswd` (Ordena pelo terceiro campo).               |
| `-n`      | Realiza uma ordenação numérica. É útil quando os valores nos campos contêm números, permitindo que a ordenação leve em conta seu valor numérico em vez de ordem lexicográfica. | `sort -t: -k3 -n mypasswd` (Ordena numericamente o terceiro campo). |

### Observações:

1. **Uso combinado de opções:**

- É comum usar `-t`, `-k`, e `-n` em conjunto para especificar o delimitador, o campo, e o tipo de ordenação. Por exemplo:
	`sort -t: -k3 -n mypasswd

- Ordena os dados do arquivo `mypasswd` pelo terceiro campo, usando `:` como delimitador, e realiza uma ordenação numérica.

- **Padrão do `sort`:**
    
    - Sem a opção `-t`, o comando considera espaços ou tabulações como delimitadores padrão.
    - Sem `-k`, a ordenação ocorre com base no conteúdo completo das linhas.
- **Flexibilidade:**
    
    - As opções podem ser combinadas de diversas maneiras para atender a necessidades específicas, como ordenação por múltiplos campos ou diferentes delimitadores.



| **Opção** | **Função**                                                   | **Exemplo**                 |
| --------- | ------------------------------------------------------------ | --------------------------- |
| `-t,`     | Especifica a vírgula como delimitador de campo.              | `sort -t, arquivo.csv`      |
| `-k2`     | Classifica as linhas com base no conteúdo do segundo campo.  | `sort -t, -k2 arquivo.csv`  |
| `-k1n`    | Classifica numericamente com base no primeiro campo.         | `sort -t, -k1n arquivo.csv` |
| `-k3`     | Classifica as linhas com base no conteúdo do terceiro campo. | `sort -t, -k3 arquivo.csv`  |


### Observações:

1. **Combinando opções:**
- As opções podem ser usadas juntas para criar classificações complexas.  

- Exemplo:
	`sort -t, -k1n -k3 arquivo.csv

- Este comando classifica numericamente pelo primeiro campo e, em seguida, pelo terceiro campo.


1. **Uso do delimitador:**
- O delimitador especificado com `t`(neste caso, `,`) substitui o padrão de espaços/tabulações para separar campos.

1. **Ordenação numérica (`-n`):**
- O `-n` após um campo (`-k1n`) realiza a classificação com base no valor numérico, ideal para campos contendo números.

