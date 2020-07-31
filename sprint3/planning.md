RCOMP 2019-2020 Project - Sprint 3 planning
===========================================
### Sprint master: 1180017 ###
(This file is to be created/edited by the sprint master only)
# 1. Sprint's backlog #
Neste ultimo sprint, o grupo terá como objetivo continuar a simulação da rede privada iniciada no sprint 2 através da aplicação Packet Tracer seguindo as sub-tasks especificadas a seguir.
# 2. Technical decisions and coordination #
In this section, all technical decisions taken in the planning meeting should be mentioned. Most importantly, all technical decisions impacting on the subtasks implementation must be settled on this 	meeting and specified here.

#### Sub-Tasks: ####

  * DHCPv4 service
  * VoIP service
  * Adding a second server to each DMZ network to run the HTTP service.
  * Configuring DNS servers to establish a DNS domains tree.
  * Enforcing NAT (Network Address Translation).
  * Establishing traffic access policies (static firewall) on routers.


#### Tasks: ####
  A divisão das tarefas neste sprint tem como base na divisão feita no sprint anterior, ou seja, cada elemento deste grupo desenvolverá as respectivas camadas(2 e 3) dos edificios que cabearam no sprint 1.
 
  * 1181056 - Continuar a desenvolver a simulacao das camadas dois e tres do edificio A.
  * 1180017(*) - Continuar a desenvolver a simulacao das camadas dois e tres no edificio B.
  * 1180871 - Continuar a desenvolver a simulacao das camadas dois e tres no edificio C.
  * 1181053 - Continuar a desenvolver a simulacao das camadas dois e tres no edificio D.
  * 1170894 -  Continuar a desenvolver a simulacao das camadas dois e tres no edificio E.

  (*) O encarregado do edifício B devera também integrar todos os projetos ao fim do do desenvolvimento do trabalho pratico.

  Nota: Para evitar conflitos do desenvolvimento do projecto, adotamos uma especifica nomeclatura no sprint passado para os equipamentos representados no packet tracer e iremos continuar com esse padrão.
  
  Nota 2: Cada elemento do grupo deve continuar o desenvolvimento da simulação respeitando cada sub-task identificada.

### Ids para as areas (OSFP) ###
  ![tabela_id](/doc/sprint3/figura_aux/id_areas.png)


# Tabelas das Wild Card masks #

#### Tabela para os calculos ####
  ![tabela_id](/doc/sprint3/figura_aux/tabela_para_calculos_wildcard.png)
#### Tabela para Wild Cards masks ####
  ![tabela_id](/doc/sprint3/figura_aux/wildCards.png)

# DNS domains #

  ![tabela_dns](/doc/sprint3/figura_aux/dns_domain.png)

# Números dos Telefones
  ![tabela_dns](/doc/sprint3/figura_aux/telefone_numbers.PNG)
  
# Portas para configurar o NAT 
  * As portas usadas para realizar a configuração do NAT (Network Address Translation) são: 80,443 e 50.
