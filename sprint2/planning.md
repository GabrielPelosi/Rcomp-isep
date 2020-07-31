RCOMP 2019-2020 Project - SprRCOMP 2019-2020 Project - Sprint 2 planning
===========================================
### Sprint master: 1180017 ###
(This file is to be created/edited by the sprint master only)
# 1. Sprint's backlog #
Neste sprint, o grupo será destinado a criar uma simulacao da rede estruturada nos edificios anteriormente no sprint 1 com o auxilio
do Packet Tracer.
Nesta fase do projecto o foco será a configuracao da segunda e da terceira camada (enderecamento de IPs e static routing).
# 2. Technical decisions and coordination #
In this section, all technical decisions taken in the planning meeting should be mentioned.     Most importantly, all technical decisions impacting on the subtasks implementation must be settled on this    meeting and specified here.

  * Definir e configurar as VLANs dos edificios
  * Definir e atribuir os IPs
  * Routers e static routing
  * Realizar a conexão com a internet



# 3. Subtasks assignment #

A divisão das tarefas neste sprint tem como base na divisão feita no sprint anterior, ou seja, cada elemento deste grupo desenvolverá as respectivas camadas(2 e 3) dos edificios que cabearam no sprint passado.
 
  * 1181056(*) - Desenvolver uma simulacao das camadas dois e tres do edificio A.
  * 1180017 - Desenvolver a simulacao da rede das camdas dois e tres no edificio B.
  * 1180871 - Desenvolver a simulacao da rede das camdas dois e tres no edificio C.
  * 1181053 - Desenvolver a simulacao da rede das camdas dois e tres no edificio D.
  * 1170894 -  Desenvolver a simulacao da rede das camdas dois e tres no edificio E.

(*) O encarregado da primeira tarefa devera também integrar todos os projetos ao fim do do desenvolvimento do trabalho pratico.
  Nota: Para evitar conflitos do desenvolvimento do projecto, adotamos uma especifica nomeclatura para os equipamentos representados no packet tracer.

  
# 5. Padrão de nomes para equipamentos do projeto #
  * tipoAparelho_Edificio_Andar_numero
  * Exemplo: switch_A_0_002
  
# 6. Tabela com as Vlans e suas designações #
  ![tablea](/doc/sprint2/figura_aux/Tabelas_Todos_Edifícios.PNG)
  
# 7. Tabela com os IPS das VLNAS criadas #
  ![tabela](/doc/sprint2/figura_aux/Tabela_IPs_VLAN.PNG)

# 8. Table com as Routing tables de todos os edificio #

>#### 8.1 Tables do Edificio A 

  ![tabela](/doc/sprint2/figura_aux/Routing_Tables/Routing_Table_A_parte1.PNG)

  ![tabela](/doc/sprint2/figura_aux/Routing_Tables/Routing_Table_A_parte2.PNG)

  ![tabela](/doc/sprint2/figura_aux/Routing_Tables/Routing_Table_A_parte3.PNG)

  ![tabela](/doc/sprint2/figura_aux/Routing_Tables/Routing_Table_A_parte4.PNG)

  ![tabela](/doc/sprint2/figura_aux/Routing_Tables/Routing_Table_A_parte5.PNG)


>#### 8.2 Tabelas do Edificio B 

  ![tabela](/doc/sprint2/figura_aux/Routing_Tables/Routing_Table_B.PNG)

>#### 8.3 Tabelas do Edificio C 

  ![tabela](/doc/sprint2/figura_aux/Routing_Tables/Routing_Table_C.PNG)

>####  8.3 Tabelas do Edificio D #

  ![tabela](/doc/sprint2/figura_aux/Routing_Tables/Routing_Table_D.PNG)

>#### 8.4 Tabelas do Edificio E #

  ![tabela](/doc/sprint2/figura_aux/Routing_Tables/Routing_Table_E.PNG)



# Atribuicão das VLANIDs, VTP Domains, IPv4 addresses e ISP routers IPv4 address 

![tabela](/doc/sprint2/figura_aux/tabela.png)

# Nota sobre Laptops no Packet Tracer #
  * Devido a um bug da plataforma Cisco Packet Tracer, só será necessário realizar a configuração completa dos Laptops no proximo sprint, pois ao fechar o programa os ips e as conexões e as configurações 
    são perdidas.
    