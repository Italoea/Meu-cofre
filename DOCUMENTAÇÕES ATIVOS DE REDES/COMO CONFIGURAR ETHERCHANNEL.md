![[Pasted image 20250401141432.png]]
# SW1 
```
interface range e0/1-2
switchport trunk encapsulation dot1q
switchport mode trunk 
channel-group 1 mode auto

```


|Modo|Protocolo|Como Funciona|
|---|---|---|
|**On**|Nenhum|Sem negociação, configuração manual.|
|**PAgP - Auto**|PAgP|Aguarda negociação (não inicia).|
|**PAgP - Desirable**|PAgP|Ativa a negociação (tenta formar o canal).|
|**LACP - Passive**|LACP|Aguarda negociação (não inicia).|
|**LACP - Active**|LACP|Ativa a negociação (tenta formar o canal).|