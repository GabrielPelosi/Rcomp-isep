
RCOMP 2019-2020 Project - Sprint 1 - Member 1180017 folder
===========================================
# Edifício B #

A estrutura do Edifício B (envolvendo os seus dois andares B0 e B1) está presente nas seguintes figura, contendo também as respetivas medidas de cada sala:

![B_medidas_Terreo](/doc/sprint1/1180017/Figuras_aux/B_medidas_Terreo.png)

![B_medidas_1](/doc/sprint1/1180017/Figuras_aux/B_medidas_1.png)



### Áreas ###
**Andar B0:**

Mesa B-> 4 tomadas

Área B0.2 = +-106,25 m² 21 tomadas

Área B0.3 = +-126,35 m², 27 tomadas

Área B0.4 = +- 180 m², 38 tomadas


**Andar B1:**

Área B1.1 = 13,5m², 5 tomadas

Área B1.2-1.8 = 52,5m², 11 ou 12 tomadas

Área  B1.8 = 87,775m², 19 tomadas

Área  B1.10,1.11 =57,75m², 12 tomadas

## Representação do raio de propagação do wifi

Foi escolhido dois routers para realizar a cobertura de wifi pois o diametro ed cobertura de um router são de 50 metros, o comprimento do piso é de 60 metros, ao posicionar um router exatamente no meio sobrariam
10 metros sem cobertura, 5 de cada lado do piso, portanto, foi decidido posicionar 2 router em casa piso.

![B_terreo_wifi](/doc/sprint1/1180017/Figuras_aux/B_terreo_wifi.PNG)

![B_1_wifi](/doc/sprint1/1180017/Figuras_aux/B_1_wifi.PNG)

## Representação dos andares e seus equipamentos de rede

![B_projeto_terreo](/doc/sprint1/1180017/Figuras_aux/B_projeto_terreo.PNG)

![B_projeto_1](/doc/sprint1/1180017/Figuras_aux/B_projeto_1.PNG)

Foram adotados Pontos de Consolidação(CP) para suportar o elevado número de tomadas de rede dos andares e em possivelemnte todos os caso foram necessários dois switches com 24 portas cada
para não só suportar o cabeamento mas sim, pode ser adaptar com futuras atualizações, vide que sobrará portas disponíveis em certas conexões cruzadas.

Nota: no primeiro piso(B1), foi adicionado mais um CP, isso porque poderia acontecer de cabos de cobres teram mais de 90 metros, o que não é permitido, logo, uma solução pensada
foi posicionar mais um CP neste piso.

## Tipo de cabos utilizados e os caminhos por eles percorridos
Neste edificio foi adotado fios de cobre do tipo CAT6 para cobertura de cabos(desde que sejam inferiores a 90 metros).

## Metros de cabos necessários
**Foi verificado que nenhum cabo há mais de 90 m de comprmento**
# B0
**Cabos de fora para o IC(em laranja):** 15m

**Cabos do IC(em verde):** 22,5m(utilizar dois em para realizar a redundancia)

**Cabos do HC(em preto):** 41,5m

**Cabos para os router(pontilhados):** 1ª router: 5m; 2ª router: 20m
**Cabos do CP(em azul):**  13,5

**Cabos para tomadas(em vermelho):** 130m(total)

# B1
**Cabos que vem do IC:** 1m (utilizar dois em para realizar a redundancia)

**Cabos do HC(tanto para tomadas quanto para os cps(em azul)):** 97m(total)

**Cabos dos 2 CP para tomadas(em vermelho):** 150m(total)

**Cabos para os router:** 1ª router: 15m; 2ª router: 20m

**Total:** (294m do B0)+(284m do B1) = 578 m(contando coma redundancia)

## Inventário
# B0

**Total de tomadas:** 86

**routers:** 2, cada um com um PoE

**Para o IC:** 1 switch de 8 entradas, para conetar os HCs e o MC, sobrando duas entradas e 1 patch panel do tipo CAT6 para o swtich com 8 entradas.

**Para o HC:** 2 swtiches de 24 entradas cada para conectar os routers e as tomadas de rede e 1 patch panel do tipo CAT6 com 48 portas.

**Para o CP** 2 swtiches de 24 entradas cada para conectar os routers e as tomadas de rede e 1 patch panel do tipo CAT6 com 48 portas.

**3 Telecomuniation Enclousers:** dois de tamanho 8U, para o HC e o CP e um de tamanh 6U para o IC


# B1

**Total de tomadas:** 124

**routers:** 2, cada um com um PoE

**Para o HC:**  2 swtiches de 24 entradas cada para conectar os routers e as tomadas de rede e 1 patch panel do tipo CAT6 com 48 portas.

**Para o CP**  2 swtiches de 24 entradas cada para conectar os routers e as tomadas de rede e 1 patch panel do tipo CAT6 com 48 portas.

**Para o segundo CP**  2 swtiches de 24 entradas cada para conectar os routers e as tomadas de rede e 1 patch panel do tipo CAT6 com 48 portas.

**3 Telecomuniation Enclousers:** todos de tamanho 8U para suportar o HC e os CPs

Nota: Foram adotados Telecomunication Enclousers de tamanho 8U pois o total de equipamentos somam 4U de tamanha, e recomeda-se que os Telecomuniation Enclousers tenha 100% a mais do tamanho 
de seus equipamentos, o mesmo para o IC de tamanho 6U.

2 Nota: Todos os telecomunications enclousers devem estar a um metro e meio do chão.


