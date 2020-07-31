RCOMP 2019-2020 Project - Sprint 3 - Member 1181053 folder
===========================================

## Building D ##

### OSPF (Open Shortest Path First) dynamic routing ###

As routes estáticas criadas no sprint anterior precisam de ser excluídas.

Depois de excluídos, podemos criar a área ospf neste edifício.
O edifício A terá o ID do processo 1, o edifício B terá o ID 2, etc.
Portanto, este edifício terá id = 4 e sua área terá id 4 pelo mesmo motivo. Também será usada a área 0, que representa a infraestrutura de backbone.

Então, usamos os comandos:

```
router ospf 4
network 10.167.200.193 0.0.0.63 area 4
network 10.167.199.1 0.0.0.63 area 4
network 10.167.198.129 0.0.0.63 area 4
network 10.167.194.1 0.0.0.255 area 4
network 10.167.201.193 0.0.0.31 area 4
network 10.167.196.1 0.0.0.255 area 0
```



### HTTP (HyperTet Transfer Protocol) ###

Nesta simulação, é adicionado um novo server e o seu IP é definido estaticamente. A página HTML é configurada para identificar o edifício onde este HTTP está armazenado.



### DNS (Domain Name System) ###

Tabela DNS:

![image-20200517182837084](C:\Users\João Magalhães\Documents\rcomp-19-20-di-g2\doc\sprint3\1181053\Tabela_DNS_D)

## DNS client's configuration (end-nodes) ##

Todos os computadores e laptops são configurados de Static Adresssing para DHCP.

Configuração do DCHP

	ip dhcp pool Piso0_D
	network 10.167.200.192 255.255.255.192
	default-router 10.167.200.193
	domain-name building-d.rcomp-19-20-di-g2
	dns-server 10.167.194.2
	exit
	ip dhcp excluded-address 10.167.200.193
	
	ip dhcp pool Piso1_D
	network 10.167.199.0 255.255.255.192
	default-router 10.167.199.1
	domain-name building-d.rcomp-19-20-di-g2
	dns-server 10.167.194.2
	exit
	ip dhcp excluded-address 10.167.199.1
	
	ip dhcp pool Wifi_D
	network 10.167.198.128 255.255.255.192
	default-router 10.167.198.129
	domain-name building-d.rcomp-19-20-di-g2
	dns-server 10.167.194.2
	exit
	ip dhcp excluded-address 10.167.198.129
	
	ip dhcp pool VOIP_D
	network 10.167.201.192 255.255.255.224
	default-router 10.167.201.193
	option 150 ip 10.167.201.193
	exit
	ip dhcp excluded-address 10.167.201.193



### VOIP phones

Para cada switch/interface (X) com phones, a seguinte configuração será feita: 

```
int interfaceX
switchport mode access
switchport voice vlan 480
no switchport access vlan
```

No router do edifício de nivel mais alto (IC no edifício D), o seguinte será feito para o número de telemóveis necessários (neste caso, 5): 

```
telephony-service
auto-reg-ephone
ip source-address 10.167.201.193 port 2000
max-ephones 5
max-dn 5
auto assign 1 to 5
exit
ephone-dn 1
number 4000
ephone-dn 2
number 4001
ephone-dn 3
number 4002
ephone-dn 4
number 4003
ephone-dn 5
number 4004
```



### NAT (Network Address Translation ###

Para a configuração do NAT, fizemos o seguinte: 

	interface FastEthernet0/0.1 (para cada FastEthernet do router sem o backbone)
	ip nat inside
	interface FastEthernet0/0.6 (router para backbone)
	ip nat outside
	no access-list 5
	access-list 5 permit ip-rede-servers wild-mask-ip-rede-servers
	ip nat inside source list 5 interface FastEthernet0/0.1 (a mesma que em cima) overload
	ip nat inside source static tcp ip-server-http 80 ip-router-backbone 80
	
	interface FastEthernet0/0.1 (para cada FastEthernet do router sem o backbone)
	ip nat inside
	interface FastEthernet0/0.6 (router para backbone)
	ip nat outside
	no access-list 5
	access-list 5 permit ip-rede-servers wild-mask-ip-rede-servers
	ip nat inside source list 5 interface FastEthernet0/0.1 (a mesma que em cima) overload
	ip nat inside source static tcp ip-server-http 443 ip-router-backbone 443
	
	interface FastEthernet0/0.1 (para cada FastEthernet do router sem o backbone)
	ip nat inside
	interface FastEthernet0/0.6 (router para backbone)
	ip nat outside
	no access-list 5
	access-list 5 permit ip-rede-servers wild-mask-ip-rede-servers
	ip nat inside source list 5 interface FastEthernet0/0.1 (a mesma que em cima) overload
	ip nat inside source static tcp ip-server-dns 53 ip-router-backbone 53

