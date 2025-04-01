| **Comando**             | **Descrição**                                    | **Exemplo**              | **Observação**                                                             |
| ----------------------- | ------------------------------------------------ | ------------------------ | -------------------------------------------------------------------------- |
| `head <arquivo>`        | Exibe as 10 primeiras linhas de um arquivo.      | `head arquivo.txt`       | Útil para visualizar o início de arquivos grandes.                         |
| `head -n <N> <arquivo>` | Exibe as primeiras **N** linhas de um arquivo.   | `head -n 5 arquivo.txt`  | Substitua **N** pelo número de linhas desejadas.                           |
| `tail <arquivo>`        | Exibe as 10 últimas linhas de um arquivo.        | `tail arquivo.log`       | Ideal para verificar as mensagens mais recentes de arquivos de log.        |
| `tail -n <N> <arquivo>` | Exibe as últimas **N** linhas de um arquivo.     | `tail -n 20 arquivo.log` | Substitua **N** pelo número de linhas desejadas.                           |
| `tail -f <arquivo>`     | Monitora um arquivo em tempo real.               | `tail -f servidor.log`   | Ótimo para monitorar logs em execução, como os de servidores ou processos. |
| `tail -c <N> <arquivo>` | Exibe os últimos **N** caracteres de um arquivo. | `tail -c 50 arquivo.txt` | Exibe apenas os últimos caracteres, útil para arquivos binários ou texto.  |


### Observações:

1. **Uso conjunto com pipes:**

- Você pode usar **`head`** e **`tail`** em combinação com outros comandos. Exemplo:
	`cat arquivo.txt | tail -n 5

- **Opção `-f` no `tail`:**
    - O **`tail -f`** é especialmente útil para acompanhar logs em tempo real durante a depuração de sistemas ou análise de servidores.
- **Compatibilidade:**
    - Ambos os comandos funcionam em sistemas baseados em Unix/Linux.

### Exemplos:

1. Para exibir as primeiras 15 linhas de um arquivo:
	`head -n 15 arquivo.txt`

2. Para monitorar continuamente os novos registros adicionados a um arquivo de log:
    `tail -f servidor.log`