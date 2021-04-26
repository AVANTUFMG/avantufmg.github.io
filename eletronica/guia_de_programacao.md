---
title: Guia de Programação
layout: default
---

# Guia de Programação da Eletrônica <a class="anchor" id="topo"></a>

**Autor**: Caio Conti Guidote Ribeiro
**Revisado por**: Arthur Amorim, Pedro Giacomin, João Pedro Miranda, Leonardo Hemerly, Arthur Nader, Emanuel Mendes,Gabriel Henrique.

**Publicado**: 03/04/2021 

## Introdução
O objetivo deste guia é unir apresentar sites, vídeos, documentos de aprendizado para os tópicos do contexto da equipe de Eletrônica da iniciativa AVANT UFMG, ou seja, para aeronaves autônomas. Este documento é atualizado constantemente pelos membros, para conter fontes coerentes com as atividades desenvolvidas pela equipe a todo tempo.

Para saber mais sobre a AVANT, acesse nosso [site](https://avant-ufmg.wixsite.com/avantufmg).
Todos relatórios técnicos completos e públicos se encontram no [Drive Público AVANT](https://drive.google.com/drive/u/0/folders/1Hdz1nv4uH7lsDzs-XulJL0Ub4Opml2fZ).
Os códigos podem ser vistos em nosso perfil no [GitHub](https://github.com/AVANTUFMG/AVANTLink).

## Índice
- [Python para Iniciantes](#python-para-iniciantes)

- [Integração de Sistemas](#integracao)
  - [Comunicação com WiFi](#integracao-1)

- [ROS(Robot Operating System)](#ros)
  - [Instalação e Configuração](#ros-1)
  - [Conceitos e Programação Básica](#ros-2)
  - [Instalando o Turtlebot3 no Melodic no Ubuntu 18.04](#ros-3)
  - [Utilizando Python com classes e sem variáveis globais](#ros-4)
  - [Como fizemos na competição Petrobras](#ros-5)
  - [Mavros](#ros-6)
  - [Dicas e soluções de erros](#ros-7)

- [Visão Computacional](#visao)
  - [Processamento de Imagens](#visao-1)
  - [OpenCV](#visao-2)
  - [Machine Learning](#visao-3)
    - [Deep Learning em Visão Computacional](#visao-3-1)
    - [TensorFlow](#visao-3-2)
  - [Visão Computacional na AVANT](#visao-4)

- [Busca de Rota](#busca)
  - [Grafos](#busca-1)
  - [Algoritmos de busca](#busca-2)
    - [Dijkstra](#busca-2-1)
    - [A* (A star)](#busca-2-2)
  - [Implementação e relatórios da AVANT](#busca-3)
  - [Próximos passos](#busca-4)

- [Controle](#controle)
  - [Curso de Controle Clássico](#controle-1)
    - [Material Adicional](#controle-1-2)
  - [Introdução ao Controle Automático de Aeronaves](#controle-2)
    - [Referenciais usados em controles de Aeronaves](#controle-2-1)
    - [Mudanças de Coords e Representação Matricial do Produto Vetorial](#controle-2-2)
  - [Vídeo do professor Leonardo Torres sobre Dinâmica Longitudinal](#controle-3)
  - [Página do professor Dimas no GitHub (mecânica do voo e modelo longitudinal)](#controle-4)
  - [Introdução a Controladores PID](#controle-5)
  - [Para aprender SimuLink](#controle-6)

- [Hardware](#hardware)
  - [Relatórios do Hardware da AVANT](#hardware-1)
      - [Descrição dos documentos](#hardware-1-1)
  - [Construindo um multirrotor](#hardware-2)
  - [Erros comuns](#hardware-3)
  - [Links úteis](#hardware-4)
    - [Sobre Pixhawk](#hardware-4-1)
    - [Sobre Ardupilot](#hardware-4-2)
    - [Funcionamento de um motor brushless](#hardware-4-3)

- [Git e GitHub](#git-github)
  - [Básico de Git](#git-github-1)

- [Mecânica Básica](#mec-basica)
  - [Introdução à Engenharia Aeronáutica](#mec-basica-1)

- [Linux](#linux)
  - [Introdução ao Terminal](#linux-1)

*** 

## 1) Python para Iniciantes <a class="anchor" id="python-para-iniciantes"></a>
[Voltar ao topo](#topo)

Este site é muito bom para começar a aprender os básicos de programação em Python:
https://www.learnpython.org/

Sugerimos a seguinte playlist de python para os que ainda não conhecem programação:
https://www.youtube.com/playlist?list=PLHz_AreHm4dlKP6QQCekuIPky1CiwmdI6


## 2) Integração de Sistemas <a class="anchor" id="integracao"></a>
[Voltar ao topo](#topo)

Essa é a área responsável pela comunicação entre os dois diferentes tipos de hardware utilizados em um projeto de drones autônomos, o computador de bordo e a controladora. No nosso caso utilizamos uma raspberry pi e pixhawk. 
No caso da AVANT a comunicação entre ambos os hardwares se dá utilizando o protocolo MAVLink, no entanto, a programação utilizando apenas o protocolo como base é de muito baixo nível e trabalhosa. Para melhorar a situação utilizaremos o ROS (Robot Operating System), framework utilizado que abstrai e facilita essa comunicação que é muito utilizado para toda área de robótica.
Utilizaremos então o pacote Mavros que faz a ponte entre o ROS e o protocolo MAVLink, veja o tópico do ROS para entender melhor.

### 2.1) Comunicação com Wifi <a class="anchor" id="integracao-1"><a/>
O documento “[Andorinha Autônoma](https://drive.google.com/file/d/1jd6OjqJyxdhe5hmFh7nz6wxVSnbxnLhD/view?usp=sharing)” descreve as conexões, piloto automático e comunicação WiFi da Pixhawk com Raspberry. Esse documento é útil apesar de não retratar com exatidão a operação da AVANT atualmente.


## 3) ROS (Robot Operating System) <a class="anchor" id="ros"><a/>
[Voltar ao topo](#topo)

A documentação do ROS não é muito boa porém explicaremos e evidenciaremos os tutoriais e documentos que utilizamos para o conhecimento básico. Como esse sistema requer o conhecimento de novos conceitos, recomendamos fortemente que o estudante anote as ideias básicas (o que é um nó, tópico, publisher...) para quando se perder ou confundir possa rapidamente olhar suas anotações e relembrar.
Fica também a sugestão de quando estiver programando deixar sempre a página de tutoriais do ROS aberta e a utilizar como uma espécie de apostila.

### 3.1) Instalação e configuração <a class="anchor" id="ros-1"><a/>
Em Core ROS Tutorials -> Begginer Level da aula 1 até a aula 4 explicam como instalar o ROS e criar um pacote.  Você pode também seguir o tutorial da playlist mostrada no próximo item, porém o site tem algumas dicas interessantes que não tem nos vídeos. Por segurança nada o impede de ver os dois.
http://wiki.ros.org/ROS/Tutorials

### 3.2) Conceitos e programação básica <a class="anchor" id="ros-2"><a/>
Os tutoriais do ROS do 5 até o 16 servem para entender os conceitos básicos e fazer simples programas, recomendo fortemente pelo menos a sua leitura.
http://wiki.ros.org/ROS/Tutorials

Segue uma excelente playlist, em português, muito bem explicativa sobre os básicos do ROS, ela basicamente (com exceções) segue os passos dos tutoriais do site. Vale a pena assistir até a aula 14, a aula 15 em diante diz sobre simulações, veja qual dos simuladores te interessa mais (nosso caso utilizamos o Gazebo).
https://www.youtube.com/watch?v=DcJhspJiHV4&list=PLhxZVyws6YtsbTPilPWwiPFEGf2ztH5kR

Criamos um documento com anotações sobre essa aula: [Guia com anotações sobre as aulas da playlist](https://drive.google.com/file/d/1Abr1z3Ndiyu4ymqji2Av0lACO1tdBTtY/view?usp=sharing)

### 3.3) Instalando o Turtlebot3 no Mellodic no Ubuntu 18.04 <a class="anchor" id="ros-3"><a/>
Pode vir a ser útil ou interessante ao usuário saber como instalar o Turtlebot3 nessa versão. O tutorial abaixo explica de forma fácil.
https://automaticaddison.com/how-to-launch-the-turtlebot3-simulation-with-ros

### 3.4)  Utilizando Python com classes e sem variáveis globais <a class="anchor" id="ros-4"><a/>
Pode ter visto que na playlist sugerida a pessoa utiliza variáveis globais no seu código, porém esse método não é o ideal, como python não consegue utilizar referências como o C++ podemos driblar criando classes. Segue abaixo um link explicando o funcionamento.
https://roboticsbackend.com/oop-with-ros-in-python/

### 3.5) Como fizemos na competição <a class="anchor" id="ros-5"><a/>
Disponibilizamos uma aula de como fizemos a parte de controle para o Desafio de robótica PETROBRAS onde um drone simulado tinha que fazer várias missões como por exemplo pousar numa plataforma com visão computacional. Participamos desse projeto junto com a Xquad time de drones do VeRLab. Também disponibilizamos os documentos da competição e os github.

Aula explicativa por Caio Conti da AVANT sobre como fizemos o sistema funcionar com o ROS em Python, com dicas e informações importantes que descobrimos durante a competição e também sem utilizar variáveis globais. Fazer um pequeno documento com essas dicas pode ser interessante:
https://youtu.be/CX3fGPBugc4

Nosso github da competição:
https://github.com/AVANTUFMG/CompeticaoPetrobras2020

Sobre o desafio (categorias -> simulação 3d -> Desafio de Robótica PETROBRAS): http://www.cbrobotica.org/

Para mexer/simular nesses espaços seguem pdfs e github da competição:
- Github da petrobras (também explicando como instalar): https://github.com/LASER-Robotics/Petrobras_Challenge
- Github do sistema (mas explica no git da petrobras também): https://github.com/ctu-mrs/mrs_uav_system
- Documentação do sistema mrs_uav: https://ctu-mrs.github.io/docs/system/uav_ros_interface.html
- PDF da competição: [PDF COMPETIÇÃO PETROBRAS](https://drive.google.com/file/d/11FIZEAySuLh-3QkqDKS8rUDU-DtM04Y_/view?usp=sharing)
- Regras auxiliares da competição (diz sobre a parte virtual): [PDF REGRAS AUXILIARES COMPETIÇÃO](https://drive.google.com/file/d/1R5OrlU1JsNfebHDtPqy5MI2X_C1IAbK0/view?usp=sharing)

### 3.6) Mavros <a class="anchor" id="ros-6"><a/>
Agora que já aprendeu os básicos do ROS, deve começar o estudo do Mavros, como dito acima, é um pacote que utiliza o protocolo MAVLink e já nos dá facilidades para não termos programar em muito baixo nível utilizando apenas esse protocolo.
Essa seção precisa de mais detalhamento e relatórios quando formos progredindo com o Mavros.

Caso queira entender apenas o que é o MAVLink:
https://mavlink.io/en/

Documentação do Mavros (contém os tópicos e etc):
http://wiki.ros.org/mavros

Instalação do Mavros: 
https://dev.px4.io/master/en/ros/mavros_installation.html

Siga as instruções do site PX4 para simular e fazer um controle básico de um drone (precisa-se de mais testes para avaliar esses tutoriais):
https://dev.px4.io/master/en/ros/

GitHub de Mavros com python:
https://github.com/PX4/PX4-Autopilot/tree/master/integrationtests/python_src/px4_it/mavros

Modos (pode vir a ser útil):
http://wiki.ros.org/mavros/CustomModes#PX4_native_flight_stack

### 3.7) Dicas e soluções de erros <a class="anchor" id="ros-7"><a/>
Segue um documento de erros encontrados durante a instalação do ROS e também durante a competição da Petrobras juntamente com algumas dicas.
[Dicas e Erros do ROS e da competição](https://docs.google.com/document/d/1DxpssgU64V2rT5Q-HbBRzzdbMkeMCCxI-k7ubdSpmLI/edit?usp=sharing)

Como no ROS costuma ser necessário manter várias instâncias do terminal abertas simultaneamente, o Terminator pode ser útil para melhorar a organização. Segue um link explicando o que é e como instalá-lo:
https://dev.to/xeroxism/how-to-install-terminator-a-linux-terminal-emulator-on-steroids-1m3h


## 4) Visão Computacional <a class="anchor" id="visao"><a/>
[Voltar ao topo](#topo)

A equipe de visão computacional tem como função desenvolver algoritmos que extraem informação das imagens capturadas pelo equipamento do VANT. Extrair informações das imagens, nesse caso, é interpretá-las e conseguir determinar o que ela contém, se é uma pista de pouso, um possível obstáculo, e etc. Essas informações são essenciais para a autonomia da aeronave, pois é com elas que ela pode “decidir” que caminho tomar.


### 4.1) Processamento de Imagens <a class="anchor" id="visao-1"><a/>
As imagens captadas pelo VANT podem conter ruídos e diversas outras informações que não são relevantes para o algoritmo de extração de informação. Para eliminar tais ruídos é necessário, durante a execução do algoritmo, uma sequência de operações e filtros na imagem em questão. Segue livro que introduz processamento de imagens e conceitos da visão computacional.

<br>[Concise Computer Vision](https://doc.lagout.org/science/0_Computer%20Science/2_Algorithms/Concise%20Computer%20Vision_%20An%20Introduction%20into%20Theory%20and%20Algorithms%20%5BKlette%202014-01-20%5D.pdf) (necessária somente a leitura dos capítulos 1 e 2)


### 4.2) OpenCV <a class="anchor" id="visao-2"><a/>
A equipe utiliza a biblioteca OpenCV para desenvolver os programas. Essa biblioteca é open source e completamente livre para o uso acadêmico e profissional. Ela fornece toda a base para o desenvolvimento dos programas dado que muitos algoritmos já vem prontos e abstrai a maior parte da matemática que acontece por baixo dos panos. A própria documentação da biblioteca é uma ótima fonte para aprender o que é necessário:

[OpenCV: OpenCV Tutorials](https://docs.opencv.org/master/d9/df8/tutorial_root.html)
[OpenCV - Python Tutorials](https://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_tutorials.html)

Atualmente utilizamos o python como linguagem  dos algoritmos  desenvolvidos dentro da equipe. Segue alguns cursos introdutórios para um primeiro contato com a biblioteca utilizando python:

[Aulas de introdução python e opencv](https://www.youtube.com/watch?v=oAH_GJclePY&list=PL-t7zzWJWPtx3enns2ZAV6si2p9zGhZJX&ab_channel=UniversoDiscreto)  [BR]
[Introdução OpenCV](https://www.youtube.com/watch?v=WQeoO7MI0Bs&ab_channel=Murtaza%27sWorkshop-RoboticsandAI) [EN]
[Curso de Introdução com exemplos](https://www.youtube.com/playlist?list=PLS1QulWo1RIa7D1O6skqDQ-JZ1GGHKK-K) [EN]

## 4.3 Machine Learning <a class="anchor" id="visao-3"><a/>
Muitos dos problemas sob responsabilidade da área de Visão Computacional, como reconhecimento de objetos em imagens aéreas e detecção e localização de pistas de pouso em imagens, são complexos demais para serem resolvidos apenas com processamento de imagem, por isso a equipe usa algoritmos de aprendizado de máquina (machine learning), que é uma abordagem mais robusta para esses tipos de problema. 

### 4.3.1 Deep Learning em Visão Computacional <a class="anchor" id="visao-3-1"><a/>
Um excelente recurso para entender como Deep Learning pode ser aplicado para resolver problemas de Visão Computacional é o curso CS231n, de Stanford, disponível online.

[Playlist com as videoaulas no YouTube](https://www.youtube.com/playlist?list=PLkt2uSq6rBVctENoVBg1TpCC7OQi31AlC)
[Site do curso com exercícios e notas de aula](https://cs231n.github.io/)

### 4.3.2 TensorFlow <a class="anchor" id="visao-3-2"><a/>
Para aplicar a teoria, a AVANT utiliza o TensorFlow, uma biblioteca de código aberto utilizada para implementar algoritmos de Machine Learning. 

[Tutoriais do site oficial](https://www.tensorflow.org/tutorials)
[Documentação da biblioteca](https://www.tensorflow.org/api_docs) 

### 4.4) Visão Computacional na AVANT <a class="anchor" id="visao-4"><a/>
No drive da AVANT há também relatórios feitos pelos membros da equipe que explicam muitos dos conceitos utilizados nos algoritmos desenvolvidos e também os próprios algoritmos, o que é útil para que o novo membro consiga entender como a equipe trabalha e ter um panorama geral de como foram feitos os trabalhos até então:

[Visão Computacional - Google Drive](https://drive.google.com/drive/folders/1EPiASUdPu588jAsrnuemCakcglNFD3RZ?usp=sharing)

Segue o link dos algoritmos desenvolvidos :

[Algoritmo de detecção de objetos](https://github.com/AVANTUFMG/AVANTLink/blob/master/pythonSublib/visao_comp/canny-t.py) 
[Algoritmo de classificação de objetos](https://github.com/AVANTUFMG/AVANTLink/blob/master/pythonSublib/visao_comp/classificacao.py) 


## 5) Busca de Rota <a class="anchor" id="busca"></a>
[Voltar ao topo](#topo)

É responsável pela implementação de algoritmo que decidem a rota do drone, desviando de obstáculos e que seja um bom caminho a ser percorrido. 
A AVANT implementou primeiramente um algoritmo de busca simples para depois programar o dijkstra até sua modificação para o A* (A estrela) em 3D.

### 5.1) Grafos <a class="anchor" id="busca-1"></a>
Para começar, veja um pouco sobre grafos, pois os algoritmos de busca de caminho (inclusive o que usamos) os utilizam sugerimos os seguintes links:

Explicação muito breve sobre grafos:
https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/

Explica o conceito rapidamente e um exemplo de implementação em c++. Contém também um vídeo:
https://www.geeksforgeeks.org/graph-and-its-representations/

### 5.2) Algoritmos de busca <a class="anchor" id="busca-2"></a>
Antes de ver como foi nossa implementação e nossos relatórios entenda o funcionamento dos algoritmos utilizados, recomendamos os seguintes vídeos explicativos:

#### 5.2.1) Dijkstra <a class="anchor" id="busca-2-1"></a>
Vídeo de uma aula de estrutura de dados do canal UNIVESP, contém a melhor explicação do algoritmo que encontrei:
https://youtu.be/ovkITlgyJ2s
O Canal Computerphile também abordou o Dijkstra:
https://youtu.be/GazC3A4OQTE
O site geeksforgeeks explica o algoritmo e propõe exemplos em C++, Java, Python e C*
https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7

#### 5.2.2) A* (A star) <a class="anchor" id="busca-2-2"></a>
O A* é basicamente uma modificação do Dijkstra, segue um vídeo explicativo do canal Computerphile:
https://youtu.be/ySN5Wnu88nE
Geeksforgeeks também tem conteúdo bem explicativo que vale a pena ler e um exemplo de código, mas um pouco longo, não é necessário o entendimento deste código específico para atividades da AVANT.
https://www.geeksforgeeks.org/a-search-algorithm/

### 5.3) Implementação e relatórios da AVANT <a class="anchor" id="busca-3"></a>
Em nosso drive temos uma série de relatórios explicativos da evolução da abordagem que utilizamos para busca de rota até chegar a implementação.

Os relatórios de busca de rota podem ser encontrados aqui: [Pathfinding AVANT](https://drive.google.com/drive/u/0/folders/1mCHgJYzLHMw_YRCPsKOI_xmbBXPacv_X)

Sugerimos o seguinte estudo dos relatórios na ordem:
1. Relatório Pathfinding - Ideia Geral
2. Relatório Pathfinding - Transformação
3. Relatório Pathfinding - V1
4. Relatório Pathfinding - V2
5. Relatório Pathfinding - Dijkstra e A estrela

Para facilitar temos uma versão zipada do projeto do A* no drive: [Demo de programas](https://drive.google.com/drive/u/0/folders/1fNqX0t35iMUD3tY5m3Msvr5lR6s6C1JH)
No entanto essa versão pode não ser a última.

### 5.4 Próximos passos <a class="anchor" id="busca-4"></a>
Estamos trabalhando com curvas de Bézier para otimizar o movimento do drone já que pelo algoritmo ele faria um movimento brusco de 90º o que não é nada ideal. Um relatório já pode ser encontrado no drive em pathfinding (link no tópico anterior) com o nome de Relatório AVANT - Implementação Bézier.


## 6. Controle <a class="anchor" id="controle"></a>
[Voltar ao topo](#topo)

A área de controle pode requerer mais conhecimento prévio para compreender em sua totalidade, especificaremos vídeo aulas sobre engenharia de controle e controle de aeronaves que utilizamos para estudar. Para fazer o controle devemos entender o básico de mecânica de aeronaves, portanto, as playlists abaixo também discorrem sobre o assunto. A modelagem do sistema de controle será feita em MATLAB com o SimuLink.

### 6.1 Curso de Controle Clássico <a class="anchor" id="controle-1"></a>
A seguinte playlist contém as aulas de controle clássico/contínuo do professor Luiz Antonio Aguirre da UFMG:
https://www.youtube.com/playlist?list=PLALrL4i0Pz6CfqappJPo-45HZj0AavVyO

Para acompanhar o conteúdo abordado por ele, é preciso ter conhecimento sobre o que é e como funciona a Transformada de Laplace. Esse assunto é abordado no vídeo:
https://www.youtube.com/watch?v=GrRWAOqF2p0&t=310s

#### 6.1.1 Material Adicional <a class="anchor" id="controle-1-1"></a>
O seguinte vídeo traz uma explicação geral sobre funções de transferência, e o canal tem mais alguns vídeo sobre controle:
https://www.youtube.com/watch?v=RJleGwXorUk&t=325s

Além disso, o canal “Eng Luis Cesar Emanuelli” também abordou o tema de controle clássico, dando uma boa visão sobre sinais de teste e sistemas de 1ª e 2ª Ordem, respectivamente nos vídeos:
https://www.youtube.com/watch?v=sTXlDr3lglU
https://www.youtube.com/watch?v=2oOTkSRnaG4&list=PLotZYHQBkGgQ7LzIkslTtXzmElRn7-Y99&index=4
https://www.youtube.com/watch?v=UVFer8huMKE&list=PLotZYHQBkGgQ7LzIkslTtXzmElRn7-Y99&index=5

### 6.2 Introdução ao Controle Automático de Aeronaves <a class="anchor" id="controle-2"></a>
A seguinte playlist contém as aulas do professor Leonardo Torres da UFMG da matéria de Introdução ao Controle Automático de Aeronaves:
https://www.youtube.com/watch?v=V6xtp1PTThc&list=PLlYmsBqKzggTCQsnK65BiJFyIzcmRRQLZ

Os dois vídeos a seguir estão contidos na playlist acima, porém são de extrema importância para o entendimento da aula sobre a dinâmica longitudinal de uma aeronave:

#### 6.2.1 Referenciais usados em controles de Aeronaves <a class="anchor" id="controle-2-1"></a>
https://www.youtube.com/watch?v=UG5i2uGFOCk

#### 6.2.2 Mudanças de Coordenadas e Representação Matricial do Produto Vetorial <a class="anchor" id="controle-2-2"></a>
https://www.youtube.com/watch?v=mVkJSTPyi2Q

### 6.3 Vídeo do professor Leonardo Torres sobre Dinâmica Longitudinal <a class="anchor" id="controle-3"></a>
Aula onde é feita a modelagem matemática da dinâmica longitudinal de vôo de uma aeronave:
https://www.youtube.com/watch?v=NAvZyyTD-lM

### 6.4 Página do professor Dimas no GitHub (mecânica do voo e modelo longitudinal) <a class="anchor" id="controle-4"></a>
A página contém notas sobre mecânica de voo e modelo longitudinal de um avião, tendo compiladas suas principais fórmulas e conceitos. Pode ser usada como material complementar aos vídeos acima ou para consulta. 
http://dimasad.github.io

### 6.5 Introdução a Controladores PID <a class="anchor" id="controle-5"></a>
Fizemos um relatório de Introdução a Controladores PID, disponível em:
Pasta de controle

### 6.6 Para aprender SimuLink <a class="anchor" id="controle-6"></a>
Playlist do MATLAB sobre a utilização do SimuLink:
https://www.youtube.com/playlist?list=PL484BA2AD3AE4C2D0


## 7. Hardware <a class="anchor" id="hardware"></a>
O Hardware utilizado por nós é bem simples, básico e direto, utilizamos um computador de bordo e uma controladora (Raspberry e Pixhawk respectivamente) seguem as documentações criadas explicando o funcionamento. 

### 7.1 Relatórios do Hardware da AVANT <a class="anchor" id="hardware-1"></a>
A seguinte pasta contém os relatórios do hardware utilizado por nós, com a descrição dos componentes, manuais e um PDF contendo os erros comuns:
[Hardware AVANT](https://drive.google.com/drive/folders/1acZNQaCOLzAjtIl4iHGaLYlTvzeT6rPf?usp=sharing)

#### 7.1.1 Descrição dos documentos <a class="anchor" id="hardware-1-1"></a>
Os documentos de conexão e hardware com uma breve descrição:
- Hardware Besourinho: descreve os componentes básicos utilizados no projeto da aeronave da AVANT chamada de “Besourinho”

- Andorinha Autônoma: Descreve as conexões, piloto automático e comunicação WiFi da Pixhawk com Raspberry. Esse documento é antigo e não retrata com exatidão a operação da AVANT atualmente.

- pixhawk-manual-rev7-1: Deve ser lido, explica o funcionamento e conexões da Pixhawk, um manual.

- Direção da rotação: Imagem demonstrando as direções de rotação de um quadricóptero.

### 7.2 Construindo um Multirrotor <a class="anchor" id="hardware-2"></a>
O documento “Metodologia de Construção de um Multirrotor” descreve o procedimento de escolha de componentes e construção de drones multirrotores.

### 7.3 Erros Comuns <a class="anchor" id="hardware-3"></a>
No documento “Erros comuns” , como diz o nome, são as falhas mais frequentes encontradas durante nossos testes com possíveis diagnósticos.

### 7.4 Links Úteis <a class="anchor" id="hardware-4"></a>
Seguem alguns links e referências úteis:

#### 7.4.1 Sobre PixHawk <a class="anchor" id="hardware-4-1"></a>
https://pixhawk.org/

#### 7.4.2 Sobre o Ardupilot <a class="anchor" id="hardware-4-2"></a>
https://ardupilot.org/

#### 7.4.3 Funcionamento de um motor brushless <a class="anchor" id="hardware-4-3"></a>
https://howtomechatronics.com/how-it-works/how-brushless-motor-and-esc-work/


## 8) Git e GitHub <a class="anchor" id="git-github"></a>
O git é um sistema de controle de versão/versionamento distribuído, utilizado amplamente no desenvolvimento colaborativo de software. Seu funcionamento pode ser um pouco confuso, mas em resumo ele serve para armazenar o histórico de alterações de um ou mais arquivos. O GitHub é um website que utiliza Git, além de acrescentar algumas funcionalidades, e é onde se encontram os repositórios de código da AVANT.

### 8.1) Básico sobre Git <a class="anchor" id="git-github-1"></a>
Além da pasta “Slides GIT” que contém os slides de uma aula de Git ministrada anteriormente na equipe, há também o próprio handbook do GitHub:
https://guides.github.com/introduction/git-handbook/


## 9) Mecânica Básica <a class="anchor" id="mec-basica"></a>
Ser introduzido às diferentes áreas de um projeto contribui para que o engenheiro tenha uma visão mais holística daquilo que está construindo. Dessa forma, ficam mais claras as consequências e finalidades de cada parte desenvolvida no projeto, bem como as limitações daquilo que pode ser feito. Por isso, é importante que os membros da eletrônica conheçam ao menos o básico do funcionamento mecânico de uma aeronave.

### 9.1 Introdução à Engenharia Aeronáutica <a class="anchor" id="mec-basica-1"></a>
Livros introdutórios de Engenharia Aeronáutica
- Leitura necessária: páginas 17 a 35
https://engenhariaaeronautica.com.br/ebook/introducao/ebookintro.pdf

- Leitura necessária: capítulos 2, 4 e 5
https://drive.google.com/file/d/1OfFzopyx0OIA-PQz4zjX5VTKibwRHPDt/view?usp=sharing


## 10) Linux <a class="anchor" id="linux"></a>
O termo Linux é comumente usado para se referir a Sistemas Operacionais que utilizam o kernel Linux, desenvolvido por Linus Torvalds, e é a isso que estamos nos referindo aqui. Feita a ressalva quanto ao termo, sentir-se confortável utilizando o terminal no Linux para navegar pelos arquivos é fundamental para o desenvolvimento de software de maneira geral. Muitas vezes é inclusive mais eficiente utilizar o terminal ao invés de uma interface gráfica, se o desenvolvedor sabe como utilizá-lo.

### 10.1 Introdução ao Terminal <a class="anchor" id="linux-1"></a>
Segue abaixo um livro introdutório e bastante completo que ensina a comandos básicos do terminal, programação em Bash, Git e GitHub e algumas ideias de computação em nuvem. O capítulo 7 sobre computação em nuvem não precisa ser lido, fica a nível de curiosidade, mas recomendamos a leitura dos capítulos 1 ao 5, sobre Linux básico e Bash, e do 6, sobre Git e GitHub.
[The Unix Workbench - Sean Kross](https://seankross.com/the-unix-workbench/)

Abaixo estão dois cursos gratuitos (MOOC) sobre Linux
[Linux Basics: The Command Line Interface - Dartmouth College](https://www.edx.org/course/linux-basics-the-command-line-interface)
[Introduction to Linux - The Linux Foundation](https://www.edx.org/course/introduction-linux-linuxfoundationx-lfs101x-1)























