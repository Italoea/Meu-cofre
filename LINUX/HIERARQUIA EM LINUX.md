

### **Hierarquia do Sistema de Arquivos no Linux**

No Linux, o sistema de arquivos segue uma estrutura hierárquica em formato de **árvore invertida**, onde o diretório raiz (`/`) está no topo. Todos os arquivos e diretórios estão organizados de forma lógica abaixo dele. Essa hierarquia padronizada é definida pelo **FHS (Filesystem Hierarchy Standard)**, que determina o propósito de cada diretório.

### **Conceitos Fundamentais**

1. **Raiz (`/`)**
    
    - É o ponto de partida da hierarquia de arquivos.
    - Todos os arquivos e diretórios estão contidos ou montados abaixo de `/`.
    - Diretórios, dispositivos e sistemas de arquivos adicionais são montados dentro dessa estrutura.
2. **Montagem de Sistemas de Arquivos**
    
    - Dispositivos físicos, como discos rígidos e pendrives, são montados em diretórios específicos dentro dessa hierarquia.
    - O Linux permite montar diferentes sistemas de arquivos (ext4, NTFS, etc.) na mesma árvore.
3. **Diretórios Importantes**
    
    - Cada diretório raiz tem um propósito específico, definido pelo FHS. Exemplos incluem `/home` para diretórios de usuários e `/bin` para executáveis essenciais.

### **Estrutura de Diretórios Padrão**

Aqui está uma visão geral dos diretórios comuns na raiz `/` e suas funções:

|Diretório|Descrição|
|---|---|
|**`/`**|Diretório raiz, o topo da hierarquia.|
|**`/bin`**|Contém binários essenciais, como `ls`, `cp` e `bash`, usados por todos os usuários.|
|**`/boot`**|Contém arquivos de inicialização, como o kernel e o GRUB.|
|**`/dev`**|Contém arquivos de dispositivos, como discos e terminais (`/dev/sda`, `/dev/tty`).|
|**`/etc`**|Arquivos de configuração do sistema e de aplicativos.|
|**`/home`**|Diretórios pessoais dos usuários. Ex.: `/home/user1`.|
|**`/lib`**|Bibliotecas compartilhadas usadas pelos binários em `/bin` e `/sbin`.|
|**`/media`**|Pontos de montagem para dispositivos removíveis, como CDs e USBs.|
|**`/mnt`**|Ponto de montagem temporária para sistemas de arquivos adicionais.|
|**`/opt`**|Software opcional instalado manualmente (não gerenciado pelo sistema).|
|**`/proc`**|Sistema de arquivos virtual com informações do kernel e processos em execução.|
|**`/root`**|Diretório pessoal do superusuário (root).|
|**`/run`**|Arquivos temporários de runtime usados durante a inicialização do sistema.|
|**`/sbin`**|Binários essenciais para administração do sistema.|
|**`/srv`**|Dados de serviços fornecidos pelo sistema, como servidores web.|
|**`/tmp`**|Arquivos temporários (geralmente excluídos ao reiniciar).|
|**`/usr`**|Programas e arquivos de usuário, subdividido em `/usr/bin`, `/usr/lib`, etc.|
|**`/var`**|Dados variáveis, como logs, cache e filas de impressão.|
### **Conceitos Avançados**

1. **Sistema de Arquivos Virtual**
    
    - Diretórios como `/proc` e `/sys` não contêm dados reais no disco, mas são sistemas de arquivos virtuais que representam informações dinâmicas sobre o sistema (ex.: processos e dispositivos).
2. **Separação de Usuário e Sistema**
    
    - Diretórios como `/home` e `/var` contêm dados específicos do usuário ou serviços, enquanto diretórios como `/bin` e `/sbin` são usados pelo sistema operacional.
3. **Permissões e Proprietários**
    
    - A estrutura do sistema de arquivos inclui um sistema de permissões que regula o acesso de usuários e grupos a arquivos e diretórios.
4. **Links Simbólicos e Montagem**
    
    - O Linux permite criar **links simbólicos** que apontam para outros arquivos/diretórios e montar sistemas de arquivos em qualquer ponto da hierarquia.