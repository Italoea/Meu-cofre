### **Usar o comando `sudo`**

A maneira mais comum e segura de obter permissões de superusuário é usando o comando `sudo`. Este comando permite que um usuário com permissões adequadas execute comandos com os privilégios de superusuário (root), sem precisar fazer login diretamente como root.

#### **Sintaxe do `sudo`:**
	`sudo comando`

**Exemplo:** Se você quiser atualizar os pacotes do sistema, pode usar o seguinte comando:
	`sudo apt update`

- Aqui, `sudo` eleva as permissões para que o comando `apt update` seja executado como root.

### **Alterar para o usuário root com `sudo`**

Se você deseja **entrar no modo superusuário** para executar vários comandos sem precisar prefixá-los com `sudo`, pode usar o comando `sudo -i` ou `sudo su`. Isso abre uma sessão interativa do shell como root.

#### **Usar `sudo -i` (shell de root):**
	`sudo -i`

- Isso abrirá um novo shell onde você estará logado como root. O prompt pode mudar para indicar que você está no shell de root (por exemplo, o prompt mudará de `$` para `#`).

#### **Usar `sudo su` (trocar para root):**
	`sudo su`

- Isso também mudará o shell para o root, permitindo que você execute comandos como superusuário.

### **Usar o comando `su` (substituir usuário)**

O comando `su` (substitute user) pode ser usado para mudar para o usuário root, mas **requer a senha de root**. Diferente do `sudo`, o `su` não exige que o usuário tenha permissões no arquivo `sudoers`. No entanto, a prática de usar `sudo` é preferível por questões de segurança, já que o `sudo` permite um controle mais detalhado sobre os comandos e ações permitidas para um usuário.

#### **Usar `su` para se tornar root:**
	`su`

- Depois de executar o comando, o sistema pedirá a **senha de root**. Após inserir a senha corretamente, você terá acesso ao shell de root.


### **Verificar se o Usuário Tem Permissão de Superusuário**

O acesso ao `sudo` é controlado pelo arquivo `/etc/sudoers`. Para verificar se um usuário tem permissões para usar `sudo`, você pode olhar esse arquivo ou verificar com o comando:
	`sudo -l`

- Esse comando lista todos os comandos que o usuário pode executar com `sudo`.

### **Práticas Recomendadas ao Usar o Acesso de Superusuário**

- **Usar `sudo` sempre que possível**: O uso do `sudo` é mais seguro porque ele registra os comandos executados e oferece mais controle, além de ser possível conceder permissões limitadas (com base em um arquivo de configuração).

- **Evitar usar o usuário root diretamente**: Usar a conta root diretamente (com `su`) não é recomendado, pois ela não oferece o controle e a auditoria de comandos que o `sudo` oferece.

- **Rever permissões de sudo**: Se você é o administrador do sistema, pode configurar quais usuários têm permissões de superusuário editando o arquivo `/etc/sudoers` com o comando `visudo`.



### **Exemplo Completo de Uso de `sudo`:**

1. **Atualizando o sistema como root:**
	`sudo apt update && sudo apt upgrade`

2. **Mudando para o shell de root (modo interativo):**
	`sudo -i`

3. **Executando um comando que requer permissões de superusuário:**
	`sudo nano /etc/hosts`

- Este comando abre o editor `nano` para editar o arquivo `/etc/hosts` com permissões de superusuário.

### **Resumo:**

- **`sudo comando`**: Executa um comando como superusuário.
- **`sudo -i` ou `sudo su`**: Entra no shell como superusuário.
- **`su`**: Muda para o usuário root, mas exige a senha de root.
- **Usar `sudo` é mais seguro** do que fazer login diretamente como root.