#### Na maioria das distribuições Linux, o comando ``whatis`` faz a mesma coisa que ``man -f.`` Nessas distribuições, ambos produzirão a mesma saída.


#### Na maioria das distribuições Linux, o comando ``apropos ``faz a mesma coisa que ``man -k``. Nessas distribuições, ambos produzem a mesma saída.


## Onde Esses Comandos Estão Localizados?
#### Para procurar a localização de um comando ou as páginas de manual de um comando, use o comando ``whereis``. Este comando procura por comandos, arquivos de origem e páginas de manual em locais específicos onde esses arquivos são normalmente armazenados:


#### Para encontrar qualquer arquivo ou diretório, use o comando`` locate.`` Este comando pesquisa um banco de dados de todos os arquivos e diretórios que estavam no sistema quando o banco de dados foi criado. Normalmente, o comando para gerar este banco de dados é executado todas as noites.
	sysadmin@localhost:~$ locate gshadow

#### Em muitos casos, é útil começar descobrindo quantos arquivos correspondem. Faça isso usando a opção ``-c ``para o comando locate:
	sysadmin@localhost:~$ locate -c passwd
	107

#### Para limitar a saída produzida pelo comando locate, use a opção ``-b.`` Esta opção inclui apenas listagens que têm o termo de pesquisa no nome base do nome do arquivo. O nome base é a parte do nome do arquivo que não inclui os nomes dos diretórios.
	sysadmin@localhost:~$ locate -c -b passwd
	92

#### Como você pode ver na saída anterior, ainda haverá muitos resultados quando a opção -b for usada. Para limitar a saída ainda mais, coloque um caractere \ na frente do termo de pesquisa. Esse caractere limita a saída a nomes de arquivo que correspondem exatamente ao termo:

	sysadmin@localhost:~$ locate -b "\passwd"               
	/etc/passwd                                                 
	/etc/pam.d/passwd                                          
	/usr/bin/passwd                                             
	/usr/share/doc/passwd                                       
	/usr/share/lintian/overrides/passwd


#### Observe que entrar no nó sobre classificação leva a um subnó do original. Para voltar ao nó anterior, use a tecla ``U.`` Enquanto ``U`` leva ao início do nó um nível acima, a tecla ``L`` retorna ao mesmo local de antes de entrar no nó de classificação.

