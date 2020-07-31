RCOMP 2019-2020 Project - Sprint 1 - Member 1181056 folder
===========================================

# Campus backbone #
A estrutura do campus (envolvendo todos os edifícios) está presente na seguinte figura, contendo também as respetivas medidas das valas técnicas (Technical Ditch):

![CampusMedidas](/doc/sprint1/1181056/Figuras_aux/CampusMedidas.png)

**Legenda: Figura representativa das diferentes medidas necessárias do campus**

De acordo com a figura e o enunciado, não existem quaisquer restrições ou especificidades relativamente à estrutura de cabelagem e equipamento entre os respetivos edifícios. Desta forma, as decisões tomadas serão seguindo o critério de maior eficiência e as regras do planeamento de cabelagem.
Como se trata da totalidade do campus, as únicas análises necessárias de efetuar serão relativas à localização dos cross-connects e do tipo de cabos a utilizar nas ligações entre os mesmos (estes mesmos cabos estarão compreendidos nas valas técnicas).

## Localização dos cross-connects
**Main cross-connect (MC), Distributor C (DC) or Campus Distributor (CD)**: encontrar-se-á no edifício A como é referido no enunciado (pedido do cliente).

**Intermediate cross-connect (IC), Distributor B (DB) or Building Distributor (BD)**: um em cada edifício, ligando obrigatoriamente ao MC presente no edifício A.

**Horizontal cross-connect (HC), Distributor A (DA) or Floor Distributor (FD)**: um em cada andar de cada edifício, ligados obrigatoriamente ao IC do respetivo edifício.

## Tipo de cabos utilizados e os caminhos por eles percorridos
Como as distâncias entre os diferentes edifícios são consideravelmente elevadas, serão adotados cabos do tipo fibra ótica entre o MC (edifício A) e os IC´s dos edifícios (bakcbone cabling) em comprimentos superiores a 90 metros, em distâncias inferiores será usado cobre CAT6. A utilização de fibra vai permitir uma maior banda larga e maior compatibilidade com futuras tecnologias com duas camadas.
Os cabos utilizados têm um núcleo reduzido com o intuito de minimizar a dispersão neste tipo de cabos. A fibra utilizada será de cabo monomodo que, apesar de ser mais caro de produzir e operar, a sua velocidade é bastante superior com pouca perda de integridade.
De forma a prevenir o sistema contra falhas de cabos, foi adotada a medida de redundância de cabos.

# Edifício A #
A estrutura do Edifício A (envolvendo os seus dois andares A0 e A1) está presente nas seguintes figura, contendo também as respetivas medidas das salas:

![edA0_medidas](/doc/sprint1/1181056/Figuras_aux/edA0_medidas.png)

**Legenda: medidas do andar A0, edifício A.**

![edA1_medidas](/doc/sprint1/1181056/Figuras_aux/edA1_medidas.png)

**Legenda: medidas do andar A1, edifício A.**

Após terem sido efetuadas as medidas, é possível calcular o número de tomadas de rede necessárias para as salas cuja regra do número de tomadas tenha que ser respeitada. No caso do nosso projeto, para além das 2 tomadas por cada 10 metros quadrados, o grupo também adotou uma adição de 2 tomadas se a área total da sala fosse superior a 10 metros quadrados e inferior aos 10 metros quadrados seguintes.
Exemplificação: 10 metros quadrados de área = > 2 tomadas, 15 metros quadrados de área = > 4 tomadas;

### Áreas ###
**Andar A0:**

A0.1: +-83 metros quadrados, ou seja, 18 tomadas.

A0.2: +-130 metros quadrados, ou seja, 26 tomadas.

**Andar A1:**

A1.2: +-42 metros quadrados, ou seja, 10 tomadas.

A1.3: +-83 metros quadrados, ou seja, 18 tomadas.

A1.4: +-127 metros quadrados, ou seja 26 tomadas.

![edA0_Final_total](/doc/sprint1/1181056/Figuras_aux/edA0_Final_total.png)

**Legenda: estrutura/plano de cabelagem e equipamento do andar A0 com raio de alcance do access-point do WI-FI wireless, edifício A.**

![edA0_Final_aproximado](/doc/sprint1/1181056/Figuras_aux/edA0_Final_aproximado.png)

**Legenda: estrutura/plano de cabelagem e equipamento do andar A0 aproximado, edifício A.**

