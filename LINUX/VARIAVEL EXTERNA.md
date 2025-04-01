#### O comando which procura a localização de um comando pesquisando a variável PATH.

	sysadmin@localhost:~$ which ls                                       
	/bin/ls                                                               
	sysadmin@localhost:~$ which cal                                        
	/usr/bin/cal

#### Para comandos externos, o comando type exibe a localização do comando:
	sysadmin@localhost:~$ type cal                                      
	cal is /usr/bin/cal

#### Usar a opção -a do comando type exibe todos os locais que contêm o comando chamado:

	**sysadmin@localhost:~$** type -a echo                                      
	echo is a shell builtin                                                
	echo is /bin/echo