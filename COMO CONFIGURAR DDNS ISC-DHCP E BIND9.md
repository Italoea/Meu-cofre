

![[Pasted image 20250702164338.png]]


## NO SERVIDOR DHCP-DNS CONFIGUREI:

![[Pasted image 20250702164506.png]]


## APONTEI O IP DO MEU SERVIDOR DNS

![[Pasted image 20250702164525.png]]


## NO NAMED.CONF.DEFAULT-ZONES:

![[Pasted image 20250702164859.png]]

#### ESSE allow-update para apontar aonde está o meu servidor dhcp.


# APÓS ISSO MOVA  O ARQUIVO DB PARA /VAR/LIB/BIND PARA CONSEGUIR CRIAR UM ARQUIVO JNL


 **EXEMPLO:**

/etc/dhcp/dhcpd.conf

```
authoritative;
ddns-update-style interim;
ddns-updates on;
ddns-domainname "gelosa.eu";
ddns-rev-domainname "0.168.192.in-addr.arpa.";
update-optimization off;
default-lease-time 600;
max-lease-time 7200;

subnet 192.168.0.0 netmask 255.255.255.0 {
        range 192.168.0.100 192.168.0.199;
        option subnet-mask 255.255.255.0;
        option routers 192.168.0.1;
        option domain-name-servers 192.168.0.31;
        option domain-name "gelosa.eu";
}

zone gelosa.eu. {
    primary 192.168.0.31;
}

zone 0.168.192.in-addr.arpa. {
    primary 192.168.0.31;
}

```

**Bind9**

**/var/lib/bind/db.zones

```

zone "gelosa.eu" {
    type master;
    file "db.gelosa.eu";
    allow-update { 192.168.0.31; };
};

zone "0.168.192.in-addr.arpa" {
    type master;
    file "db.192";
    allow-update { 192.168.0.31; };
};

```