![Legenda_edifícios](/doc/sprint1/1181056/Figuras_aux/Legenda_edifícios.PNG)
Nota: Por defeito, os CP´s utilizados têm 24 entradas. No caso do número de tomadas ser superior, é utilizado um com 48 entradas. O uso destes CP´s com um numero tão elevado de entradas remete para a existência de uma possível futura atualização dos aparelhos e tomadas nas salas, permitindo um costante estado de possibilidade de evolução do número de equipamentos.


## Tipo de cabos utilizados e os caminhos por eles percorridos
No interior dos edifícios a utilização de fios de cobre (CAT6) será valorizada e adotada na planificação deste edifício (desde que sejam inferiores a 90 metros).

## Metros de cabo necessários:
### Andar A0####
**CP para tomadas:** 433.5753 metros.

**CP para access-point de WI-FI wireless:** 19.1608 metros (pela parede e posteriormente pelo teto).

**HC para CP:** 59.1384 metros (por apenas um cabo ligado entre cada HC e CP).

**IC para HC:** 5.5 metros (distância desde a caixa na datacenter até ao chão onde se encontra o HC).

**MC para saída do edifício:** 6.9831 metros.

### Andar A1####
**CP para tomadas:** 526.4708 metros.

**HC para CP:** 45.8801 metros (por apenas um cabo ligado entre cada HC e CP).

**IC para HC:** distância muito reduzida, tendo em conta que se encontrar na mesma caixa (aproximadamente 20 cm por cada cabo necessário, e de forma a obter redundância utilizam-se 2 cabos).

**MC para IC:** distância muito reduzida, tendo em conta que se encontrar na mesma caixa (aproximadamente 20 cm por cada cabo necessário, e de forma a obter redundância utilizam-se 2 cabos).

![EdA1_final](/doc/sprint1/1181056/Figuras_aux/EdA1_final.png)

**Legenda: estrutura/plano de cabelagem e equipamento do andar A1, edifício A.**

Na figura seguinte, econtra-se a caixa presente na sala da datacenter (no meio da parede, a 1.5 metros do chão) que contem o MC do campus, o IC do edifício A e do HC desse mesmo andar. 
O MC é um switch com 12 entradas, sendo utilizadas 2 entradas para cada IC de cada edifício.
O IC é um switch apenas com 8 entradas (2 para o MC e as restantes para fazer ligação com os dois HC´s do edifício).
O HC é um switch com 16 entradas (duas entradas para o IC e 10 entradas para os CP´s desse mesmo andar, duas para cada CP).

![caixa_MC_IC_HC](/doc/sprint1/1181056/Figuras_aux/caixa_MC_IC_HC.png)

**Legenda: visualização da caixa de equipamento presente no andar A1, na sala reservada como datacenter, edifício A.**

## Inventário
### Andar A0####
**Total de tomadas:** 49.

**Routers/access-point:** 1, com um PoE.

**Para o HC:** é um switch com 16 entradas (duas entradas para o IC e 6 entradas para os CP´s desse mesmo andar, duas para cada CP).

**Para o CP:** 1 patch panel do tipo CAT6 com 24 ou 48 portas, dependendo do número de tomadas de rede/equipamentos presente na sala onde se encontra o CP.

**3 Telecomunication Enclousers:** todos de tamanho 8U de forma a suportar o HC e os CP´s.

### Andar A1####
**Total de tomadas:** 54.

**Routers/access-point:** 0, pois foi assumido que o router do andar A0 tem um alcance que cobre todo o edifício.

**Para o HC:** é um switch com 12 entradas, sendo utilizadas 2 entradas para cada IC de cada edifício.

**Para o CP:** 1 patch panel do tipo CAT6 com 24 ou 48 portas, dependendo do número de tomadas de rede/equipamentos presente na sala onde se encontra o CP.

**3 Telecomunication Enclousers:** dois de tamanho 8U, para o HC e o CP e um de tamanh 6U para o IC.

Nota: Foram adotados Telecomunication Enclousers de tamanho 8U pois o total de equipamentos somam 4U de tamanha, e recomeda-se que os Telecomuniation Enclousers tenha 100% a mais do tamanho de seus equipamentos, o mesmo para o IC de tamanho 6U.

Nota: O Power over Ethernet (PoE) foi utilizado permite passar energia elétrica aos dispositivos através do CAT5 ou melhores cabos de cobre de pares trançados. O principal uso do PoE é para dispositivos que são
longe de gabinetes de telecomunicações e onde podem não haver tomadas de energia disponíveis.
