

---

## **Adicionando uma Máquina Virtual Linux no EVE-NG**

### **1. Baixar a Imagem ISO do Linux**

Primeiramente, faça o download da imagem ISO do sistema operacional Linux desejado. No vídeo, é utilizada a distribuição CentOS 7:

```bash
wget http://mirror.ufam.edu.br/centos/7.9.2009/isos/x86_64/CentOS-7-x86_64-Minimal-2207-02.iso
```



### **2. Criar o Diretório para a Imagem no EVE-NG**

No EVE-NG, é necessário criar um diretório específico para armazenar a imagem do Linux. Por convenção, os diretórios são criados em `/opt/unetlab/addons/qemu/` com um nome que identifica o sistema operacional:

```bash
mkdir /opt/unetlab/addons/qemu/linux-centos-7
```



### **3. Transferir a Imagem ISO para o EVE-NG**

Utilize um cliente SCP ou SFTP, como o WinSCP ou FileZilla, para transferir a imagem ISO baixada para o diretório recém-criado no EVE-NG:

- **Host**: Endereço IP do EVE-NG
    
- **Usuário**: `root`
    
- **Senha**: Senha do root
    
- **Porta**: 22
    

Após conectar, transfira a imagem ISO para o diretório `/opt/unetlab/addons/qemu/linux-centos-7/`.

### **4. Renomear a Imagem ISO para `cdrom.iso`**

No EVE-NG, renomeie a imagem ISO para `cdrom.iso` para padronizar a instalação:

```bash
mv /opt/unetlab/addons/qemu/linux-centos-7/CentOS-7-x86_64-Minimal-2207-02.iso /opt/unetlab/addons/qemu/linux-centos-7/cdrom.iso
```



### **5. Criar um Disco Rígido Virtual para a Máquina Virtual**

Ainda no diretório da imagem, crie um disco rígido virtual no formato QCOW2 para a máquina virtual. No exemplo, é criado um disco de 30 GB:

```bash
cd /opt/unetlab/addons/qemu/linux-centos-7/
qemu-img create -f qcow2 virtioa.qcow2 30G
```



### **6. Adicionar a Máquina Virtual ao EVE-NG**

No ambiente web do EVE-NG:

1. Acesse o laboratório desejado.
    
2. Clique em "Add an Object" e selecione "Node".
    
3. Escolha a opção "Linux" e configure as seguintes opções:
    
    - **Template**: Selecione "Linux".
        
    - **Node Name**: Defina um nome para a VM.
        
    - **Image**: Selecione "linux-centos-7".
        
    - **Quantidade de CPUs**: Defina conforme necessário.
        
    - **Memória RAM**: Defina conforme necessário.
        
    - **Interfaces de Rede**: Adicione conforme necessário.
        
4. Salve as configurações.
    

### **7. Iniciar a Instalação do Linux**

Após adicionar a máquina virtual:

1. Inicie a VM clicando com o botão direito sobre ela e selecionando "Start".
    
2. Abra o console da VM para acompanhar o processo de boot pela imagem `cdrom.iso`.
    
3. Prossiga com a instalação padrão do CentOS 7 ou da distribuição escolhida.
    

### **8. Remover a Imagem ISO Após a Instalação**

Após concluir a instalação do sistema operacional, remova a imagem `cdrom.iso` para evitar que a VM inicialize pelo CD-ROM nas próximas execuções:

```bash
rm /opt/unetlab/addons/qemu/linux-centos-7/cdrom.iso
```



### **9. Comitar as Alterações para Salvar o Estado da VM**

Para garantir que as alterações realizadas na VM sejam salvas e utilizadas em futuras execuções, é necessário comitar as alterações:

1. Identifique o UUID do laboratório e o ID do nó correspondente à VM recém-criada. Essas informações podem ser encontradas na interface web do EVE-NG.
    
2. Acesse o diretório temporário correspondente à VM:
    
    ```bash
    cd /opt/unetlab/tmp/0/<UUID_do_Laboratório>/<ID_do_Nó>/
    ```
    



3. Comite as alterações no disco rígido virtual:
    
    ```bash
    qemu-img commit virtioa.qcow2
    ```
    



---

Seguindo esses passos, você terá uma máquina virtual Linux funcional dentro do EVE-NG, pronta para ser utilizada em seus laboratórios e simulações de rede.