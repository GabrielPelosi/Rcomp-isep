RCOMP 2019-2020 Project - Sprint 3 - Member 1180871 folder
===========================================

## Building C ##

### OSPF (Open Shortest Path First) dynamic routing ###

As routers estáticas criadas no sprint anterior foram excluídas.

Depois de excluídas, criamos a área ospf neste edifício. 
O edifício C terá o ID do processo 3 e sua área terá id 3. Também será usada a área 0, que representa a infraestrutura de backbone.

Então, usamos os comandos:

```
router ospf 3
network 10.167.200.129 0.0.0.63 area 3
network 10.167.199.129 0.0.0.63 area 3
network 10.167.198.65 0.0.0.63 area 3
network 10.167.193.1 0.0.0.255 area 3
network 10.167.199.193 0.0.0.63 area 3
network 10.167.196.1 0.0.0.255 area 0
```



### HTTP (HyperTet Transfer Protocol) ###

Adicionamos um servidor e definimos o seu ip. Depois, configuramos uma página html a identificar o edifício.

```html
<!DOCTYPE html>
<html>
<head>
<title>Page Title</title>
</head>
<body>

<h1>RCOMP</h1>
<p>Bem vindo ao Edificio C.</p>

</body>
</html>
```



### DNS (Domain Name System) ###

O membro que tem o edifício A tem como sua responsabilidade criar um nome de domínio DNS correspondente ao nome do repositório da equipa (rcomp-19-20-da-g2). Este é o domínio de nível mais alto, portanto será usado como se fosse o domínio raiz do DNS. Para cada edifício, foram criadas as tabelas de DNS com os DNS locais nomeadas da seguinte forma  building-x.rcomp-19-20-di-g2, sendo x a letra de cada edifício. No caso do C, building-c.rcomp-19-20-di-g2

Tabela DNS:

![tabela_DNS_C](/doc/sprint3/1180871/tabela_DNS_C.PNG)



## DNS client's configuration (end-nodes) ##

Configuração do DCHP:

	ip dhcp pool Piso0_C
	network 10.167.200.128 255.255.255.192
	default-router 10.167.200.129
	domain-name building-c.rcomp-19-20-di-g2
	dns-server 10.167.193.2
	exit
	ip dhcp excluded-address 10.167.200.129
	
	ip dhcp pool Piso1_C
	network 10.167.199.128 255.255.255.192
	default-router 10.167.199.129
	domain-name building-c.rcomp-19-20-di-g2
	dns-server 10.167.193.2
	exit
	ip dhcp excluded-address 10.167.199.129
	
	ip dhcp pool Wifi_C
	network 10.167.198.64 255.255.255.192
	default-router 10.167.198.65
	domain-name building-c.rcomp-19-20-di-g2
	dns-server 10.167.193.2
	exit
	ip dhcp excluded-address 10.167.198.65
	
	ip dhcp pool VOIP_C
	network 10.167.199.192 255.255.255.192
	default-router 10.167.199.193
	option 150 ip 10.167.199.193
	exit
	ip dhcp excluded-address 10.167.199.193

Depois fomos a cada porta de cada pc/laptop e mudamos de static para dhcp.



### VOIP phones

Para cada switch/interface (X) com telefones, a seguinte configuração foi feita: 

```
int interfaceX
switchport mode access
switchport voice vlan 465
no switchport access vlan
```

No router do edifício C, o seguinte foi feito para o número de telefones necessários (neste caso, 2*): 

```
telephony-service
auto-reg-ephone
ip source-address 10.167.199.193 port 2000
max-ephones 2
max-dn 2
auto assign 1 to 2
exit
ephone-dn 1
number 3000
ephone-dn 2
number 3001
```

*O número de telefones foi diminuido para este sprint com o objetivo de diminuir as falhas dos testes de configuração dos telefones que estavamos a ter.



### NAT (Network Address Translation ###

