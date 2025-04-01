| **Símbolo/Comando** | **Descrição**                                                                                                    | **Exemplo**                                                             |
| ------------------- | ---------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| `.`                 | Corresponde a qualquer caractere único.                                                                          | `grep "a.b" arquivo.txt` encontra "acb", "a9b", mas não "ab".           |
| `[ ]`               | Define uma lista ou intervalo de caracteres para corresponder a um caractere.                                    | `grep "[a-z]" arquivo.txt` encontra letras minúsculas.                  |
| `[^ ]`              | Corresponde a qualquer caractere que **não** esteja na lista ou intervalo.                                       | `grep "[^0-9]" arquivo.txt` encontra caracteres que não são números.    |
| `*`                 | Corresponde ao caractere anterior repetido zero ou mais vezes.                                                   | `grep "ab*c" arquivo.txt` encontra "ac", "abc", "abbc".                 |
| `^`                 | Indica que o padrão deve estar no **início** da linha. Caso contrário, é tratado como um literal.                | `grep "^abc" arquivo.txt` encontra "abc" apenas no início de uma linha. |
| `$`                 | Indica que o padrão deve estar no **final** da linha. Caso contrário, é tratado como um literal.                 | `grep "abc$" arquivo.txt` encontra "abc" apenas no final de uma linha.  |
| `\`                 | Escapa caracteres especiais para tratá-los como literais.                                                        | `grep "\^abc" arquivo.txt` procura pelo literal `^abc`.                 |
| `                   | `                                                                                                                | Usado como operador **OU** (necessário com `grep -E` ou `egrep`).       |
| `?`                 | Corresponde ao caractere anterior zero ou uma vez (necessário com `grep -E`).                                    | `grep -E "ab?c" arquivo.txt` encontra "ac" ou "abc".                    |
| `+`                 | Corresponde ao caractere anterior uma ou mais vezes (necessário com `grep -E`).                                  | `grep -E "ab+c" arquivo.txt` encontra "abc", "abbc", mas não "ac".      |
| `{n,m}`             | Especifica um número mínimo **n** e máximo **m** de repetições do caractere anterior (necessário com `grep -E`). | `grep -E "a{2,4}" arquivo.txt` encontra "aa", "aaa", ou "aaaa".         |
| `()`                | Agrupa padrões (necessário com `grep -E`).                                                                       | `grep -E "(cat                                                          |


### Observações:

1. **`grep -E` ou `egrep`:**
    
    - Use para habilitar padrões avançados (expressões regulares estendidas).
2. **Case Sensitivity:**
    
    - Por padrão, o `grep` diferencia maiúsculas de minúsculas. Use `grep -i` para ignorar diferenças de caso.
3. **Combinação com Pipes e Arquivos:**
    
    - O `grep` pode ser usado em conjunto com outros comandos ou para buscar diretamente em múltiplos arquivos:
	    `cat arquivo.txt | grep "padrão"
	``grep "padrão" arquivo1.txt arquivo2.txt
