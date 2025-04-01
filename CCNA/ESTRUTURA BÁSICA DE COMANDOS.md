
![[Pasted image 20250218142955.png]]

- **Palavra-chave** - Este é um parâmetro específico definido no sistema operacional (na figura, protocolos ip)
- **Argumento** - Isso não é predefinido; é um valor ou variável definido pelo usuário (na figura, 192.168.10.5)

Após inserir cada comando completo, incluindo palavras-chave e argumentos, pressione a tecla **Enter** para enviar o comando ao intérprete de comando.


| Convenção     | Descrição                                                                                                                                                         |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **negrito**   | O texto em negrito indica comandos e palavras-chave que você digita literalmente como mostrado.                                                                   |
| _itálico_     | O texto em itálico indica argumentos para os quais você fornece valores.                                                                                          |
| `[x]`         | Colchetes indicam um elemento opcional (palavra-chave ou argumento).                                                                                              |
| `{x}`         | Chaves indicam um elemento necessário (palavra-chave ou argumento).                                                                                               |
| [x {y \| z }] | Chaves e linhas verticais entre colchetes indicam uma necessidade dentro de um elemento opcional. Espaços são usados para delinear claramente partes do comando.` |

Por exemplo, a sintaxe para usar o comando **description** é **description** _string._ O argumento é um valor _string_ fornecido pelo usuário. O comando **description** é normalmente usado para identificar a finalidade de uma interface. Por exemplo, digitando o comando,**description Connects to the main headquarter office switch**, descreve onde o outro dispositivo está no final da conexão.

Os exemplos a seguir demonstram as convenções usadas para documentar e utilizar comandos do IOS:

- **ping** _ip-address_ - O comando é **ping** e o argumento definido pelo usuário é o _endereço-IP_ do dispositivo de destino. Por exemplo **ping ping 10.10.10.5**.
- **traceroute** _ip-address_ - O comando é **traceroute** e o argumento definido pelo usuário é o _endereço-IP_ do dispositivo de destino. Por exemplo, **traceroute 192.168.254.254**.

Se um comando é complexo com vários argumentos, você pode vê-lo representado assim:

```sh
 Switch(config-if)# switchport port-security aging {  static | time time |     type   {absolute | inactivity}

```
 
