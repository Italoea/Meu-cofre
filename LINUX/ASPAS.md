
### **Aspas simples (`'`)**

- **Uso**: Envolvem texto literal, impedindo qualquer interpretação ou expansão.
- **Comportamento**: Tudo dentro das aspas simples é tratado exatamente como está. Variáveis e caracteres especiais não são interpretados.

- **Exemplo**:
	`VAR="teste" echo 'O valor da variável é $VAR'`

- **Saída**:
	`O valor da variável é $VAR`

### **Aspas duplas (`"`)**

- **Uso**: Permitem a expansão de variáveis e a interpretação de caracteres especiais (como `$`, `\`, e outros), mas protegem a maioria dos caracteres de serem divididos ou interpretados.
- **Comportamento**: Strings dentro das aspas duplas podem incluir variáveis ou comandos para serem interpretados.

- **Exemplo**:
	`VAR="teste" echo "O valor da variável é $VAR"`

**Saída**:
	`O valor da variável é teste`

### **Acento grave (backticks, ``) e substituição de comando (`$(...)`)**

- **Uso**: Executam o comando dentro das aspas e substituem o resultado.
- **Comportamento**:
    - **Backticks (``): Usados para executar comandos (forma mais antiga, ainda funcional, mas menos recomendada).
    - **`$(...)`**: Substitui o comando pelo resultado (forma moderna e preferida, mais legível e aninhável).

- **Exemplo**:
	`echo "A data atual é $(date)"`

- **Saída**:
	`A data atual é [data atual do sistema]`

## Resumo

| Tipo de Aspas | Expansão de Variáveis | Interpretação de Caracteres Especiais | Substituição de Comandos |
| ------------- | --------------------- | ------------------------------------- | ------------------------ |
| `'` (simples) | Não                   | Não                                   | Não                      |
| `"` (duplas)  | Sim                   | Parcialmente                          | Não                      |
| `\`` ou` $()` | -                     | -                                     | Sim                      |
