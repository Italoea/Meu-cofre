
### **Tipos de Links**

1. **Link Físico (Hard Link):**
    
    - Um link direto ao mesmo inode (identificador do sistema de arquivos) de um arquivo.
    - Ambos os nomes apontam para o mesmo arquivo físico.
    - Se o arquivo original for excluído, o link continua funcionando enquanto houver pelo menos um link restante.
2. **Link Simbólico (Soft Link ou Symlink):**
    
    - Um atalho que aponta para o caminho do arquivo original.
    - Pode apontar para arquivos ou diretórios, até mesmo em sistemas de arquivos diferentes.
    - Se o arquivo original for excluído, o link simbólico não funciona (fica quebrado).



### **Criar Links Físicos**

Use o comando `ln` para criar links físicos:
`ln arquivo_origem link_destino`

- Exemplo:
	`ln arquivo.txt link_para_arquivo.txt`

Aqui, `link_para_arquivo.txt` será um link físico para `arquivo.txt`.

**Notas:**

- Links físicos só funcionam dentro do mesmo sistema de arquivos.
- Não é possível criar links físicos para diretórios por padrão (restrição para evitar loops).


### **Criar Links Simbólicos**

Use o comando `ln -s` para criar links simbólicos:
	`ln -s caminho_origem link_destino`

- Exemplo para arquivos:
    `ln -s /caminho/arquivo.txt link_para_arquivo.txt`

- O link simbólico `link_para_arquivo.txt` apontará para `/caminho/arquivo.txt`.


- Exemplo para diretórios:
    `ln -s /caminho/diretorio/ link_para_diretorio`

**Notas:**

- Links simbólicos podem apontar para arquivos ou diretórios, mesmo em sistemas de arquivos diferentes.
- Use `ls -l` para verificar o link. Ele mostrará algo como:
   
    `link_para_arquivo.txt -> /caminho/arquivo.txt`



### **Remover Links**

- Para remover um link (físico ou simbólico), use o comando `rm`:
    `rm link_para_arquivo.txt`

- Isso não remove o arquivo original.

### **Verificar Links**

- Para verificar informações sobre links:
    `ls -l link_destino`


- Para ver todos os links simbólicos em um diretório:
    `find . -type l`

### **Comparação Entre Links**

| **Característica**               | **Link Físico**                  | **Link Simbólico**                 |
| -------------------------------- | -------------------------------- | ---------------------------------- |
| Dependência do arquivo           | Independente do arquivo original | Depende do arquivo original        |
| Pode apontar para diretórios     | Não                              | Sim                                |
| Pode cruzar sistemas de arquivos | Não                              | Sim                                |
| Tamanho                          | Mesmo tamanho do original        | Tamanho pequeno (apenas um atalho) |
