

### **Criar Arquivos**

- **Criar um arquivo vazio:**
    `touch arquivo.txt`


- **Criar um arquivo com conteúdo:**
    `echo "Conteúdo do arquivo" > arquivo.txt`


- **Editar ou criar com editores de texto:**
    `nano arquivo.txt vi arquivo.txt`


### **Exibir Conteúdo de Arquivos**

- **Mostrar o conteúdo inteiro:**
    `cat arquivo.txt`



- **Exibir as primeiras linhas:**
    `head -n 5 arquivo.txt`



- **Exibir as últimas linhas:**
    `tail -n 5 arquivo.txt`



- **Visualizar um arquivo longo de forma paginada:**
    `less arquivo.txt`



### **Copiar Arquivos**

- **Copiar um arquivo para outro local:**
    `cp arquivo.txt /caminho/novo/`



- **Copiar e renomear simultaneamente:**
    `cp arquivo.txt novo_arquivo.txt`



- **Copiar diretórios recursivamente:**
    `cp -r pasta_origem pasta_destino`



### **Mover e Renomear Arquivos**

- **Mover arquivos:**
    `mv arquivo.txt /caminho/novo/`


- **Renomear um arquivo:**
    `mv arquivo.txt novo_nome.txt`


### **Excluir Arquivos e Diretórios**

- **Excluir um arquivo:**
    `rm arquivo.txt`


- **Excluir diretórios e seus conteúdos:**
    `rm -r pasta/`


- **Confirmar exclusão de arquivos:**
    `rm -i arquivo.txt`


### **Listar Arquivos**

- **Listar arquivos em um diretório:**
    `ls`


- **Listar detalhes (permissões, tamanho, etc.):**
    `ls -l`


- **Listar arquivos ocultos:**
    `ls -a`


### **Buscar Arquivos**

- **Procurar por nome:**
    `find /caminho -name "arquivo.txt"`


- **Procurar por padrão (insensível a maiúsculas):**
    `find /caminho -iname "*.txt"`


- **Buscar dentro do conteúdo dos arquivos:**
    `grep "termo" arquivo.txt`


### **Compactar e Descompactar Arquivos**

- **Compactar arquivos com tar:**
    `tar -czvf arquivo.tar.gz pasta/`


- **Descompactar arquivos tar.gz:**
    `tar -xzvf arquivo.tar.gz`


- **Compactar com zip:**
    `zip arquivo.zip arquivo.txt`


- **Descompactar com unzip:**
    `unzip arquivo.zip`


### **Alterar Permissões e Propriedades**

- **Alterar permissões:**
    `chmod 644 arquivo.txt`


- **Alterar proprietário:**
    `chown usuario:grupo arquivo.txt`


- **Alterar permissões recursivamente:**
    `chmod -R 755 pasta/`

### **. Trabalhar com Links**

- **Criar um link simbólico:**
    `ln -s /caminho/arquivo.txt link_para_arquivo.txt`


- **Criar um link físico:**
    `ln /caminho/arquivo.txt link_fisico.txt`

### **Monitorar Mudanças nos Arquivos**

- **Monitorar um arquivo em tempo real:**
    `tail -f arquivo.log`


- **Monitorar múltiplos arquivos:**
    `tail -f arquivo1.log arquivo2.log`


### **Organizar Arquivos**

- **Criar diretórios:**
    `mkdir nova_pasta`


- **Mover múltiplos arquivos para um diretório:**
    `mv *.txt nova_pasta/`
