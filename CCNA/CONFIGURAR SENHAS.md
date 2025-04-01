
Quando você se conecta inicialmente a um dispositivo, você está no modo EXEC do usuário. Este modo é protegido usando o console.

Para proteger o acesso ao modo EXEC do usuário, insira o modo de configuração do console de linha usando o comando de configuração global **line console 0**, conforme mostrado no exemplo. O zero é usado para representar a primeira interface de console (e a única, na maioria dos casos). Em seguida, especifique a senha do modo EXEC do usuário usando o comando **password**_password_. Por fim, ative o acesso EXEC do usuário usando o comando **login**

```sh
Sw-Floor-1# **configure terminal**

Sw-Floor-1(config)# **line console 0**

Sw-Floor-1(config-line)# **password cisco**

Sw-Floor-1(config-line)# **login**

Sw-Floor-1(config-line)# **end**

Sw-Floor-1#
```

O acesso ao console agora exigirá uma senha antes de permitir o acesso ao modo EXEC do usuário.

Para ter acesso de administrador a todos os comandos do IOS, incluindo a configuração de um dispositivo, você deve obter acesso privilegiado no modo EXEC. É o método de acesso mais importante porque fornece acesso completo ao dispositivo.

Para proteger o acesso EXEC privilegiado, use o comando de configuração **enable secret** _password_ global config, conforme mostrado no exemplo.

```sh
Sw-Floor-1# **configure terminal**

Sw-Floor-1(config)# **enable secret class**

Sw-Floor-1(config)# **exit**

Sw-Floor-1#
```

As linhas de terminal virtual (VTY) permitem acesso remoto usando Telnet ou SSH ao dispositivo. Muitos switches Cisco são compatíveis com até 16 linhas VTY numeradas de 0 a 15.

Para proteger linhas VTY, entre no modo VTY de linha usando o comando de configuraão global **line vty 0 15**. Em seguida, especifique a senha do VTY usando o comando **password** _password_. Por fim, ative o acesso VTY usando o comando **login**

Um exemplo de segurança das linhas VTY em um switch é mostrado.


```sh
Sw-Floor-1# **configure terminal**

Sw-Floor-1(config)# 1(config)# **line vty 0 15**

Sw-Floor-1(config-line)# **password cisco**

Sw-Floor-1(config-line)# **login**

Sw-Floor-1(config-line)# **end**

Sw-Floor-1#
```
