RCOMP 2019-2020 Project - Sprint 3 - Member 1180017 folder
===========================================
(This folder is to be created/edited by the team member 1180017 only)

Nota(*): as configuração são respectivas ao campus_Edificio_B.pkt, as configuyraçoes do caompus completo não foram exportadas
Nota2(*): Devido a um bug do pakcet Tracer, os telefones estão todos configurados porém não é possivel estabelecer as confiburações,
	para confirmar, basta verificar o configuration dump. 

### OSPF (Open Shortest Path First) dynamic routing ###

as static routing criadas no sprint anterior precisam ser excluídas. Para fazer isso, precisamos fazer o comando:
	no route [ip] [mask] [connection] - no router do edificio B.

Agora que as ststics routing foram excluídas, podemos criar a área ospf neste edifício.
O edifício A terá o ID do processo 1, o edifício B terá o ID 2, etc.
Portanto, este edifício terá id = 2 e sua área terá id 2 pelo mesmo motivo. Também será usada a área 0, que representa a infraestrutura de backbone.

Então, usamos os comandos:


	router ospf 2 
	network [ip backbone network] [wildcard] area 0 
	network [ip floor 0 network building B] [wildcard] area 2 
	network [ip floor 1 network building B] [wildcard] area 2 
	network [ip wifi network building B] [wildcard] area 2 
	network [ip server network building B] [wildcard] area 2
	network [ip voip network building B] [wildcard] area 2 
 
### HTTP (HyperTet Transfer Protocol) ###

Será adicionado a esta simulação um novo servidor e definido estaticamente seu ip. Em seguida, devemos configurar a página HTML para identificar o edifício em que este servidor HTTP está armazenado.

### DNS (Domain Name System) ###

O membro que tem o prédio A sob sua responsabilidade criará um nome de domínio DNS correspondente ao nome do repositório da equipe (rcomp-18-19-da-g2). Esse é o domínio de nível mais alto, portanto será usado como se fosse o domínio raiz do DNS.

Para o DNS, adicionamos o seguinte ao servidor:

| Type | Name | Address / Server Name |
| --- | --- | --- |
| NS | . | rcomp-18-19-db-g2 |
| A Record | rcomp-18-19-gb-g2 | 172.16.232.2 (IP of root server) |
| NS | building-b.rcomp-18-19-db-g2 | ns.building-b.rcomp-18-19-di-g2 |
| A Record | ns.building-b.rcomp-18-19-di-g2 | 172.16.226.66 (IP of DNS server of building b) |
| A Record | server1 | 172.16.226.67 (IP of HTTP server of building b) |
| CName | www | server1 |
| CName | web | server1 |

## NS (Name Server) records and glue records ##

O próprio registro NS: o nome do registro é o nome do domínio e os dados do registro são o nome DNS do servidor de nomes desse domínio.

O registro A para o registro NS: o nome do registro é o nome DNS do servidor de nomes e
os dados do registro são o endereço IPv4 do servidor de nomes.

## Other DNS records ##

Todos os servidores HTTP devem ser nomeados server1 (registro A); todos têm o mesmo nome porque pertencem a domínios DNS diferentes.

Dentro de cada domínio DNS, deve haver um alias www (CNAME) mapeado para o registro server1 A do mesmo domínio e outro alias, nomeado web, também mapeado para o registro server1 A do domínio.

Um alias adicional (CNAME), com nome dns e mapeado para o registro ns A do domínio, também deve
existir.

## DNS client's configuration (end-nodes) ##

Todos os nós finais em um edifício devem usar o servidor de nomes DNS local e, se suportado, ter o domínio DNS padrão definido como o domínio DNS local.

E adicione o servidor DNS para os pools floor0, floor1 e wifi criados no sprint anterior.

	ip dhcp pool (NOME POOL: vlans do edificio, menos a do dmz, será static)
	dns-server 10.167.202.35 (IP do server DNS do edificio B)
	domain-name building-b

### NAT (Network Address Translation ###

Nesta rede, o NAT estático será aplicado e não o dinâmico. Para que possamos usá-lo para redirecionar o tráfego.

Para criar NAT neste roteador, precisamos definir qual conexão representa a parte interna e a parte externa, neste caso a interface f0 / 0 representará a parte interna (comando "ip nat inside") e a interface1 / 0 representará a parte externa ( Comando "ip nat outside").
Para as configurações solicitadas nesta atribuição:

	ip nat inside source static tcp (IP SERVER DNS) 80 (IP ASSOCIADO A f0/1) 80
	ip nat inside source static tcp (IP SERVER DNS) 443 (IP ASSOCIADO A f0/1) 443
	ip nat inside source static tcp (IP SERVER HTTP) 53 (IP ASSOCIADO A f0/1) 53
	ip nat inside source static udp (IP SERVER HTTP) 53 (IP ASSOCIADO A f0/1) 53


