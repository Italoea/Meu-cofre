
Se as alterações feitas na configuração em execução não tiverem o efeito desejado e a configuração ainda não foi salva, você poderá restaurar o dispositivo para a configuração anterior. Remova os comandos alterados individualmente ou recarregue o dispositivo usando o comando de modo EXEC privilegiado **reload** para restaurar o startup-config.

A desvantagem de usar o comando **reload** para remover uma configuração em execução não salva é o breve período de tempo em que o dispositivo ficará offline, causando o tempo de inatividade da rede.

Quando um recarregamento é iniciado, o IOS detecta que a configuração em execução possui alterações que não foram salvas na configuração de inicialização. Um prompt será exibido para pedir que as alterações sejam salvas. Para descartar as alterações, insira **n** ou **no**.

Como alternativa, se alterações indesejadas foram salvas na configuração de inicialização, pode ser necessário limpar todas as configurações. Isso requer apagar a configuração de inicialização e reiniciar o dispositivo. A configuração de inicialização é removida usando o comando do modo EXEC privilegiado **erase startup-config**. Após o uso do comando, o switch solicitará confirmação. Pressione **Enter** para aceitar.

Após remover a configuração de inicialização da NVRAM, recarregue o dispositivo para remover o arquivo de configuração atual em execução da RAM. Ao recarregar, um switch carregará a configuração de inicialização padrão que foi fornecida originalmente com o dispositivo.