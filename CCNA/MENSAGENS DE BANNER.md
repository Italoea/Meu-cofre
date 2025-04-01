
Embora a exigência de senhas seja uma maneira de manter pessoal não autorizado fora da rede, é vital fornecer um método para declarar que apenas pessoal autorizado deve tentar acessar o dispositivo. Para fazê-lo, adicione um banner à saída do dispositivo. Banners podem ser uma parte importante do processo legal caso alguém seja processado por invadir um dispositivo. Alguns sistemas legais não permitem processo, ou mesmo o monitoramento de usuários, a menos que haja uma notificação visível.

Para criar uma mensagem de faixa do dia em um dispositivo de rede, use o comando de configuração global **banner motd #**_a mensagem do dia_**#**. O “#” na sintaxe do comando é denominado caractere de delimitação. Ele é inserido antes e depois da mensagem. O caractere de delimitação pode ser qualquer caractere contanto que ele não ocorra na mensagem. Por esse motivo, símbolos como “#” são usados com frequência. Após a execução do comando, o banner será exibido em todas as tentativas seguintes de acessar o dispositivo até o banner ser removido.

O exemplo a seguir mostra as etapas para configurar o banner no Sw-Floor-1.

```sh
Sw-Floor-1# **configure terminal**

Sw-Floor-1(config)# **banner motd #a mensagem do dia#**
```

