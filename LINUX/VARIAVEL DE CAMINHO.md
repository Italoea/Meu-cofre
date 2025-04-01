

### Uma das variáveis ​​mais importantes do shell Bash para entender é a variável PATH. Ela contém uma lista que define em quais diretórios o shell procura para encontrar comandos. Se um comando válido for inserido e o shell retornar um erro "comando não encontrado", é porque o shell Bash não conseguiu localizar um comando com esse nome em nenhum dos diretórios incluídos no caminho. O comando a seguir exibe o caminho do shell atual:

	sysadmin@localhost:~$ echo $PATH                                        
	/home/sysadmin/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games
	sysadmin@localhost:~$


#### Cada diretório na lista é separado por um caractere de dois pontos :. Com base na saída anterior, o caminho contém os seguintes diretórios. O shell verificará os diretórios na ordem em que estão listados:


#### Se o comando não for encontrado em nenhum diretório listado na variável PATH, o shell retornará um erro:

	sysadmin@localhost:~$ zed                                              
	-bash: zed: command not found                                           
	sysadmin@localhost:~$

#### ‌⁠​​⁠​ Se um software personalizado estiver instalado no sistema, pode ser necessário modificar o PATH para facilitar a execução desses comandos. Por exemplo, o seguinte adicionará e verificará o diretório /usr/bin/custom para a variável PATH:

	sysadmin@localhost:~$ PATH=/usr/bin/custom:$PATH    
	sysadmin@localhost:~$ echo $PATH                                       
	/usr/bin/custom:/home/sysadmin/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games
