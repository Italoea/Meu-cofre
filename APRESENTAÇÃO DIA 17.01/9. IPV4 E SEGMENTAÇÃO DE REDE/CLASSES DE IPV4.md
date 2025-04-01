


Formado por quatro números (de 001 á 255)


Precisa de uma máscara de subrede

Exemplo:
Endereço IP: 192.168.0.2
Máscara de Subrede:255.255.255.0

Muitas vezes precisam de um "gateway"


### **Classes de Endereço

**Classe A
- Primeiro octeto entre 1~126
(Em binário, o primeiro bit do primeiro octeto é zero)
- máscara padrão: 255.0.0.0

**Classe B
- Primeiro octeto entre 192 até 191
(Em binário, o primeiro bit do primeiro octeto deve ser 1 e o segundo bit 0)
- Máscara padrão:255.255.0.0

**Classe C
- Primeiro octeto entre 192 até 223
(EM binário, os dois primeiros bits devem ser 1 e o terceiro 0)
- Máscara padrão:255.255.255.0


# Endereço público, Privado, Loopback, Auto-configuração(Automatic Private IP Adressing)

- **Endereço Público: Usado na internet
- **Endereço Privado: usado em redes internas:
### Classe A: 10.0.0.0 -- 10.255.255.255
### Classe B: 172.16.0.0 -- 172.31.255.255
### Classe C: 192.168.0.0 -- 192.168.255.255

## **Endereço Loopback: usado para teste: 127.X.X.X


## **Endereço de auto configuração: 169.254.X.X

