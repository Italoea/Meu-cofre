
# SCRIPT PARA GERAR USUÁRIOS, GID E UID

```sh
# Nome do arquivo LDIF de saída
OUTPUT="visitantes.ldif"

# DN base onde os usuários serão criados no LDAP
BASE_DN="ou=Visitantes,dc=worldskillsbrasil,dc=com,dc=br"

# Remove o arquivo de saída caso já exista (para evitar duplicações)
> "$OUTPUT"

# Loop de 1 a 100 para gerar 100 usuários
for i in $(seq 1 100); do
    # Define o nome do usuário, com o número preenchido com zeros (ex: visit001, visit002...)
    USER=Visit$(printf "%03d" $i)

    # Define o UID (número único de identificação do usuário), começando em 23001 (ex: 23001, 23002...)
    USER_ID=2$(printf "03d" $i)

    # Adiciona as entradas no arquivo LDIF
    cat <<EOF >> "$OUTPUT"
dn: uid=$USER,$BASE_DN
objectClass: inetOrgPerson
objectClass: posixAccount
sn: $USER
cn: $USER
uid: $USER
uidNumber: $USER_ID
gidNumber: $USER_ID
homeDirectory: /home/$USER
loginShell: /bin/bash
userPassword: P@ssword
EOF
done

# Mensagem final confirmando a geração do arquivo
echo "Arquivo LDIF gerado: $OUTPUT"

```
![[Pasted image 20250515162738.png]]