
### ✅ 1. **Adicionar entradas (base, OU, usuários)**

### 🔍 2. **Pesquisar usuários (por OU e geral)**

---

## 🧱 **1. Adicionar entradas no LDAP**

### 🔹 a) Adicionar a base do diretório (ex: `dc=worldskillsbrasil,dc=com,dc=br`)

```ldif
# base.ldif
dn: dc=worldskillsbrasil,dc=com,dc=br
objectClass: top
objectClass: domain
dc: worldskillsbrasil
```

```bash
ldapadd -x -D "cn=admin,dc=worldskillsbrasil,dc=com,dc=br" -W -f base.ldif
```

---

### 🔹 b) Criar uma OU (ex: `Visitantes`)

```ldif
# ou_visitantes.ldif
dn: ou=Visitantes,dc=worldskillsbrasil,dc=com,dc=br
objectClass: organizationalUnit
ou: Visitantes
```

```bash
ldapadd -x -D "cn=admin,dc=worldskillsbrasil,dc=com,dc=br" -W -f ou_visitantes.ldif
```

---

### 🔹 c) Adicionar um usuário a uma OU

```ldif
# visitante001.ldif
dn: uid=Visit001,ou=Visitantes,dc=worldskillsbrasil,dc=com,dc=br
objectClass: inetOrgPerson
objectClass: posixAccount
objectClass: top
cn: Visitante 001
sn: Visit001
uid: Visit001
uidNumber: 1001
gidNumber: 100
homeDirectory: /home/Visit001
userPassword: {SSHA}senha_criptografada
```

```bash
ldapadd -x -D "cn=admin,dc=worldskillsbrasil,dc=com,dc=br" -W -f visitante001.ldif
```

---

## 🔎 **2. Buscar usuários**

### 🔹 a) Buscar usuários **dentro de uma OU específica**

```bash
ldapsearch -x -D "cn=admin,dc=worldskillsbrasil,dc=com,dc=br" -W \
-b "ou=Visitantes,dc=worldskillsbrasil,dc=com,dc=br" \
"(objectClass=inetOrgPerson)"
```

> 📌 Mostra todos os usuários da OU `Visitantes`.

---

### 🔹 b) Buscar **todos os usuários do LDAP**, independente da OU

```bash
ldapsearch -x -D "cn=admin,dc=worldskillsbrasil,dc=com,dc=br" -W \
-b "dc=worldskillsbrasil,dc=com,dc=br" \
"(objectClass=inetOrgPerson)"
```

> 🔍 Isso percorre todo o diretório e retorna todos os usuários do tipo `inetOrgPerson`.

---

### 🔹 c) Buscar apenas `uid` (nome de login) dos usuários

```bash
ldapsearch -x -D "cn=admin,dc=worldskillsbrasil,dc=com,dc=br" -W \
-b "dc=worldskillsbrasil,dc=com,dc=br" \
"(objectClass=inetOrgPerson)" uid
```

---

## ✅ Dica Extra: Ver todas as OUs existentes

```bash
ldapsearch -x -D "cn=admin,dc=worldskillsbrasil,dc=com,dc=br" -W \
-b "dc=worldskillsbrasil,dc=com,dc=br" \
"(objectClass=organizationalUnit)" ou
```

---
