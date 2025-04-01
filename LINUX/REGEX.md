| **Símbolo** | **Descrição**                                                                                                 | **Exemplo**                                                                 |
| ----------- | ------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| `.`         | Corresponde a qualquer caractere único.                                                                       | `a.b` corresponde a "acb", "a9b", ou "a_b", mas não a "ab".                 |
| `[ ]`       | Define uma lista ou intervalo de caracteres para corresponder a um caractere.                                 | `[a-z]` corresponde a qualquer letra minúscula.                             |
| `[^ ]`      | Corresponde a qualquer caractere que **não** esteja na lista ou intervalo.                                    | `[^a-z]` corresponde a qualquer caractere que não seja uma letra minúscula. |
| `*`         | Corresponde ao caractere anterior repetido zero ou mais vezes.                                                | `ab*c` corresponde a "ac", "abc", "abbc", ou "abbbc".                       |
| `^`         | Se colocado no início do padrão, o padrão deve corresponder ao início da linha. Caso contrário, é um literal. | `^abc` corresponde a "abc" somente se estiver no início da linha.           |
| `$`         | Se colocado no final do padrão, o padrão deve corresponder ao final da linha. Caso contrário, é um literal.   | `abc$` corresponde a "abc" somente se estiver no                            |


### Observações:

1. **`[ ]` para intervalos:**
    
    - É possível combinar intervalos, como `[a-zA-Z]` para letras maiúsculas e minúsculas.
2. **`^` e `$` para âncoras:**
    
    - São úteis para verificar se o padrão está no início ou no final de uma linha, garantindo correspondências específicas.
3. **`*` para repetições:**
    
    - Similar a "zero ou mais vezes", combina com sequências vazias também.