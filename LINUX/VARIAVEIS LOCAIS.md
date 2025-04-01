
#### Variáveis ​​locais ou de shell existem apenas no shell atual e não podem afetar outros comandos ou aplicativos. Quando o usuário fecha uma janela de terminal ou shell, todas as variáveis ​​são perdidas. Elas são frequentemente associadas a tarefas baseadas no usuário e são minúsculas por convenção.

#### Para definir o valor de uma variável, use a seguinte expressão de atribuição. Se a variável já existir, o valor da variável será modificado. Se o nome da variável ainda não existir, o shell cria uma nova variável local e define o valor:
	sysadmin@localhost:~$ variável1='Algo'


#### O comando echo é usado para exibir a saída no terminal. Para exibir o valor da variável, use um caractere cifrão $ seguido pelo nome da variável como um argumento para o comando echo:
	sysadmin@localhost:~$ echo $variable1                                   
	Something

