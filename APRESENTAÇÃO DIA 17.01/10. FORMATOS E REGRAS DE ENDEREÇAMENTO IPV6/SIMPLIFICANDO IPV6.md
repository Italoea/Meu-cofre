O IPv6 (Internet Protocol version 6) foi criado para substituir o IPv4, devido à escassez de endereços disponíveis. Ele utiliza endereços de 128 bits, divididos em grupos de 16 bits representados em hexadecimal, separados por dois pontos (`:`).

## Estrutura do IPv6

Um endereço IPv6 típico é formado por 8 blocos de 4 dígitos hexadecimais (16 bits cada). Um exemplo seria:

`2001:0db8:85a3:0000:0000:8a2e:0370:7334`

### Regras para simplificação

Para tornar os endereços IPv6 mais fáceis de ler, as seguintes regras podem ser aplicadas:

1. **Remoção de zeros à esquerda**: Os zeros iniciais de cada bloco podem ser omitidos.
    
    - Exemplo: `2001:0db8:0000:0000:8a2e:0370:7334` pode ser simplificado para `2001:db8:0:0:8a2e:370:7334`.
2. **Substituição de sequências de blocos `0000` por `::`**: Uma sequência contínua de blocos contendo apenas zeros pode ser substituída por `::`, mas isso só pode ser feito uma vez em um endereço.
    
    - Exemplo: `2001:db8:0:0:0:0:0:1` pode ser simplificado para `2001:db8::1`.
3. **Blocos finais de zeros**: Blocos de zeros ao final podem ser eliminados com a substituição por `::`.
    
    - Exemplo: `2001:db8:0:0:0:0:0:0` pode ser simplificado para `2001:db8::`.

### Exemplos

- Endereço completo: `2001:0db8:0000:0000:8a2e:0370:7334`
- Após simplificação: `2001:db8::8a2e:370:7334`

### Tipos de endereços IPv6

1. **Unicast**: Identifica um único nó na rede.
2. **Multicast**: Envia pacotes para vários nós simultaneamente.
3. **Anycast**: Permite que um pacote seja enviado para o nó mais próximo (em termos de rota) de um grupo.
4. **Endereços especiais**:
    - **Endereço de loopback**: `::1`
    - **Endereço não especificado**: `::`

O IPv6 melhora a capacidade de roteamento, segurança, e suporta um número virtualmente ilimitado de dispositivos conectados.