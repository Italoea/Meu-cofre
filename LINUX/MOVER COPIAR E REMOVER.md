

Aqui está um quadro organizado e detalhado sobre as opções do comando `mv`, incluindo informações adicionais úteis:

|**Opção**|**Significado**|
|---|---|
|`-i`|**Interativo**: Pergunta se um arquivo deve ser sobrescrito.|
|`-n`|**Sem Clobber**: Não sobrescreve o conteúdo de um arquivo de destino.|
|`-v`|**Verbose**: Mostra a movimentação resultante.|

### Informações Adicionais

- **Movimentação de Diretórios**: O comando `mv` move diretórios e seus conteúdos por padrão, sem a necessidade de uma opção específica como `-r`.
- **Sobrescrição**:
    - Se nenhuma opção for usada, o `mv` sobrescreve arquivos existentes no destino **sem aviso**.
    - Use `-i` ou `-n` para evitar perdas de dados inadvertidas.
- **Combinação de Opções**: É possível combinar opções para obter resultados específicos. Exemplo: `mv -iv arquivo1 destino/` exibirá uma confirmação antes de sobrescrever e detalhará a operação.
- **Uso Comum**:
    - Renomear arquivos: `mv arquivo1 novo_nome`.
    - Mover arquivos para outro diretório: `mv arquivo1 diretório/`.




| **Comando** | **Uso Básico**        | **Função**                            | **Principais Opções**                                                                                                     |
| ----------- | --------------------- | ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| `rm`        | `rm arquivo`          | Remove arquivos ou diretórios.        | `-i`: Confirma antes de remover.  <br>`-r`: Remove diretórios e seus conteúdos.  <br>`-f`: Força a remoção sem perguntar. |
| `mv`        | `mv arquivo destino/` | Move ou renomeia arquivos/diretórios. | `-i`: Confirma antes de sobrescrever.  <br>`-n`: Não sobrescreve arquivos existentes.  <br>`-v`: Mostra os movimentos.    |
| `cp`        | `cp arquivo destino/` | Copia arquivos ou diretórios.         | `-i`: Confirma antes de sobrescrever.  <br>`-r`: Copia diretórios recursivamente.  <br>`-v`: Mostra as cópias realizadas. |
### Exemplos Práticos:

1. **Remover Arquivo ou Diretório**
    
    - `rm arquivo.txt`: Remove o arquivo `arquivo.txt`.
    - `rm -r pasta/`: Remove o diretório `pasta` e todo o seu conteúdo.
2. **Mover ou Renomear Arquivos**
    
    - `mv arquivo.txt /home/usuario/`: Move o arquivo para o diretório `/home/usuario/`.
    - `mv arquivo.txt novo_nome.txt`: Renomeia `arquivo.txt` para `novo_nome.txt`.
3. **Copiar Arquivos ou Diretórios**
    
    - `cp arquivo.txt /home/usuario/`: Copia o arquivo para o diretório `/home/usuario/`.
    - `cp -r pasta/ /home/usuario/`: Copia o diretório `pasta` e todo o seu conteúdo para `/home/usuario/`.