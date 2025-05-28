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
dn: ou=Colaboradores,dc=worldskillsbrasil,dc=com,dc=br
objectClass: OrganizationalUnit
ou: Colaboradores
```

#### PARA CRIAR A OUTRA OU:

```sh
nano ou_visitantes
dn: ou=Visitantes,dc=worldskillsbrasil,dc=com,dc=br
objectClass: OrganizationalUnit
ou: Visitantes
```

## SCRIPT PARA CRIAR 100 USUARIOS:
### ./gerar_usuarios
### [[SCRIPT BASH]]

## PARA ADICONAR USÁRIOS E OU NO LDAP:
```bash
ldapadd -x -D "cn=admin,dc=worldskillsbrasil,dc=com,dc=br" -W -f colaboradores.ldif
```

## APÓS ISSO CONFIGURE O CLIENTE:

```sh
sudo apt update
sudo apt install libnss-ldap libpam-ldap ldap-utils nslcd -y
```

Durante a instalação, será solicitada a configuração inicial:

- **LDAP URI**: `ldap://ip_do_servidor_ldap`
    
- **Distinguished Name base** (Base DN): algo como `dc=seudominio,dc=com,dc=br`
    
- **LDAP versão**: 3
    
- **Permitir login de root local**: Sim
    
- **Configurar libpam-ldap para atualizar senhas**: Sim

Para a maioria das implementações LDAP, ative pelo menos:

- `passwd` (contas de usuário)
    
- `group` (grupos de usuários)
    
- `shadow` (senhas criptografadas)

#### `/etc/nslcd.conf`

Verifique se o conteúdo está assim (ajuste conforme sua rede):

	uri ldap://192.168.0.10/
	base dc=seudominio,dc=com,dc=br
	binddn cn=admin,dc=seudominio,dc=com,dc=br
	bindpw suasenha

### **Testar a conexão LDAP**

#### Testar com `getent`:
```sh
getent passwd usuario_ldap
```
#### Se tudo estiver correto, o sistema deve retornar a linha do usuário como se fosse um usuário local.


### Testar login LDAP:

#### Tente fazer login com um usuário do LDAP, localmente ou via SSH:
```sh
su - usuario_ldap
```
