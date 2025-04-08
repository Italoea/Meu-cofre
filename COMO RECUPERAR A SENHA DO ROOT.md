

---

## 🐧 **Linux (Ubuntu, Debian, CentOS, etc.)**

### ✅ **Se você tem acesso físico ou ao GRUB (modo de boot):**

#### 📌 _Passos para recuperar a senha do root via GRUB:_

1. **Reinicie o sistema.**
    
2. No menu do GRUB, selecione a entrada do seu sistema (geralmente a primeira), mas **não aperte Enter ainda**.
    
3. Pressione `e` para editar os parâmetros de boot.
    
4. Ache a linha que começa com:
    
    ```
    linux /boot/vmlinuz...
    ```
    
5. No final dessa linha, adicione:
    
    ```
    init=/bin/bash
    ```
    
6. Pressione `Ctrl + X` ou `F10` para iniciar com essa configuração.
    
7. O sistema vai iniciar em um shell como root. Agora digite:
    
    ```bash
    mount -o remount,rw /
    passwd
    ```
    
8. Defina a nova senha do root.
    
9. Digite:
    
    ```bash
    sync
    reboot -f
    ```
    
    para reiniciar o sistema.
    

> ⚠️ Esse método requer acesso físico à máquina ou console via IPMI/ILO/iDRAC.

---

### 🔒 **E se o root estiver desabilitado (como no Ubuntu)?**

Se o root estiver desabilitado, você pode trocar a senha com o seu usuário com `sudo`:

```bash
sudo passwd root
```

---

## 🛑 **Importante:**

Se você **não tem acesso físico**, **não tem acesso sudo**, ou a máquina está criptografada, a recuperação de senha pode não ser possível sem reinstalar ou resetar via recovery tools específicas da sua distribuição.

---

Se quiser, posso te ajudar com um passo a passo específico — me diz qual sistema operacional você tá usando.