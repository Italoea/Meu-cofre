
# Configuração de Domínio VTP em Switch Layer 2

## Introdução

O VTP (VLAN Trunking Protocol) é um protocolo da Cisco usado para gerenciar VLANs em uma rede. Ele permite a propagação automática de informações de VLAN para switches em um mesmo domínio VTP.

## Requisitos

- Switches compatíveis com VTP (Cisco).
    
- Conexão entre os switches via trunk.
    
- Definição do modo de operação do VTP.
    

## Configuração do Domínio VTP

### 1. Acessar o Switch

Conecte-se ao switch via console ou SSH e entre no modo privilegiado:

```bash
enable
configure terminal
```

### 2. Definir o Domínio VTP

```bash
vtp domain MEU_DOMINIO
```

Substitua `MEU_DOMINIO` pelo nome desejado para o domínio VTP.

### 3. Definir a Versão do VTP (Opcional)

```bash
vtp version 3
```

Caso deseje utilizar outra versão, substitua `3` por `1` ou `2`.

### 4. Configurar o Modo de Operação

Existem três modos de operação do VTP:

- **Servidor (Server):** Pode criar, modificar e distribuir VLANs.
    
- **Cliente (Client):** Apenas recebe e aplica as VLANs do domínio.
    
- **Transparente (Transparent):** Não participa do VTP, mas repassa os anúncios.
    

**Exemplo de configuração como Servidor:**

```bash
vtp mode server
```

**Exemplo de configuração como Cliente:**

```bash
vtp mode client
```

**Exemplo de configuração como Transparente:**

```bash
vtp mode transparent
```

### 5. Configurar a Senha do VTP (Opcional)

Caso deseje proteger a propagação de VLANs:

```bash
vtp password MINHA_SENHA
```

Substitua `MINHA_SENHA` pela senha desejada.

### 6. Configurar Interfaces Trunk

O VTP precisa de links trunk para propagar VLANs entre switches:

```bash
interface GigabitEthernet0/1
switchport mode trunk
exit
```

Repita para todas as interfaces que conectam outros switches.

### 7. Verificar a Configuração

Para conferir se o VTP está funcionando corretamente:

```bash
show vtp status
```

Isso exibirá o domínio, a versão, o modo e outras informações.

## Conclusão

Agora seu switch Layer 2 está configurado para operar com VTP no domínio especificado. Certifique-se de que todos os switches no domínio estejam configurados corretamente para garantir a propagação adequada das VLANs.