## Port Numbers ##

* 53 - DNS
* 80 - HTTP
* 443 - HTTPS

### ACLs (Access Control Lists) ###

Antes de tudo, garantimos que não temos nenhuma lista de acesso configurada (100-105):
	no access-list 100

Para os firewalls, precisaremos de 6 listas de acesso: uma para andar0 (100), uma para andar1 (102), para wifi (103), para DMZ (104), VOIp (105) e uma para fora do prédio (101) )

## For the internal connection ##

Os seguintes comandos garantirão:
 * para bloquear falsificações internas;
 * permitir todos os pedidos de eco do ICMP e respostas de eco;
 * permita que todo o tráfego da DMZ, bloqueie todo o tráfego direcionado ao roteador, exceto o tráfego necessário para os recursos atuais funcionarem (regras estáticas DHCP, TFTP, ITS, OSPF, NAT);

Para as configurações solicitadas nesta atribuição relacionadas ao firewall, para as listas de acesso 100.102 e 104:

	access-list (ACCESS-LIST ID) permit ip (IP NETWORK FLOOR0/FLOOR1/WIFI) (WILDCARD) any
	access-list (ACCESS-LIST ID) permit tcp (IP NETWORK FLOOR0/FLOOR1/WIFI) (WILDCARD) host (IP SERVER HTTP EDIFICIO A) eq www
	access-list (ACCESS-LIST ID) permit tcp (IP NETWORK FLOOR0/FLOOR1/WIFI) (WILDCARD) host (IP SERVER HTTP EDIFICIO B) eq www
	access-list (ACCESS-LIST ID) permit tcp (IP NETWORK FLOOR0/FLOOR1/WIFI) (WILDCARD) host (IP SERVER HTTP EDIFICIO C) eq www
	access-list (ACCESS-LIST ID) permit tcp (IP NETWORK FLOOR0/FLOOR1/WIFI) (WILDCARD) host (IP SERVER HTTP EDIFICIO E) eq www
	access-list (ACCESS-LIST ID) deny tcp any (IP NETWORK SERVER EDIFICIO A) (WILDCARD) eq www
	access-list (ACCESS-LIST ID) deny tcp any (IP NETWORK SERVER EDIFICIO B) (WILDCARD) eq www
	access-list (ACCESS-LIST ID) deny tcp any (IP NETWORK SERVER EDIFICIO C) (WILDCARD) eq www
	access-list (ACCESS-LIST ID) deny tcp any (IP NETWORK SERVER EDIFICIO E) (WILDCARD) eq www
	access-list (ACCESS-LIST ID) permit tcp (IP NETWORK FLOOR0/FLOOR1/WIFI) (WILDCARD) any eq www
	access-list (ACCESS-LIST ID) permit udp (IP NETWORK FLOOR0/FLOOR1/WIFI) (WILDCARD) host (IP SERVER HTTP EDIFICIO A) eq domain
	access-list (ACCESS-LIST ID) permit udp (IP NETWORK FLOOR0/FLOOR1/WIFI) (WILDCARD) host (IP SERVER HTTP EDIFICIO B) eq domain
	access-list (ACCESS-LIST ID) permit udp (IP NETWORK FLOOR0/FLOOR1/WIFI) (WILDCARD) host (IP SERVER HTTP EDIFICIO C) eq domain
	access-list (ACCESS-LIST ID) permit udp (IP NETWORK FLOOR0/FLOOR1/WIFI) (WILDCARD) host (IP SERVER HTTP EDIFICIO E) eq domain
	access-list (ACCESS-LIST ID) deny icmp any (IP NETWORK SERVER EDIFICIO A) (WILDCARD) echo
	access-list (ACCESS-LIST ID) deny icmp any (IP NETWORK SERVER EDIFICIO B) (WILDCARD) echo
	access-list (ACCESS-LIST ID) deny icmp any (IP NETWORK SERVER EDIFICIO C) (WILDCARD) echo
	access-list (ACCESS-LIST ID) deny icmp any (IP NETWORK SERVER EDIFICIO E) (WILDCARD) echo
	access-list (ACCESS-LIST ID) permit icmp (IP NETWORK FLOOR0/FLOOR1/WIFI) (WILDCARD) any echo
	access-list (ACCESS-LIST ID) permit udp host 0.0.0.0 eq bootpc host 255.255.255.255 eq bootps
	access-list (ACCESS-LIST ID) deny ip any any

