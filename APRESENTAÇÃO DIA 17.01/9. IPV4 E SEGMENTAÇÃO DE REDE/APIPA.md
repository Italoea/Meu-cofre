
### **Automatic Private IP Adressing/ Endereçamento de IP privado automático

- ### **Endereço de configuração automático no Windows

- ### **Atribui automaticamente IP a uma estação caso falha na comunicação com o servidor DHCP.

- ### **Garante a Comunicação entre as estações dentro de uma rede local


# **FAIXA DE ENDEREÇOS DO APIPA

### Há uma faixa de endereços reservados pelo IETF que são atribuíveis por meio do APIPA:

- ### 169.254.0.1 até 169.254.255.254


### O primeiro e o último blocos dessa faixa são reservados, de modo que as estações na verdade, irão receber endereços localizados entre:

- ### 169.254.1.0 até 169.254.254.255
- ### Máscara de sub rede 255.255.0.0 (Classe B)


# **APLICAÇÕES DO APIPA

### Além de ser um indicativo de que não há conectividade com o servidor DHCP em uma rede, o APIPA pode ajudar a detectar variados problemas, como:

- ### **Patch cable defeituoso
- ### **Servidor DHCP com problema
- ### **Sem conexão adequada á rede sem fio
- ### **Cabeamento fico com problemas
- ### **Problemas em uma ou mais portas do switch

### Ou seja, problemas que, em última instância, levem á quebra de comunicação entre as estações e o servidor DHCP da rede.


