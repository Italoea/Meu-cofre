## Passo 1: Instalação do BIND

O primeiro passo é instalar o BIND em seu servidor Linux. Você pode fazer isso utilizando o gerenciador de pacotes de sua distribuição. Por exemplo, se estiver utilizando o Ubuntu, execute o seguinte comando:
``

```sh
sudo apt-get install bind9
```
``
## Passo 2: Configuração do arquivo named.conf.default-zones

O próximo passo é configurar as zonas DNS, que são responsáveis por armazenar as informações de resolução de nomes. Existem dois tipos principais de zonas: a zona direta (forward zone) e a zona reversa (reverse zone) em /etc/bind/named.conf.default-zones.

```sh
nano named.conf.default-zones
```

![[Pasted image 20250401082804.png]]
## Para verificar se a sintaxe está certa insira o comando abaixo:

```
named-checkconf /etc/bind/named.conf.default-zones
```
## Passo 3: Configuração dos arquivos de zona

Após configurar as zonas no arquivo named.conf, você deve criar os arquivos de zona correspondentes. Por exemplo, se você configurou uma zona direta para o domínio exemplo.com, crie o arquivo /etc/bind/db.worldskillsbrasil.com.br e adicione os registros DNS dentro dele.

Os arquivos de zona utilizam uma sintaxe específica. Por exemplo, para adicionar um registro A para o domínio exemplo.com, você deve adicionar uma linha como esta:

```sh
nano db.worldskillsbrasil.com.br
```

![[Pasted image 20250401083104.png]]

## Para verificar se a sintaxe do arquivo db. está certa insira o comando abaixo:

```
sudo named-checkzone exemplo.com /etc/bind/db.exemplo.com
```


## Passo 4: Reiniciar o BIND

Após configurar as zonas e os arquivos de zona, reinicie o serviço do BIND para que as configurações entrem em vigor. Você pode fazer isso utilizando o seguinte comando:

```sh
sudo service bind9 restart ou systemctl restart bind9
```

Pronto! Seu servidor DNS no Linux está configurado e pronto para ser utilizado. Agora você pode adicionar seus próprios registros DNS e gerenciar a resolução de nomes em sua rede local ou na internet.

# COMO FAÇO O TESTE?

```sh
host worldskillsbrasil.com.br
```

Se o servidor DNS estiver configurado corretamente irá aparecer um mensagem igual a essa:

![[Pasted image 20250401083606.png]]


## Se o comando não funcionar você pode está inserindo o comando abaixpo:

```
sudo apt-get update
sudo apt-get install bind9-host
```
# NÃO SE ESQUEÇA DE ADICONAR UM IP NA SUA MÁQUINA!!!!

