RCOMP 2019-2020 Project - Sprint 1 - Member 1181053 folder
===========================================

# Edifício D

A representação do Edifício D pode ser visualizada nas seguintes imagens. Inclui a localização dos cabos, cross-connects e access-points e das fichas.

![CampusMedidas](/doc/sprint1/1181053/Figuras_aux/D0.png)

![CampusMedidas](/doc/sprint1/1181053/Figuras_aux/D1.png)

Há cabos que estão dentro das paredes e também cabos numa calha suspensa representada a verde. Deve ainda ser referido que as fichas mais perto das paredes são fichas de parede e os cabos situados na respetiva parede ligam-se a elas. Os APs estão situados na calha suspensa, daí a sua representação no 2º andar sem nenhum suporte.

## Áreas:

#### Andar D0:

D0.1: 56 metros quadrados (12 tomadas)

D0.2: 56 metros quadrados (12 tomadas)

D0.3: 64 metros quadrados (14 tomadas)

D0.4: 48 metros quadrados (10 tomadas)

Área Aberta: 1872 metros quadrados (376 tomadas)

#### Andar D1:

D1.1: 56 metros quadrados (12 tomadas)

D1.2: 56 metros quadrados (12 tomadas)

D1.3: 96 metros quadrados (20 tomadas)

D1.4: 48 metros quandrados (10 tomadas)



Considerou-se para este edifício que ambos o HC e o CP têm a capacidade de 48 fichas em cada rack, com 6 racks, para um total de 288 fichas por HC ou CP.



## Tipo de cabos utilizados e os caminhos por eles percorridos

No interior dos edifícios a utilização de fios de cobre (CAT6) será valorizada e adotada na planificação deste edifício (desde que sejam inferiores a 90 metros).

## Metros de cabo necessários:

Cabo entre MC e IC: 60 metros. Para redundância podemos multiplicar este valor pelo número de cabos que queremos.

Cabo entre IC e HC: 12 metros. Para redundância podemos multiplicar este valor pelo número de cabos que queremos.

Cabo entre HC e CPs: 125 metros. Para redundância podemos multiplicar este valor pelo número de cabos que queremos.

Cabo entre HC e fichas: 6000 metros. Este valor é aproximado e foi calculado através de multiplicações usando os valores mais elevados em sistemas homogéneos.

## Inventário

### Andar D0

**Total de tomadas:** 424.

**Para o HC:** 1 patch panel do tipo CAT6 com 48 portas.

**Para o IC:** switch com 8 entradas.

**Para o CP:** 3 CPs, cada um com 6 patch panel do tipo CAT6 com 48 portas, dependendo do número de tomadas de rede/equipamentos presente na sala onde se encontra o CP.

### Andar D1

**Total de tomadas:** 54.

**Para o HC:** 1 patch panel do tipo CAT6 com 48 portas.



Nota: Dois routers estão situados nas calhas entre andares.

Nota: Foram adotados Telecomunication Enclosers de tamanho 8U pois o total de equipamentos somam 4U de tamanha, e recomenda-se que os Telecomunication Enclosers tenha 100% a mais do tamanho de seus equipamentos, o mesmo para o IC de tamanho 6U.

Nota: O Power over Ethernet (PoE) foi utilizado permite passar energia elétrica aos dispositivos através do CAT5 ou melhores cabos de cobre de pares trançados. O principal uso do PoE é para dispositivos que são longe de gabinetes de telecomunicações e onde podem não haver tomadas de energia disponíveis.