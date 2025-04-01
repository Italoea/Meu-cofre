
Os arquivos startup-config e running-config exibem a maioria das senhas em texto simples. Esta é uma ameaça à segurança, porque qualquer pessoa pode descobrir as senhas se tiver acesso a esses arquivos.

Para criptografar todas as senhas de texto simples, use o comando de configurção global **service password-encryption** conforme mostrado no exemplo.

```sh
Sw-Floor-1# **configure terminal**

Sw-Floor-1(config)# **service password-encryption**

Sw-Floor-1(config)#
```

O comando aplica criptografia fraca a todas as senhas não criptografadas. Essa criptografia se aplica apenas às senhas no arquivo de configuração, não às senhas como são enviadas pela rede. O propósito deste comando é proibir que indivíduos não autorizados vejam as senhas no arquivo de configuração.

Use o comando **show running-config** para verificar se as senhas agora estão criptografadas.

```sh
1(config)# **end**Sw-Floor-

Sw-Floor-1# **show running-config**

!

(Output omitted)

!

line con 0

password 7 094F471A1A0A

login

!

line vty 0 4

password 7 094F471A1A0A

login

line vty 5 15

password 7 094F471A1A0A

login

!

!

end
```
