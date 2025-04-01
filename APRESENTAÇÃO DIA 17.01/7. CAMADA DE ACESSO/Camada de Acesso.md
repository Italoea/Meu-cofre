

## **Pra que serve a camada de acesso?

### **Funções da Camada de Acesso**

1. **Prover Conectividade**:
    
    - É responsável por conectar dispositivos à rede de forma física (cabos) ou sem fio.
2. **Garantir Desempenho e Escalabilidade**:
    - Suporta uma quantidade adequada de dispositivos sem comprometer o desempenho.
    - Implementa recursos como **Power over Ethernet (PoE)** para alimentar dispositivos conectados.
3. **Fornecer Segurança Local**:
    - Realiza autenticação e aplicação de políticas para permitir apenas dispositivos autorizados.
4. **Servir como Interface para Camadas Superiores**:
    - Encaminha o tráfego para a **camada de distribuição**, onde ocorre o roteamento e aplicação de políticas mais complexas.


## **Como funciona a camada de acesso?


### A **camada de acesso** em redes é responsável por conectar os dispositivos finais (como computadores, smartphones, impressoras, etc.) à rede, gerenciar o tráfego local e garantir a segurança da comunicação. Vamos ver como ela funciona passo a passo:

### **Passo 1: Conexão do Dispositivo à Rede**

- **Com fio**: Dispositivos finais, como computadores, se conectam à rede por meio de cabos Ethernet a um **switch**.
- **Sem fio**: Dispositivos móveis ou laptops se conectam a **pontos de acesso (APs)** Wi-Fi.

### **Passo 2: Autenticação e Controle de Acesso**

#### **Quando um dispositivo tenta se conectar à rede:

1. **Autenticação de dispositivos**:
    - Para **redes com fio**, o switch pode usar o protocolo **802.1X** para autenticar o dispositivo antes de permitir o acesso.
    - Para **redes sem fio**, o ponto de acesso realiza a autenticação através de senhas ou outros protocolos de segurança como **WPA2/WPA3**.
2. **Verificação de credenciais**: A camada de acesso pode integrar-se a servidores **RADIUS** ou **LDAP** para verificar se as credenciais fornecidas pelo dispositivo estão corretas.

### **Passo 3: Atribuição de Recursos e Configuração**

#### **Depois que o dispositivo é autenticado:

1. **Atribuição de VLAN**: O switch ou ponto de acesso pode atribuir o dispositivo a uma **VLAN** específica, segmentando o tráfego. Por exemplo, um dispositivo de um funcionário pode ser colocado em uma VLAN diferente de um visitante.
2. **Atribuição de endereço IP**: O dispositivo pode obter um **endereço IP** automaticamente via **DHCP** (Protocolo de Configuração Dinâmica de Host), ou manualmente, se for configurado dessa forma.

### **Passo 4: Encaminhamento de Dados**

#### **Agora que o dispositivo está conectado e configurado:

1. **Comutação de pacotes**: O switch ou ponto de acesso faz a **comutação** (encaminhamento de pacotes) com base nos **endereços MAC** de origem e destino.
    
    - Para **comutação com fio**, o switch usa o endereço MAC de cada dispositivo para enviar pacotes para o destino correto dentro da LAN (rede local).
    - Para **comutação sem fio**, o ponto de acesso faz a tradução entre os pacotes Wi-Fi e Ethernet, encaminhando-os para os dispositivos dentro da rede.
2. **Tráfego dentro da rede**: Caso o tráfego seja enviado para outro dispositivo na mesma rede local, ele é processado diretamente na camada de acesso e não precisa sair para outras camadas.
    

### **Passo 5: Aplicação de Políticas de Segurança e QoS**

- **Listas de Controle de Acesso (ACLs)**: A camada de acesso pode definir **ACLs** para restringir o tráfego de dispositivos com base em IP, MAC ou VLAN.
- **Segurança adicional**: Pode bloquear ou permitir o acesso a determinados recursos da rede, controlando, por exemplo, se um dispositivo pode acessar a internet ou apenas uma rede interna.
- **Qualidade de Serviço (QoS)**: Se a rede precisar priorizar certos tipos de tráfego (como voz ou vídeo), a camada de acesso aplica **QoS** para garantir que esses pacotes recebam prioridade no encaminhamento.

### **Passo 6: Encaminhamento para Camadas Superiores**

1. Se o dispositivo precisar acessar recursos fora da sua LAN (por exemplo, servidores ou a internet), o tráfego será encaminhado da camada de acesso para a **camada de distribuição**.
2. A camada de distribuição, geralmente composta por **roteadores**, realiza o roteamento do tráfego para outras sub-redes ou à **camada de núcleo**, onde as conexões mais amplas (por exemplo, à internet) são gerenciadas.

### **Passo 7: Gerenciamento e Monitoramento**

#### **A camada de acesso também permite monitorar e gerenciar os dispositivos conectados:

- **Monitoramento de tráfego**: Ferramentas de gerenciamento de rede podem ser usadas para monitorar a atividade dos dispositivos e verificar se há tráfego não autorizado ou comportamentos anômalos.
- **Ajustes dinâmicos**: Com base no tráfego e nas necessidades da rede, a camada de acesso pode ajustar a largura de banda, a prioridade do tráfego ou até mesmo as configurações de segurança (como reforçar autenticações).