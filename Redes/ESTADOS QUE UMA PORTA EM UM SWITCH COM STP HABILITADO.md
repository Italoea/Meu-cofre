### **Blocking** -- Uma porta que causaria um loop caso estivesse ativa. Ela não recebe nem envia dados de usuário neste estado, mas continua recebendo BPDU's e pode ser transformar em uma porta que faz encaminhamento caso a situação da rede se altere e seja necessário. 


### **Listening** -- O switch verifica os BPDU's e verifica se ele não deve ficar bloqueado, neste caso ele não ajuda a construir a tabela MAC nem encaminha quadros.

### **Learning** -- Neste estado a porta ainda não encaminha os quadros, mas "aprende" endereços MAC dos quadros que passam por ela e ajuda a contribuir a tabela MAC.

### **Forwading** -- Uma porta funcionando normalmente ou seja, recebendo e encaminhando quadros, mesmo assim, continua monitorando BPDU's para saber se em algum momento não deve entrar em estado bloqueado.

### **Disabled** -- Uma porta desabilitada, pode ser feito pelo administrador da rede manualmente.