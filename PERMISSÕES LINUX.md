

## As permissões são divididas em três partes: 

	primeira parte o tipo do arquivo
	Logo em seguida tem as permissões do dono (user)
	Depois tem as permmissões do grupo "group"
	E a última parte são as permissões de "outros"

```sh
-rw-r--r--

Isto é um arquivo pois começa com "-"
O usuário root pode ler e escrever "rw"
O grupo só pode ler "r"
E outros só pode ler também "r"
```

### PERMISSÕES

	x = Executar 1
	r = ler 4
	w = escrever 2

### TIPOS DE ARQUIVOS
	d = Diretório
	- = arquivo
	l = link aponta pra outro arquivo ou diretório

### COMO DAR PERMISSÃO PARA UM ARQUIVO?

```sh
chmod o+rwx arquivo.txt ou 
g = group
r = ler
w = escrever
x = executar


chmod 764 arquivo.txt 
Para o root ler, escrever e executar 4+2+1
grupo ler e escrever 4+6
outros ler 4


```



### COMO DAR PERMISSÃO PARA UM DIRETÓRIO?

####  O mesmo comando usado para dar permissões para um arquivo é usado para dar permissões para um diretório


### COMO DEFINIR UM DONO PARA UM ARQUIVO:

```sh
chown italo arquivo.txt
```


### COMO ADIOCIONAR UM USUÁRIO EM UM GRUPO:

```sh
chown italo:TI
```

