### **Estrutura do Quadro Ethernet**

O quadro Ethernet é a unidade de transmissão de dados na camada de enlace. Ele segue um formato padronizado para que todos os dispositivos na rede possam interpretá-lo.

#### Estrutura básica de um quadro Ethernet:

| Campo                           | Tamanho (bytes) | Descrição                                                         |
| ------------------------------- | --------------- | ----------------------------------------------------------------- |
| **Preambulo**                   | 7               | Sequência para sincronizar o receptor com o transmissor.          |
| **SFD (Start Frame Delimiter)** | 1               | Indica o início do quadro Ethernet.                               |
| **Endereço MAC de destino**     | 6               | Identifica o dispositivo que deve receber o quadro.               |
| **Endereço MAC de origem**      | 6               | Identifica o dispositivo que enviou o quadro.                     |
| **Tipo/EtherType**              | 2               | Especifica o protocolo da camada superior (ex.: IPv4, IPv6, ARP). |
| **Dados/Payload**               | 46–1500         | Contém os dados úteis da camada superior.                         |
| **FCS (Frame Check Sequence)**  | 4               | Código de verificação para detectar erros na transmissão.         |
### **Detalhes Importantes**

1. **Preambulo e SFD:**
    - O preâmbulo consiste em uma sequência de bits alternados (101010...) que prepara os dispositivos para receber o quadro.
    - O SFD sinaliza o início dos dados reais do quadro.
2. **Endereços MAC:**
    
    - São identificadores exclusivos de 48 bits atribuídos a cada dispositivo na rede.
    - O endereço MAC de destino permite que o quadro seja entregue ao destinatário correto.
3. **EtherType:**
    
    - Este campo indica qual protocolo da camada de rede está encapsulado nos dados (por exemplo, IPv4 usa o valor hexadecimal `0x0800`).
4. **Dados/Payload:**
    
    - Deve ter no mínimo 46 bytes (com preenchimento, se necessário) e no máximo 1500 bytes, dependendo do protocolo usado.
5. **FCS (Frame Check Sequence):**
    
    - É um código de 32 bits gerado pelo remetente e verificado pelo receptor. Ele ajuda a identificar se ocorreram erros durante a transmissão.


### **Exemplo do Funcionamento**

1. **Envio de dados:**
    
    - Um computador deseja enviar um pacote de dados para outro na rede.
    - Os dados são encapsulados em um quadro Ethernet, com endereços MAC e o protocolo indicado no EtherType.
2. **Transmissão:**
    
    - O quadro viaja pelo meio físico (cabos ou Wi-Fi) até chegar ao destino.
3. **Recepção e validação:**
    
    - O dispositivo receptor verifica o FCS para garantir que o quadro não foi corrompido.
    - Em seguida, processa os dados e os encaminha para a camada superior (ex.: camada de rede).


- **Encapsulamento:** Processo de adicionar cabeçalhos e rodapés aos dados para transmissão estruturada.
- **Quadro Ethernet:** Estrutura básica que transporta os dados na camada de enlace, contendo informações como endereços MAC, tipo de protocolo e verificações de erro.