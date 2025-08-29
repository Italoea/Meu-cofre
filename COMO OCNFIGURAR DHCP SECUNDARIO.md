

## NO HA-01 PRIMARIO

```
authoriritative;
ddns-style interim;
ddns updates on;
ddns-domainname "worldskills.cn";
ddns-rev-domainname "in-addr.arpa";

failover peer "dhcp-failover" {
	primary;
	address 172.16.10.1;
	port 519;
	peer address 172.16.10.2;
	peer port 520;
	split 128;
	mclt 3600;
	}
subnet 172.16.10.0 netmask 255.255.255.0 {
	pool {
	range 172.16.10.80 172.16.10.150;
	option routers 172.16.10.254;
	option domain-name "worldskills.cn";
	option domain-name-servers 172.16.10.1, 172.16.10.2;


	}
}

zone worldskills.cn {
	primary 172.16.10.1;
	key "skill39";
}

zone "16.172.in-addr.arpa" {
	primary 172.16.10.1;
	key "skill39";
	}
```

## HA-02 SECUNDARIO



```
authoritative;

feilover peer "dhcp-failover" {
	secondary;
	address 172.16.10.2;
	port 520;
	peer address 172.16.10.1;
	peer port 519;
	}

sunbnet 172.16.10.0 netmask 255.255.255.0 {
	pool {
	failover peer "dhcp-failover";
	range 172.16.10.80 172.16.10.150;
	option routers 172.16.10.254;
	option domain-name "worldskills.cn";
	option domain-name-servers 172.16.10.1, 172.16.10.2;
	
	}

}

```
