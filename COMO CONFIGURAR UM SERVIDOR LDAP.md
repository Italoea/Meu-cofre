## PARA INSTALR O LDAP E SUAS DEPENDÊNCIAS:

```
sudo apt install slapd ldap-utils
```

## PARA TER UM WIZARD (Configuração guiada)

```
sudo dpkg-reconfigure slapd
```

![[Pasted image 20250513131438.png]] [NO]

## INSIRA SEU DOMINIO:

![[Pasted image 20250513131508.png]]

## ESCREVA O NOME DA SUA ORGANIZAÇÃO(Tendo contexto do dominio)

![[Pasted image 20250513131616.png]]



![[Pasted image 20250513131638.png]]
[NO]


![[Pasted image 20250513131703.png]]

[YES]

## PRONTO DOMINIO CRIADO!

#### AGORA PARA CRIAR UMA OU (Unidade organizacional):

```sh
nano ou_colaboradores
dn: ou:Colaboradores,dc=worldskillsbrasil,dc=com,dc=br
objectClass: OrganizationalUnit
ou: Colaboradores
```

#### PARA CRIAR A OUTRA OU:

```sh
nano ou_visitantes
dn: ou:Visitantes,dc=worldskillsbrasil,dc=com,dc=br
objectClass: OrganizationalUnit
ou: Visitantes
```

## SCRIPT PARA CRIAR 100 USUARIOS:
./gerar_usuarios
```sh
#!/bin/bash  # Usa o interpretador Bash

OUTPUT="ou_visitantes.ldif"  # Nome do arquivo LDIF de saída
BASE_DN="ou=Visitantes,dc=worldskillsbrasil,dc=com,dc=br"  # DN base onde os usuários serão criados no LDAP

> "$OUTPUT"  # Limpa o conteúdo do arquivo de saída (ou cria novo se não existir)

for i in $(seq 2 100); do  # Loop de 2 até 100 com preenchimento de zeros à esquerda (002, 003, ..., 100)
  USER="Visit$(printf "%03d" $i)"  # Formata o nome do usuário como Visit002, Visit003, ..., Visit100

  cat <<EOF >> "$OUTPUT"  # Inicia bloco de texto (heredoc) e redireciona o conteúdo para o arquivo LDIF
dn: uid=$USER,$BASE_DN  # DN completo do usuário no LDAP
objectClass: inetOrgPerson  # Classe de objeto usada para representar uma pessoa no LDAP
sn: $USER  # Sobrenome (required pelo schema inetOrgPerson)
cn: $USER  # Nome comum (common name)
uid: $USER  # ID do usuário
userPassword: P@ssw0rd  # Senha do usuário (pode ser criptografada ou em texto plano, dependendo da config do LDAP)

EOF  # Fim do bloco heredoc
done  # Fim do loop

echo "Arquivo LDIF gerado: $OUTPUT"  # Mensagem final informando que o arquivo foi gerado

```

## PARA ADICONAR USUARIOS NO DB LDAP:

```bash
ldapadd -x -D "cn=admin,dc=worldskillsbrasil,dc=com,dc=br" -W -f visitante001.ldif
```