##### Port Numbers #####

* 53 - DNS
* 80 - HTTP
* 443 - HTTPS





### ACLs (Access Control Lists) ###

Antes de tudo, garantimos que não temos nenhuma lista de acesso configurada (100-105):
sem lista de acesso 100.

Para os firewalls, precisaremos de 6 listas de acesso: uma para o andar0 (100), uma para o andar1 (101), para o wifi (102), para o DMZ (105), VOIp (103) e uma para fora do prédio (104) ).

## For the internal connection ##

Os comandos seguintes vão garantir:

 * bloqueio do Internal Spoofing;
 * permitir todos os ICMP echo requests e echo replies;
 * permitir todo o trafico do DMZ, bloquear todo o tráfego direcionado ao router, exceto o tráfego necessário para os recursos atuais funcionarem (regras estáticas DHCP, TFTP, ITS, OSPF, NAT);

Para as configurações pedidas, o seguinte foi feito:

	FLOOR0:
		- access-list 100 permit ip host 0.0.0.0 host 255.255.255.255					
		- access-list 100 permit ip 10.166.213.0 0.0.0.63 any
						//network FLOOR0 e wildcard
	
	FLOOR1:
		- access-list 101 permit ip host 0.0.0.0 host 255.255.255.255
		- access-list 101 permit ip 10.166.212.128 0.0.0.127 any
					//network FLOOR1 e wildcard
	
	WIFI:
		- access-list 102 permit ip host 0.0.0.0 host 255.255.255.255
		- access-list 102 permit ip 10.166.212.0 0.0.0.127 any
						//network WIFI e wildcard
	
	DMZ:
		- access-list 105 deny ip 10.166.213.128 0.0.0.15 any
					//network WIFI e wildcard
		- access-list 105 permit udp any host 10.166.213.129 eq 53
		- access-list 105 permit tcp any host 10.166.213.129 eq 53
						//IP Servidor DNS
		- access-list 105 permit tcp any host 10.166.213.131 eq 80
		- access-list 105 permit tcp any host 10.166.213.131 eq 443
						//IP Servidor HTTP
	
	VOIP:
		- access-list 103 permit ip host 0.0.0.0 host 255.255.255.255
		- access-list 103 permit udp 10.166.213.64 0.0.0.63 host 10.166.216.3 eq 69
		- access-list 103 permit tcp 10.166.213.64 0.0.0.63 host 10.166.216.3 eq 2000
					//network WIFI e wildcard      //ip da interface BACKBONE do router
		- access-list 103 permit ip 10.166.213.64 0.0.0.63 any

## For the external connection: ##

The following commands will ensure:

 * bloqueio do Internal Spoofing;
 * permitir todos os ICMP echo requests e echo replies;
 * bloquear todo o trafico do DMZ;
 * bloquear todo o tráfego direcionado ao router, exceto o tráfego necessário para os recursos atuais funcionarem (regras estáticas DHCP, TFTP, ITS, OSPF, NAT);

For the access-list 104, which represents the outside:

    BACKBONE:
    	- access-list 104 deny ip 10.166.212.0 0.0.1.255 any
    				 //network do edificio inteiro e wildcard	
    	- access-list 104 permit ospf any host 10.166.216.3
    	- access-list 104 permit udp any host 10.166.216.3 eq 53
    	- access-list 104 permit tcp any host 10.166.216.3 eq 53
    	- access-list 104 permit tcp any host 10.166.216.3 eq 80
    	- access-list 104 permit tcp any host 10.166.216.3 eq 443
    	- access-list 104 permit tcp any host 10.166.216.3 eq 2000
    	- access-list 104 deny ip any host 10.166.216.3
    					 //ip da interface BACKBONE do router
    	- access-list 104 permit ip any any

Para agrupar as access-lists fizemos no final o seguinte: 

```
interface FastEthernet0/0.1 (	CORRESPONDE AO MEU FLOOR0)
 ip access-group 100 in
!
interface FastEthernet0/0.2 (	CORRESPONDE AO MEU FLOOR1)
 ip access-group 101 in
!
interface FastEthernet0/0.3 (	CORRESPONDE AO MEU WIFI)
 ip access-group 102 in
!
interface FastEthernet0/0.4	(CORRESPONDE AO MEU DMZ)
 ip access-group 105 out
!
interface FastEthernet0/0.5	(CORRESPONDE AO MEU VOIP)
 ip access-group 103 in
!
interface FastEthernet0/0.6	(CORRESPONDE AO MEU BACKBONE)
 ip access-group 104 in
```

