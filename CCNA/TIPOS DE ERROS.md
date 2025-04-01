
| **Tipo de erro      | Descrição**                                                                                                                                                               |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Erros de input**  | Número total de erros. Inclui runts, gigantes, sem buffer, CRC, quadro, sobrecarga e contagens ignoradas.                                                                 |
| **Runts**           | Pacotes descartados por serem menores que o mínimo tamanho do pacote para o meio. Por exemplo, qualquer pacote Ethernet que seja menos de 64 bytes é considerado um runt. |
| **Giants**          | Pacotes descartados porque excedem o tamanho máximo do pacote para o meio. Por exemplo, qualquer pacote Ethernet maior que 1.518 bytes é considerado um gigante.          |
| **CRC**             | Erros CRC são gerados quando a soma de verificação calculada não é a mesma que a soma de verificação recebida.                                                            |
| **Erros de output** | Soma de todos os erros que impediram a transmissão final dos datagramas da interface que está sendo examinada.                                                            |
| **Colisões**        | Número de mensagens retransmitidas devido a uma colisão Ethernet.                                                                                                         |
| **Late Collisions** | Uma colisão que ocorre após 512 bits do quadro terem sido transmitidos.                                                                                                   |


``` sh
Executar um show interfaces

         │
         ▼
A interface está ativada?
      /   \
    Sim    Não
    │        │
    ▼        ▼
• Existem indicações de EMI/ruído? Se sim, remova as fontes.
• Verifique se a configuração duplex está definida corretamente nas duas extremidades.  

             • Verifique os cabos adequados.
             • Verifique se há danos nos cabos e conectores.
             • Verifique se a velocidade está configurada corretamente nas duas extremidades.

         ▼
O problema foi resolvido?
      /   \
    Sim    Não
    │        │
    ▼        ▼
 Concluído   Documente o trabalho e dimensione o problema.

```


### **1. Interface Desativada**

- Verifique se os cabos são apropriados e estão em boas condições.
    
- Se houver suspeita de defeito, substitua o cabo.
    
- Verifique a configuração de velocidade e ajuste manualmente em ambas as extremidades, se necessário.
    

### **2. Interface Ativa com Problemas de Conectividade**

- **Ruído excessivo:**
    
    - Use **show interfaces** para verificar erros (runts, gigantes, CRC).
        
    - Se houver ruído, remova a fonte e verifique o tipo e comprimento do cabo.
        
- **Colisões excessivas:**
    
    - Verifique as configurações duplex.
        
    - Caso haja incompatibilidade, defina manualmente para **full duplex** em ambas as extremidades.