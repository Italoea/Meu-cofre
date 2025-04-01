### **Exemplo de Máscaras de Sub-rede Comuns**

Aqui estão alguns exemplos de máscaras de sub-rede comuns e como elas são representadas na notação CIDR:

| Máscara de Sub-rede | Notação CIDR | Descrição                                                 |
| ------------------- | ------------ | --------------------------------------------------------- |
| 255.255.255.0       | /24          | Uma rede com até 256 endereços (254 hosts utilizáveis).   |
| 255.255.0.0         | /16          | Uma rede com até 65.536 endereços (65.534 hosts).         |
| 255.0.0.0           | /8           | Uma rede com até 16.777.216 endereços (16.777.214 hosts). |


### A **máscara de sub-rede** no IPv4 é um conceito fundamental utilizado para dividir uma rede IP em sub-redes menores. Ela define quais partes do endereço IP são responsáveis pela **identificação da rede** e quais partes são usadas para identificar os **dispositivos (hosts)** dentro dessa rede. A máscara de sub-rede ajuda a separar a parte da rede e a parte do host de um endereço IP.



#### **Estrutura de uma Máscara de Sub-rede**

Uma máscara de sub-rede é composta por 32 bits, assim como um endereço IP, e é escrita em notação **decimal pontuada**. A máscara pode ser representada de duas formas principais:

- **Notação padrão (muito usada em configurações)**: Como `255.255.255.0`, `255.255.0.0`, etc.
- **Notação CIDR (Classless Inter-Domain Routing)**: Como `/24`, `/16`, etc. Onde o número após a barra indica quantos bits da máscara são usados para a parte de rede.

### A máscara de sub-rede no IPv4 é usada para dividir uma rede em sub-redes menores, facilitando o roteamento e a administração de redes. Ela determina quais bits do endereço IP correspondem à rede e quais correspondem aos hosts, ajudando a definir o escopo de endereços válidos dentro de uma rede específica. A combinação do endereço IP e da máscara de sub-rede permite que dispositivos na mesma rede se comuniquem diretamente, enquanto dispositivos em redes diferentes dependem de roteadores para se comunicarem.