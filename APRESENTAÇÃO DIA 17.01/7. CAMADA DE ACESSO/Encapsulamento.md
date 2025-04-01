

### **Encapsulamento na Ethernet**

O encapsulamento é o processo de adicionar informações extras (metadados) aos dados originais para que eles possam ser transmitidos corretamente por meio da rede. No caso da Ethernet, ele ocorre na camada de enlace do modelo OSI.

1. **Divisão em camadas:**
    
    - Os dados da camada superior (camada de transporte ou aplicação) são empacotados em uma unidade chamada **quadro (frame)**.
    - Cada camada adiciona um cabeçalho ou rodapé, criando o encapsulamento.
2. **Processo de encapsulamento na Ethernet:**
    
    - **Dados:** A carga útil (payload) vem das camadas superiores (por exemplo, um segmento TCP).
    - **Cabeçalho Ethernet:** Contém informações como endereços MAC de origem e destino.
    - **Trailer Ethernet:** Inclui o **CRC (Cyclic Redundancy Check)**, usado para verificar erros.

O encapsulamento garante que os dados sejam identificáveis e possam ser entregues ao destino correto, mesmo em redes complexas.

