
- **startup-config** - Este é o arquivo de configuração salvo armazenado na NVRAM. Ele contém todos os comandos que serão usados pelo dispositivo na inicialização ou reinicialização. O flash não perde seu conteúdo quando o dispositivo está desligado.
- **running-config** - Isto é armazenado na memória de acesso aleatório (RAM). Ele reflete a configuração atual. A modificação de uma configuração ativa afeta o funcionamento de um dispositivo Cisco imediatamente. A RAM é uma memória volátil. Ela perde todo o seu conteúdo quando o dispositivo é desligado ou reiniciado.

O comando **show running-config** do modo EXEC privilegiado é usado para visualizar a configuração em execução. Como mostrado no exemplo, o comando irá listar a configuração completa atualmente armazenada na RAM.

```sh
Sw-Floor-1# **show running-config**

Building configuration...

Current configuration : 1351 bytes

!

! Last configuration change at 00:01:20 UTC Mon Mar 1 1993

!

version 15.0

no service pad

service timestamps debug datetime msec

service timestamps log datetime msec

service password-encryption

!

hostname Sw-Floor-1

!
(output omitted)
```

Para visualizar o arquivo de configuração de inicialização, use o comando EXEC privilegiado **show startup-config**.

Se a energia do dispositivo for perdida ou se o dispositivo for reiniciado, todas as alterações na configuração serão perdidas, a menos que tenham sido salvas. Para salvar as alterações feitas na configuração em execução no arquivo de configuração de inicialização, use o comando do modo EXEC privilegiado **copy running-config startup-config**.

Ou **Do wr**
