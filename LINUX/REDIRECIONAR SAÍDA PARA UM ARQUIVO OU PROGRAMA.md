

## **1. Redirecionar Saída Padrão para um Arquivo**

A saída padrão é o que um comando normalmente exibe no terminal. Para redirecioná-la para um arquivo, use `>` ou `>>`.

- **Substituir o conteúdo do arquivo (sobrescrever):**
    `comando > arquivo.txt`

- Exemplo:
    `echo "Olá, Mundo!" > saida.txt`
    
- O arquivo `saida.txt` conterá `Olá, Mundo!`.


- **Adicionar ao final do arquivo (sem sobrescrever):**
    `comando >> arquivo.txt`


- Exemplo:
    `echo "Adicionando linha" >> saida.txt`
   
- Isso adicionará `Adicionando linha` ao final de `saida.txt`.

## **Redirecionar Erros para um Arquivo**

Os erros no Linux são enviados para a **saída de erro padrão** (file descriptor `2`). Você pode redirecioná-los separadamente:

- **Enviar apenas erros para um arquivo:**
    `comando 2> erros.txt`

- Exemplo:
    `ls /pasta/inexistente 2> erros.log`


- **Adicionar erros ao arquivo existente:**
    `comando 2>> erros.txt`


## **Redirecionar Saída e Erros Juntos**

Para enviar tanto a saída quanto os erros para o mesmo arquivo:

- **Substituir o conteúdo do arquivo:**
	`comando > arquivo.txt 2>&1`


- Ou de forma mais moderna (Bash 4 e superior):
    `comando &> arquivo.txt`


- **Adicionar ao arquivo existente:**
    `comando >> arquivo.txt 2>&1`
   
- Ou:
    `comando &>> arquivo.txt`

## **Redirecionar Saída para Outro Programa (Pipes)**

Use o operador `|` (pipe) para enviar a saída de um comando como entrada para outro comando:

- **Exemplo simples:**
    `ls | grep .txt`

- Aqui, a saída de `ls` (lista de arquivos) é enviada para `grep`, que filtra arquivos com `.txt`.


- **Encadear múltiplos comandos:**
    `cat arquivo.txt | sort | uniq`

- Isso ordena e remove linhas duplicadas de `arquivo.txt`.

## **Redirecionar Entrada para um Comando**

Você pode redirecionar um arquivo para ser usado como entrada por um comando:

- **Exemplo:**
    `comando < arquivo.txt`


- Exemplo prático:
    `sort < lista.txt`

- Isso ordenará as linhas de `lista.txt`.


## **Redirecionar para `/dev/null` (Descartar Saída)**

Se você não deseja salvar nem exibir a saída, pode redirecioná-la para `/dev/null`, um "buraco negro" virtual:

- **Descartar a saída padrão:**
    `comando > /dev/null`


- **Descartar apenas os erros:**
    `comando 2> /dev/null`


- **Descartar tudo (saída e erros):**
    `comando > /dev/null 2>&1`


## **Combinações Avançadas**

Você pode combinar vários redirecionamentos e pipes para criar fluxos complexos de dados:

- **Salvar saída e exibir no terminal simultaneamente:**
    `comando | tee arquivo.txt`

- Exemplo:
    `ls | tee lista.txt`

-  Isso salva a saída do `ls` em `lista.txt` e também a exibe no terminal.
  
- **Filtrar erros e enviar apenas a saída para outro comando:**
    `comando 2>/dev/null | outro_comando`

## **Resumo dos Operadores de Redirecionamento**

| **Operador** | **Descrição**                           |
| ------------ | --------------------------------------- |
| `>`          | Redireciona saída padrão (sobrescreve). |
| `>>`         | Redireciona saída padrão (adiciona).    |
| `2>`         | Redireciona saída de erro.              |
| `2>>`        | Redireciona erros (adiciona).           |
| `&>`         | Redireciona saída padrão e erros.       |
| `            | `                                       |
| `/dev/null`  | Descartar saída.                        |
