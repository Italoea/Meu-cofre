

### A camada de link de dados (ou enlace ) é a segunda camada do modelo OSI e, entre outras, é responsável por traduzir as informações da camada de rede em bits para que então sejam enviadas pela camada física.

![[Pasted image 20241104151136.png]]

### Nessa camada, as mensagens são formatadas em pedaços chamados "frames" ou "quadros" que contém endereços de origem e destino.



# MAC: Essa subcamada diz como os dados serão colocados no meio físico e define qual *endereço físico* do dispositivo. Outras coisas como notificação de erro, de fluxo e a ordem em que os quadros serão enviados podem ser descritos aqui.

![[Pasted image 20241104151635.png]]

- ### O endereço MAC é um endereço de 48 bits sempre em hexadecimal, como por exemplo: 00-23-10-35-00-3B.

- ### Ao invés de traços, ás vezes é escrito com dois pontos entre os números: 00:23:10:35:00:3B.

- ### O endereço MAC é dividido em duas partes, sendo que a primeira identifica o fabricante e a segunda identifica apenas aquela placa de rede.




![[Pasted image 20241104153310.png]]



# LLC: Essa subcamada deve conhecer qual protocolo estará atuando na camada de rede.
# Quando o host recebe o quadro, o cabeçalho presente no LLC dirá para onde aquele quadro deverá ser destinado.

# Essa subcamada também pode fornecer controle de fluxo e sequencia de bits de controle.