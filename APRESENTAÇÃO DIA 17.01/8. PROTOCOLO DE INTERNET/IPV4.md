
### **Características do IPv4**

1. **Endereçamento**:
    
    - O IPv4 usa endereços de **32 bits**, o que resulta em uma quantidade total de **4.294.967.296 (aproximadamente 4 bilhões) de endereços únicos**.
    - Os endereços são geralmente representados em formato **decimal pontuado**, dividido em quatro octetos (ou blocos de 8 bits) separados por pontos, como por exemplo: `192.168.1.1`.
2. **Formato de Endereço**:
    
    - O endereço IPv4 é dividido em quatro partes, chamadas de **octetos**. Cada octeto pode variar de **0 a 255**.
    - Exemplo de endereço IPv4: `192.168.0.1`
    - Cada octeto pode ser escrito como um número decimal, mas seu valor binário equivale a um conjunto de 8 bits.
3. **Classes de Endereço IPv4**:
    
    - O IPv4 organiza os endereços em diferentes **classes** (A, B, C, D, E) para diversos tipos de uso:
        - **Classe A**: Usado para grandes redes (endereços de 1.0.0.0 a 127.255.255.255).
        - **Classe B**: Usado para redes de tamanho médio (endereços de 128.0.0.0 a 191.255.255.255).
        - **Classe C**: Usado para pequenas redes (endereços de 192.0.0.0 a 223.255.255.255).
        - **Classe D**: Usado para multidifusão (endereços de 224.0.0.0 a 239.255.255.255).
        - **Classe E**: Reservado para futuros desenvolvimentos e experimentos (endereços de 240.0.0.0 a 255.255.255.255).
4. **Exaustão de Endereços**:
    
    - Com o aumento da demanda por dispositivos conectados à internet, o espaço de endereçamento do IPv4 começou a se esgotar, especialmente após a popularização de dispositivos móveis e a IoT (Internet das Coisas).
    - Para solucionar a falta de endereços únicos, técnicas como **NAT (Network Address Translation)** e **subnetting** (subdivisão de redes) foram introduzidas.
5. **Cabeçalho IPv4**:
    
    - O cabeçalho de um pacote IPv4 contém informações essenciais, como o endereço de origem, o endereço de destino, o protocolo a ser usado (como TCP ou UDP), a versão do protocolo e outros campos para controle e verificação de erros.
    - **Exemplo de um cabeçalho**:
        - Versão: 4
        - Tamanho do cabeçalho
        - Endereço de origem e destino
        - Protocolo (TCP, UDP, ICMP)
        - Verificação de erro (checksum)
6. **Limitações do IPv4**:
    
    - **Escassez de Endereços**: Como mencionado, o número limitado de endereços IPv4 disponíveis é um dos principais problemas, levando à adoção gradual do **IPv6**.
    - **Segurança**: O IPv4 foi projetado sem uma camada de segurança, o que exigiu o desenvolvimento de soluções externas, como **IPSec**, para garantir a segurança da comunicação.