
#### As funções são úteis, pois permitem que um conjunto de comandos seja executado um de cada vez, em vez de digitar cada comando repetidamente. No exemplo abaixo, uma função chamada my_report é criada para executar os comandos ls, date e echo.
	sysadmin@localhost:~$ my_report () {
	ls Documents
	date
	echo "Document directory report"
	}

#### Ao criar uma função, um caractere > aparecerá como um prompt para inserir os comandos para a função. As chaves {} são usadas para informar ao shell quando uma função começa e termina para sair do prompt >.

#### Depois que uma função é criada, o nome da função pode ser invocado do prompt BASH para executar a função:



## Double Pipe

#### command1 || command2
#### O double pipe || é um "ou" lógico. Dependendo do resultado do primeiro comando, o segundo comando será executado ou ignorado.
#### Com o double pipe, se o primeiro comando for executado com sucesso, o segundo comando será ignorado; se o primeiro comando falhar, o segundo comando será executado. Em outras palavras, você está essencialmente dizendo ao shell, "Execute este primeiro comando ou o segundo".
