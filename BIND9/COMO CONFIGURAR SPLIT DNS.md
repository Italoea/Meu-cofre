
## O SPLIT DNS SERVER PARA FAZER A DIVISÃO DE DNS.

![[Pasted image 20250702105721.png]]

### QUANDO O WIN-CLI FIZER UMA PESUISA NO SERVIDOR DNS ELE IRÁ PESQUISAR NO 192.168.17.130

### QUANDO O CLIENT7 FIZER UMA PESQUISA NO SERVIDOR DNS ELE IRÁ PESQUISAR NA PORTA PUBLICAR QUE CONFIGUREI NO CASO É A 210.103.5.1

#### CONFIGURAÇÃO PARA OS HOSTS EXTERNOS

![[Pasted image 20250702110015.png]]



#### CONFIGURAÇÃO PARA OS HOSTS INTERNOS:

![[Pasted image 20250702110111.png]]


#### CONFIGURAÇÃO DE VIEWS 

![[Pasted image 20250702110248.png]]

##### 1 NESSA CONFIGURAÇÃO CRIEI A ACL INTERNO MOSTRANDO MINHA REDE LOCAL AONDE ESTÁ MEU SERVIDOR DNS, E LOGO EM SEGUIDA COLOQUEI O ANY PARA FAZER A REFERENCIA DE TODO O RESTO.

##### 2 DEPOIS DECLAREI MINHA VIEW INTERNA E LÁ COLOQUEI O MATCH-CLIENTS COM MINHA ACL INTERNO, APÓS ISSO DECLAREI MINHA ZONA NORMALMENTE COMO SEMPRE DECLARO.

##### 3 AGORA ADICONEI TODAS AS ZONAS DEFAULTS NA MINHA VIEW INTERNO POIS SE EU NÃO FIZER ISSO VAI DAR ERRO NA CONFIURAÇÃO

##### 4 CONFIGUREI DA MESMA FORMA MINHA VIEW EXTERNO

![[Pasted image 20250702110724.png]]
## LEMBRANDO QUE ELA ESTÁ FORA DA VIEW INTERNO






```
// named.conf

acl "interna" {
    192.168.0.0/24;
    10.0.0.0/8;
    localhost;
};

acl "externa" {
    any;
};

view "internal" {
    match-clients { "interna"; };
    recursion yes;

    zone "exemplo.com" {
        type master;
        file "/etc/bind/db.exemplo.com.interna";
    };

    zone "0.168.192.in-addr.arpa" {
        type master;
        file "/etc/bind/db.192.168.0";
    };
};

view "external" {
    match-clients { "externa"; };
    recursion no;

    zone "exemplo.com" {
        type master;
        file "/etc/bind/db.exemplo.com.externa";
    };
};

```