## For the external connection: ##

Os seguintes comandos garantirão:
  * Bloquear falsificação externa;
  * Permitir todos os pedidos de eco do ICMP e respostas de eco;
  * Bloqueie todo o tráfego para a DMZ
  * Bloqueie todo o tráfego direcionado ao roteador, exceto o tráfego necessário para os recursos atuais funcionarem (DHCP, TFTP, ITS, OSP)


 
    access-list 101 permit tcp any eq www (IP NETWORK F0) (WILDCARD) established
	access-list 101 permit tcp any eq www (IP NETWORK F1) (WILDCARD) established
	access-list 101 permit tcp any eq www (IP NETWORK WIFI) (WILDCARD) established
	access-list 101 permit tcp any eq www (IP NETWORK SERVERS) (WILDCARD) established
	access-list 101 deny ip (IP NETWORK F0) (WILDCARD) any
	access-list 101 deny ip (IP NETWORK F1) (WILDCARD) any
	access-list 101 deny ip (IP NETWORK SERVERS) (WILDCARD) any
	access-list 101 deny ip (IP NETWORK VOIP) (WILDCARD) any
	access-list 101 deny ip (IP NETWORK WIFI) (WILDCARD) any
	access-list 101 permit ip any any
	access-list 101 permit udp host (IP SERVER DNS BUILDING A) eq domain (IP NETWORK F0) (WILDCARD)
	access-list 101 permit udp host (IP SERVER DNS BUILDING A) eq domain (IP NETWORK F1) (WILDCARD)
	access-list 101 permit udp host (IP SERVER DNS BUILDING A) eq domain (IP NETWORK WIFI) (WILDCARD)
	access-list 101 permit udp host (IP SERVER DNS BUILDING A) eq domain (IP NETWORK SERVERS) (WILDCARD)
	access-list 101 permit udp host (IP SERVER DNS BUILDING B) eq domain (IP NETWORK F0) (WILDCARD)
	access-list 101 permit udp host (IP SERVER DNS BUILDING B) eq domain (IP NETWORK F1) (WILDCARD)
	access-list 101 permit udp host (IP SERVER DNS BUILDING B) eq domain (IP NETWORK WIFI) (WILDCARD)
	access-list 101 permit udp host (IP SERVER DNS BUILDING B) eq domain (IP NETWORK SERVERS) (WILDCARD)
	access-list 101 permit udp host (IP SERVER DNS BUILDING C) eq domain (IP NETWORK F0) (WILDCARD)
	access-list 101 permit udp host (IP SERVER DNS BUILDING C) eq domain (IP NETWORK F1) (WILDCARD)
	access-list 101 permit udp host (IP SERVER DNS BUILDING C) eq domain (IP NETWORK WIFI) (WILDCARD)
	access-list 101 permit udp host (IP SERVER DNS BUILDING C) eq domain (IP NETWORK SERVERS) (WILDCARD)
	access-list 101 permit udp host (IP SERVER DNS BUILDING E) eq domain (IP NETWORK F0) (WILDCARD)
	access-list 101 permit udp host (IP SERVER DNS BUILDING E) eq domain (IP NETWORK F1) (WILDCARD)
	access-list 101 permit udp host (IP SERVER DNS BUILDING E) eq domain (IP NETWORK WIFI) (WILDCARD)
	access-list 101 permit udp host (IP SERVER DNS BUILDING E) eq domain (IP NETWORK SERVERS) (WILDCARD)
	access-list 101 permit tcp any host (IP SERVER HTTP) eq www
	access-list 101 deny ip (IP NETWORK SERVER EDIFICIO A) (WILDCARD) any
	access-list 101 deny ip (IP NETWORK SERVER EDIFICIO B) (WILDCARD) any
	access-list 101 deny ip (IP NETWORK SERVER EDIFICIO C) (WILDCARD) any
	access-list 101 deny ip (IP NETWORK SERVER EDIFICIO E) (WILDCARD) any
	access-list 101 permit icmp any (IP NETWORK SERVER EDIFICIO A) (WILDCARD) echo-reply
	access-list 101 permit icmp any (IP NETWORK SERVER EDIFICIO B) (WILDCARD) echo-reply
	access-list 101 permit icmp any (IP NETWORK SERVER EDIFICIO C) (WILDCARD) echo-reply
	access-list 101 permit icmp any (IP NETWORK SERVER EDIFICIO E) (WILDCARD) echo-reply
	access-list 101 permit icmp any host (IP SERVER HTTP) echo


#### Tabela DNS ####

![tabela](/doc/sprint3/1180017/figuras_aux/tabela_DNS_B.PNG)
