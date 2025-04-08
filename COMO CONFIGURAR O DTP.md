## (Dynamic Trunk Protocol)

---

# 📘 Documentação: Configuração do Protocolo DTP (Dynamic Trunking Protocol)

## ✅ O que é o DTP?

O **DTP (Dynamic Trunking Protocol)** é um protocolo proprietário da Cisco utilizado para negociar dinamicamente o encapsulamento e o estado da porta (acesso ou trunk) entre switches.

> ⚠️ **Atenção**: DTP só funciona entre dispositivos Cisco e deve ser desabilitado em ambientes onde há switches de outros fabricantes ou onde segurança é uma preocupação.

---

## 🎯 Objetivo

Configurar as portas de switch para:

- Usar DTP e negociar dinamicamente o trunking.
    
- Ou forçar uma porta a trunk ou acesso e evitar negociações automáticas (melhor prática para segurança).
    

---

## 📌 Modos do DTP

|Modo|Descrição|
|---|---|
|`access`|Força a porta a ser modo acesso. DTP desativado.|
|`trunk`|Força a porta a ser trunk. Envia DTP.|
|`dynamic auto`|Espera receber DTP para formar trunk. Não envia.|
|`dynamic desirable`|Envia e escuta DTP. Forma trunk se possível.|
|`nonegotiate`|Força trunk e desativa DTP (usado com switches que não suportam DTP).|

---

## 🛠️ Exemplo de Topologia

```
SwitchA ----------- SwitchB
 Fa0/1               Fa0/1
```

---

## 🧪 Exemplo de Configuração

### 🔹 SwitchA - Modo `dynamic desirable`

```bash
SwitchA> enable
SwitchA# configure terminal
SwitchA(config)# interface fastethernet0/1
SwitchA(config-if)# switchport mode dynamic desirable
SwitchA(config-if)# switchport trunk encapsulation dot1q
SwitchA(config-if)# no shutdown
SwitchA(config-if)# exit
SwitchA(config)# exit
```

### 🔹 SwitchB - Modo `dynamic auto`

```bash
SwitchB> enable
SwitchB# configure terminal
SwitchB(config)# interface fastethernet0/1
SwitchB(config-if)# switchport mode dynamic auto
SwitchB(config-if)# switchport trunk encapsulation dot1q
SwitchB(config-if)# no shutdown
SwitchB(config-if)# exit
SwitchB(config)# exit
```

> Resultado: Como um lado está em `dynamic desirable` e o outro em `dynamic auto`, **o trunk será formado automaticamente**.

---

## 🔐 Segurança: Como Desabilitar o DTP

Em portas onde **não se deseja trunking**, desabilite o DTP:

```bash
Switch(config)# interface fastethernet0/2
Switch(config-if)# switchport mode access
Switch(config-if)# switchport nonegotiate
```

---

## 🔍 Verificação

### Verificar o estado da porta:

```bash
Switch# show interfaces fa0/1 switchport
```

### Verificar se a interface está em trunk:

```bash
Switch# show interfaces trunk
```

---

## ✅ Boas Práticas

- Em ambientes de produção, **evite usar DTP**. Prefira configurar trunk e access estaticamente.
    
- Use `switchport nonegotiate` em trunks com equipamentos que não suportam DTP.
    
- Sempre documente quais portas estão em trunk e quais em acesso.
    

---

