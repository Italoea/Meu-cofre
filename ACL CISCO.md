
### Access Control Lists (ACLs) em Roteadores Cisco

As Access Control Lists são listas de controle de acesso usadas para filtrar o tráfego com base em critérios como endereços IP, protocolos, portas e outras condições. Elas são aplicadas em interfaces de roteadores para controlar o fluxo de pacotes, permitindo ou negando o tráfego com base nas regras definidas.

#### Tipos de ACLs em Cisco:

1. **Standard ACLs**: Filtram o tráfego com base apenas no endereço IP de origem. São identificadas pelos números de 1 a 99 e 1300 a 1999.
    
2. **Extended ACLs**: Permitem filtrar com base em endereço IP de origem e destino, protocolo, porta e outras condições. São identificadas pelos números de 100 a 199 e 2000 a 2699.
    

#### Sintaxe de Configuração Básica:

```plaintext
Router(config)# access-list {number} {permit | deny} {source} [source-wildcard] [destination] [destination-wildcard] [protocol] [port]
```

- **number**: Número da ACL.
    
- **permit | deny**: Indica se o tráfego que corresponder à regra deve ser permitido ou negado.
    
- **source**: Endereço IP de origem ou rede.
    
- **source-wildcard**: Máscara curinga para o endereço IP de origem.
    
- **destination**: Endereço IP de destino ou rede (apenas para ACLs estendidas).
    
- **destination-wildcard**: Máscara curinga para o endereço IP de destino (apenas para ACLs estendidas).
    
- **protocol**: Protocolo a ser filtrado (TCP, UDP, ICMP, etc.).
    
- **port**: Número da porta (opcional).
    

#### Exemplos de Configuração:

1. **Standard ACL**:
    

```plaintext
Router(config)# access-list 1 permit 192.168.1.0 0.0.0.255
```

Neste exemplo, a ACL padrão número 1 permite todo o tráfego originado da rede 192.168.1.0/24.

2. **Extended ACL**:
    

```plaintext
Router(config)# access-list 101 permit tcp any host 192.168.1.10 eq 80
```

Neste exemplo, a ACL estendida número 101 permite tráfego TCP destinado ao host 192.168.1.10 na porta 80 de qualquer origem.

### Máscaras Curinga (Wildcard Masks) em Roteadores Cisco

As máscaras curinga são usadas em conjunto com as ACLs para especificar ranges de endereços IP ou sub-redes. Elas são o inverso das máscaras de sub-rede padrão, onde 0 bits indicam bits que devem ser correspondidos exatamente, e 1 bits indicam bits que são indiferentes.

#### Sintaxe da Máscara Curinga:

- **Wildcard Mask**: Especifica quais partes do endereço IP devem ser verificadas contra a ACL.
    

#### Exemplo de Máscara Curinga:

Para a rede 192.168.1.0/24, a máscara curinga seria 0.0.0.255, permitindo a correspondência com todos os IPs na faixa de 192.168.1.1 a 192.168.1.254.

#### Exemplo de Uso em uma ACL:

```plaintext
Router(config)# access-list 10 permit 192.168.1.0 0.0.0.255
```

Neste exemplo, a máscara curinga 0.0.0.255 é aplicada à rede 192.168.1.0, permitindo que a ACL número 10 corresponda a qualquer IP entre 192.168.1.1 e 192.168.1.254.

### Considerações Finais:

- Ao configurar ACLs, sempre teste e verifique sua configuração para garantir que esteja funcionando conforme esperado.
    
- Utilize ACLs de maneira criteriosa para evitar bloqueios ou permissões não intencionais de tráfego.
    
- As máscaras curinga são essenciais para definir intervalos de IPs ou sub-redes específicos em suas regras de filtragem.
    

Esta documentação fornece uma base sólida para entender e começar a configurar ACLs e máscaras curinga em roteadores Cisco. A prática regular e a familiaridade com a sintaxe são essenciais para o uso eficaz desses recursos de segurança de rede.

A **máscara curinga para um IP específico** (ou seja, um único host) em um roteador Cisco é:

```
0.0.0.0
```

### ✔ Explicação:

A máscara curinga diz ao roteador quais bits do endereço IP devem ser comparados **exatamente**. Quando usamos `0.0.0.0`, estamos dizendo: **“compare todos os 32 bits do endereço IP”**, ou seja, **somente esse IP exato será correspondido**.

---

### 📌 Exemplo:

Se você quiser permitir ou negar tráfego **somente do host 192.168.1.10**, use:

```cisco
access-list 10 permit 192.168.1.10 0.0.0.0
```

Ou, com ACL estendida:

```cisco
access-list 100 permit tcp host 192.168.1.10 any eq 80
```

---

### ✅ Dica:

Você também pode usar o atalho `host`:

```cisco
access-list 10 permit host 192.168.1.10
```

Isso é exatamente igual a:

```cisco
access-list 10 permit 192.168.1.10 0.0.0.0
```

---
![[Pasted image 20250515103823.png]]
