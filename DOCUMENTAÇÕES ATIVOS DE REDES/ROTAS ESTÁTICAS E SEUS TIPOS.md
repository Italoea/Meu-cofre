
### Resumo sobre Rotas Estáticas e seu Funcionamento em Roteadores

As **rotas estáticas** são caminhos fixos configurados manualmente no roteador para direcionar o tráfego de rede a um destino específico. Diferente das rotas dinâmicas (que são aprendidas automaticamente por protocolos como OSPF ou BGP), as rotas estáticas não mudam a menos que o administrador as altere. Elas são úteis em redes pequenas, estáveis ou quando se deseja controle total sobre o tráfego.

#### Como Funcionam no Roteador:
1. **Configuração Manual**: O administrador define o destino (endereço de rede), a máscara de sub-rede e o próximo salto (gateway ou interface de saída).
2. **Tabela de Roteamento**: O roteador adiciona a rota estática à sua tabela de roteamento. Essa tabela é consultada para decidir como encaminhar pacotes.
3. **Prioridade (Distância Administrativa)**: Rotas estáticas têm uma distância administrativa (AD) padrão de 1, o que as torna preferidas sobre rotas dinâmicas (ex.: OSPF tem AD 110) a menos que o AD seja ajustado.
4. **Encaminhamento**: Quando um pacote chega, o roteador compara o endereço de destino com as entradas na tabela de roteamento e usa a rota estática correspondente para encaminhar o pacote ao próximo salto.
5. **Manutenção**: Como são fixas, rotas estáticas não se adaptam a mudanças na rede (ex.: falhas de link). Se o próximo salto não estiver disponível, o roteador pode descartar os pacotes, a menos que haja uma rota alternativa configurada.

#### Vantagens:
- Simplicidade e previsibilidade.
- Baixo uso de recursos (não exige protocolos de roteamento dinâmico).
- Controle total sobre o caminho do tráfego.

#### Desvantagens:
- Não se ajusta a mudanças na topologia.
- Configuração trabalhosa em redes grandes.

---

### Exemplos de Rotas Estáticas

Vamos usar um cenário simples: um roteador (Router1) conectado a duas redes e à Internet.

#### Topologia:
- **Rede 1**: 192.168.1.0/24 (conectada diretamente ao Router1 via interface GigabitEthernet0/0).
- **Rede 2**: 192.168.2.0/24 (acessível via outro roteador, Router2, com IP 10.0.0.2).
- **Internet**: Acessível via um gateway 10.0.0.1.

#### 1. Rota Estática para uma Rede Específica (Totalmente Especificada)
Para alcançar a Rede 2 (192.168.2.0/24), configuramos uma rota estática no Router1 apontando para o Router2 (10.0.0.2):

```plaintext
Router1(config)# ip route 192.168.2.0 255.255.255.0 10.0.0.2
```

- **Explicação**: Qualquer pacote destinado à Rede 2 será enviado para o IP 10.0.0.2 (Router2). O roteador assume que Router2 sabe como alcançar essa rede.

#### 2. Rota Estática Padrão (Default Route)
Para enviar todo o tráfego que não corresponde a redes conhecidas (como para a Internet) ao gateway 10.0.0.1:

```plaintext
Router1(config)# ip route 0.0.0.0 0.0.0.0 10.0.0.1
```

- **Explicação**: A rota 0.0.0.0/0 é uma "rota padrão". Qualquer pacote sem destino específico na tabela de roteamento será enviado ao gateway 10.0.0.1.

#### 3. Rota Estática com Distância Administrativa Ajustada
Se houver outra rota para a Rede 2 aprendida por um protocolo dinâmico (ex.: OSPF), podemos priorizar a rota estática ajustando sua AD:

```plaintext
Router1(config)# ip route 192.168.2.0 255.255.255.0 10.0.0.2 50
```

- **Explicação**: Aqui, definimos a AD como 50. Se o OSPF (AD 110) também tiver uma rota para 192.168.2.0/24, a estática será preferida (AD 50 < 110).

#### 4. Rota Estática para Interface Diretamente Conectada
Se a Rede 1 (192.168.1.0/24) já está conectada diretamente à interface GigabitEthernet0/0, o roteador a reconhece automaticamente (AD 0). Mas, se precisarmos apontar para uma interface em vez de um próximo salto:

```plaintext
Router1(config)# ip route 192.168.1.0 255.255.255.0 GigabitEthernet0/0
```

- **Explicação**: O tráfego para 192.168.1.0/24 será enviado diretamente pela interface especificada.

---

### Cenário Prático
Imagine que um pacote chega ao Router1 com destino 192.168.2.10:
1. Router1 consulta sua tabela de roteamento.
2. Encontra a rota estática `ip route 192.168.2.0 255.255.255.0 10.0.0.2`.
3. Encaminha o pacote para 10.0.0.2 (Router2).
4. Se o destino fosse 8.8.8.8 (Google DNS), a rota padrão `ip route 0.0.0.0 0.0.0.0 10.0.0.1` seria usada, enviando o pacote ao gateway da Internet.

Rotas estáticas são simples, mas exigem configuração cuidadosa para evitar loops ou perda de pacotes em caso de falhas na rede.