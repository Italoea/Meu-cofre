# O que é o User Datagram Protocol (UDP)?


### O User Datagram Protocol, ou UDP, é um protocolo de comunicação utilizado em toda a internet para transmissões especialmente sensíveis ao tempo, tais como reproduções de vídeo ou pesquisas de DNS. Ele acelera as comunicações ao não estabelecer formalmente uma conexão antes que os dados sejam transferidos. Isso permite que os dados sejam transferidos muito rapidamente, mas também pode fazer com que pacotes se percam em trânsito, além de criar oportunidades de exploração na forma de ataques DDoS.



# Como funciona o protocolo UDP?

### Como todos os protocolos de rede, o UDP é um método padronizado de transferência de dados entre dois computadores de uma rede. Em comparação com outros protocolos, o UDP realiza este processo de forma simples: envia pacotes (unidades de transmissão de dados) diretamente para um computador de destino, sem estabelecer uma conexão antes, indicando a ordem desses pacotes ou verificando se eles chegaram como previsto. (Os pacotes UDP são denominados "datagramas").


![[Pasted image 20241107152011.png]]


# APLICAÇÕES DO UDP

- ### Nenhuma conexão é necessária para enviar ou receber dados, portanto, os aplicativos e sistemas operacionais funcionam mais rapidamente.

- #### A transmissão por difusão e multitransmissão está disponível, o que significa que uma transmissão UDP pode enviar dados para múltiplos destinatários.

- #### Ela suporta a perda de pacotes, entregando dados mesmo que estejam incompletos.

- ##### O tamanho menor do pacote e a menor sobrecarga reduzem o atraso de ponta a ponta.

- #### Opera em uma gama maior de condições de rede do que o TCP.

- #### A comunicação UDP é mais eficiente.

- #### Pode transmitir dados ao vivo e em tempo real.

![[Pasted image 20241107145621.png]]

# APLICAÇÕES DO UDP



### O UDP é mais adequado para transferir um fluxo constante de dados ao vivo. Isto permite que muitos usuários tenham acesso aos dados de forma fácil e rápida, se não em perfeitas condições. Um bom exemplo é jogar um jogo online. O UDP pode manter a ação em movimento, apesar de possíveis erros ou perda de dados. Aqui estão algumas aplicações da UDP na vida real.

- Jogos online

- Multitransmissão

- Chamadas de vídeo/videoconferência

- VoIP (chamada de voz por aplicativo)

- Sistemas de nomes de domínio (que traduzem nomes de domínio em endereços de IP)