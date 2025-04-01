
#### Variáveis ​​de ambiente, também chamadas de variáveis ​​globais, estão disponíveis em todo o sistema, em todos os shells usados ​​pelo Bash ao interpretar comandos e executar tarefas. O sistema recria automaticamente variáveis ​​de ambiente quando um novo shell é aberto. Exemplos incluem as variáveis ​​PATH, HOME e HISTSIZE. A variável HISTSIZE define quantos comandos anteriores armazenar na lista de histórico. O comando no exemplo abaixo exibe o valor da variável HISTSIZE:

	sysadmin@localhost:~$ echo $HISTSIZE
	1000

#### Para modificar o valor de uma variável existente, use a expressão de atribuição:

	sysadmin@localhost:~$ HISTSIZE=500                                          
	sysadmin@localhost:~$ echo $HISTSIZE                              
	500


#### Quando executado sem argumentos, o comando env produz uma lista de variáveis ​​de ambiente. Como a saída do comando env pode ser bem longa, os exemplos a seguir usam uma pesquisa de texto para filtrar essa saída.


#### O comando export é usado para transformar uma variável local em uma variável de ambiente.

	export variable

#### Após exportar a variável1, ela agora é uma variável de ambiente. Agora ela é encontrada na busca por meio das variáveis ​​de ambiente:
	sysadmin@localhost:~$ export variable1                                  
	sysadmin@localhost:~$ env | grep variable1
	variable1=Something

#### O comando export também pode ser usado para tornar uma variável uma variável de ambiente após sua criação usando a expressão de atribuição como argumento:
	sysadmin@localhost:~$ export variable2='Else'                           
	sysadmin@localhost:~$ env | grep variable2                             
	variable2=Else

#### Para alterar o valor de uma variável de ambiente, use a expressão de atribuição:

	sysadmin@localhost:~$ variable1=$variable1' '$variable2                
	sysadmin@localhost:~$ echo $variable1                                   
	Something Else


#### Variáveis ​​exportadas podem ser removidas usando o comando unset:

	sysadmin@localhost:~$ unset variable2


