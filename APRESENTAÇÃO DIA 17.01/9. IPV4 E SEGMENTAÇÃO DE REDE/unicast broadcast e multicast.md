### **Unicast**

- **Definição**: Comunicação entre um único emissor (origem) e um único receptor (destino).
- **Exemplo**: Quando você acessa um site ou envia um e-mail, os dados são enviados diretamente entre o seu dispositivo e o servidor.
- **Uso**: Mais eficiente para comunicações ponto a ponto, como chamadas de vídeo ou downloads.
- **Características**:
    - Baixo impacto na rede, pois envolve apenas dois dispositivos.
    - É o método mais comum em redes.



### **Broadcast**

- **Definição**: Comunicação de um único emissor para todos os dispositivos em uma rede.
- **Exemplo**: Mensagens ARP (Address Resolution Protocol) usadas para descobrir o endereço físico de um dispositivo na rede local.
- **Uso**: Geralmente limitado a redes locais (LAN), pois pode causar congestionamento em redes maiores.
- **Características**:
    - Todos os dispositivos recebem a mensagem, mesmo que não sejam o destino.
    - Usa o endereço MAC de broadcast, como `FF:FF:FF:FF:FF:FF`, em redes Ethernet.
    - Ineficiente para redes grandes, pois pode sobrecarregar os dispositivos.



### **Multicast**

- **Definição**: Comunicação de um único emissor para um grupo específico de dispositivos que tenham "assinado" para receber os dados.
- **Exemplo**: Transmissões de vídeo ao vivo ou streaming de mídia para vários espectadores.
- **Uso**: Ideal para distribuição eficiente de dados para múltiplos dispositivos em grandes redes.
- **Características**:
    - Requer que os dispositivos interessados participem de um grupo multicast.
    - Usa endereços IP específicos para multicast, como o intervalo `224.0.0.0/4` no IPv4.
    - Mais eficiente do que broadcast, pois os dados são enviados apenas para os dispositivos interessados.

### Comparação

|**Tipo**|**Destino**|**Eficiência**|**Uso Principal**|
|---|---|---|---|
|**Unicast**|Um dispositivo específico|Alta|Comunicação ponto a ponto|
|**Broadcast**|Todos os dispositivos na rede|Baixa em redes grandes|Mensagens de descoberta ou alerta|
|**Multicast**|Grupo específico de dispositivos|Alta em grupos grandes|Streaming, videoconferência|