Para a configuração do NAT, fizemos o seguinte: 

	interface FastEthernet0/0.1
	ip nat inside 
	interface FastEthernet0/0.6
	ip nat outside
	no access-list 1
	access-list 1 permit 10.167.193.0 0.0.0.255 
	ip nat inside source list 1 interface FastEthernet0/0.1 overload 
	ip nat inside source static tcp 10.167.193.3 80 10.167.196.3 80
	
	interface FastEthernet0/0.1
	ip nat inside 
	interface FastEthernet0/0.6
	ip nat outside
	no access-list 1
	access-list 1 permit 10.167.193.0 0.0.0.255 
	ip nat inside source list 1 interface FastEthernet0/0.1 overload 
	ip nat inside source static tcp 10.167.193.3 443 10.167.196.3 443
	
	interface FastEthernet0/0.1
	ip nat inside 
	interface FastEthernet0/0.6
	ip nat outside
	no access-list 1
	access-list 1 permit 10.167.193.0 0.0.0.255 
	ip nat inside source list 1 interface FastEthernet0/0.1 overload 
	ip nat inside source static tcp 10.167.193.2 53 10.167.196.3 53
	
	interface FastEthernet0/0.2
	ip nat inside 
	interface FastEthernet0/0.6
	ip nat outside
	no access-list 2
	access-list 2 permit 10.167.193.0 0.0.0.255 
	ip nat inside source list 2 interface FastEthernet0/0.2 overload 
	ip nat inside source static tcp 10.167.193.3 80 10.167.196.3 80
	
	interface FastEthernet0/0.2
	ip nat inside 
	interface FastEthernet0/0.6
	ip nat outside
	no access-list 2
	access-list 2 permit 10.167.193.0 0.0.0.255 
	ip nat inside source list 2 interface FastEthernet0/0.2 overload 
	ip nat inside source static tcp 10.167.193.3 443 10.167.196.3 443
	
	interface FastEthernet0/0.2
	ip nat inside 
	interface FastEthernet0/0.6
	ip nat outside
	no access-list 2
	access-list 2 permit 10.167.193.0 0.0.0.255 
	ip nat inside source list 2 interface FastEthernet0/0.2 overload 
	ip nat inside source static tcp 10.167.193.2 53 10.167.196.3 53
	
	interface FastEthernet0/0.3
	ip nat inside 
	interface FastEthernet0/0.6
	ip nat outside
	no access-list 3
	access-list 3 permit 10.167.193.0 0.0.0.255 
	ip nat inside source list 3 interface FastEthernet0/0.3 overload 
	ip nat inside source static tcp 10.167.193.3 80 10.167.196.3 80
	
	interface FastEthernet0/0.3
	ip nat inside 
	interface FastEthernet0/0.6
	ip nat outside
	no access-list 3
	access-list 3 permit 10.167.193.0 0.0.0.255 
	ip nat inside source list 3 interface FastEthernet0/0.3 overload 
	ip nat inside source static tcp 10.167.193.3 443 10.167.196.3 443
	
	interface FastEthernet0/0.3
	ip nat inside 
	interface FastEthernet0/0.6
	ip nat outside
	no access-list 3
	access-list 3 permit 10.167.193.0 0.0.0.255 
	ip nat inside source list 3 interface FastEthernet0/0.3 overload 
	ip nat inside source static tcp 10.167.193.2 53 10.167.196.3 53
	
	interface FastEthernet0/0.4
	ip nat inside 
	interface FastEthernet0/0.6
	ip nat outside
	no access-list 4
	access-list 4 permit 10.167.193.0 0.0.0.255 
	ip nat inside source list 4 interface FastEthernet0/0.4 overload 
	ip nat inside source static tcp 10.167.193.3 80 10.167.196.3 80
	
	interface FastEthernet0/0.4
	ip nat inside 
	interface FastEthernet0/0.6
	ip nat outside
	no access-list 4
	access-list 4 permit 10.167.193.0 0.0.0.255 
	ip nat inside source list 4 interface FastEthernet0/0.4 overload 
	ip nat inside source static tcp 10.167.193.3 443 10.167.196.3 443
	
	interface FastEthernet0/0.4
	ip nat inside 
	interface FastEthernet0/0.6
	ip nat outside
	no access-list 4
	access-list 4 permit 10.167.193.0 0.0.0.255 
	ip nat inside source list 4 interface FastEthernet0/0.4 overload 
	ip nat inside source static tcp 10.167.193.2 53 10.167.196.3 53
	
	interface FastEthernet0/0.5
	ip nat inside 
	interface FastEthernet0/0.6
	ip nat outside
	no access-list 5
	access-list 5 permit 10.167.193.0 0.0.0.255 
	ip nat inside source list 5 interface FastEthernet0/0.5 overload 
	ip nat inside source static tcp 10.167.193.3 80 10.167.196.3 80
	
	interface FastEthernet0/0.5
	ip nat inside 
	interface FastEthernet0/0.6
	ip nat outside
	no access-list 5
	access-list 5 permit 10.167.193.0 0.0.0.255 
	ip nat inside source list 5 interface FastEthernet0/0.5 overload 
	ip nat inside source static tcp 10.167.193.3 443 10.167.196.3 443
	
	interface FastEthernet0/0.5
	ip nat inside 
	interface FastEthernet0/0.6
	ip nat outside
	no access-list 5
	access-list 5 permit 10.167.193.0 0.0.0.255 
	ip nat inside source list 5 interface FastEthernet0/0.5 overload 
	ip nat inside source static tcp 10.167.193.2 53 10.167.196.3 53

##### Port Numbers #####

* 53 - DNS
* 80 - HTTP
* 443 - HTTPS



### ACLs (Access Control Lists) ###

Os comandos de Access Control List não foram postos em prática, uma vez que criaram conflitos que bloquearam algumas das funcionalidades configuradas anterioramente.
