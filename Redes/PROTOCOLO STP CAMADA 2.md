

### O protocolo Spanning Tree Protocol é um protocolo baseado em um algorítmo criado pela engenheira de software Radia Perlman que garente que não ocorrerá loop em um rede local.


### O protocolo STP possibilita a inclusão de ligações redundantes entre  os computadores"  provendo caminhos alternativos no caso de falha de uma dessas ligações. Nesse contexto, ele serve para evitar a formação de loops entre os comutadores e permitir a ativação e desativação automática dos caminhos alternativos.



# O que o Spanning tree IEEE 802.1d faz?

### O algoritmo spanning tree coloca cada porta de bridge/switch no estado forwarding ou no estado blocking. Considera-se que todas as portas no estado forwarding em um dado momento estão na spanning tree ativa. O conjunto de portas no estado forwarding cria um único caminho pelo qual os quadros são enviados entre os segmentos.



![[Pasted image 20241104165816.png]]


# BPDU's

### O bloco BPDU é um recurso que defende a topologia STP de um aplicativo ou dispositivo de usuário mal comportado ou uma ameaça. Você deve habilitar o guarda BPDU nas interfaces que não devem receber nenhuma BPDUs.


![[Pasted image 20241105140327.png]]



### O STP, definido pelo padrão IEEE 802.1d, é um protocolo que funciona ao nível da **camada 2 do modelo OSI** e tem como principal objetivo controlar ligações redundantes, garantindo o desempenho de uma rede.
