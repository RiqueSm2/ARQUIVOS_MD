 * CONSOLE CABLE
 Cabo utilizado para conectar a roteadores e switches.
 Possui duas extremidades:
 1. DB9 (9 pinos) - Conectada ao computador.
 2. RJ45 - Conectada ao roteador ou switch.
 Hoje em dias os laptops não possuem mais a porta DB9, então é necessário um adaptador USB 
 para DB9 para conectar o cabo ao laptop.

* CABOS E FIBRA
Normalmente utilizamos fibra para conectar os switches e roteadores, e utilizamos cabos de rede para conectar os computadores aos switches.

 __ETHERNET:__
  - CAT5e: Distancia de 100m e velocidade de 10 a 1000 Mbps.
  - CAT6: Distancia de 100m e velocidade de 100 a 1gbps e ate 10gbps em distancias menores. Chega a 250mhz. 
  - CAT6a: A principal diferença para o CAT6, é que esta versao trafega a 500mhz.
  - CAT7a: Distancia de 100m, em distancia menores pode chegar a 40gbps mas normalmente ele fica a 10gbps.

 Para distancia muitos grandes, para eliminar a necessida de repetidores, é recomendado o uso de fibra optica.
__FIBRA OPTICA:__

 - Fibra multimodo: Consegue enviar varios sinais de luz ao mesmo tempo cobre
  ate 300m.

 - Fibra monomodo: Envia um sinal de luz ao mesmo tempo, consequente cobre uma distancia maior ate 80km.

 Existem 2 tipos de conectores para fibra optica:
 1. LC (Lucent Connector) -> Conector pequeno, utilizado para conexoes de alta velocidade.
 2. SC (Square Connector) -> Conector maior, utilizado para conexoes de baixa velocidade.

 * ROTEADORES
  __PRINCIPAIS COMPONENTES TRASEIROS__
 1. GROUND CONNECTOR -> "FIO TERRA" - evita queima e retira a eletricidade estatica. 
 2. SECURITY SLOT -> UMA TRAVA PARA EVITAR ROUBO DO ROTEADOR (CADEADO POR EXEMPLO).
 3. POE(POWER OVER ETHERNET) -> PoE (Power over Ethernet) é uma tecnologia que permite enviar energia elétrica + dados pelo mesmo cabo de rede (Ethernet).
 4. GE0/0, GE0/1.. -> GIGA ETHERNET PORTS -> Portas de rede para conexao de computadores, switches, etc.
 5. AUX PORT -> Serve para configuração do dispositivo
 6. CONSOLE PORT (PORTA AZUL) -> Serve para configuração do dispositivo, utilizando o cabo console. (Utiliza-se um RJ45 ou mini usb)
 7. SLOTS -> Para colocar placas de expansão, como por exemplo placas de fibra optica.

 * SWITCHES
 __PRINCIPAIS COMPONENTES TRASEIROS__
 1. POE
 2. FIBER INTERFACES -> Portas para conexao de fibra optica.
 3. LUZES
  3.1 SYSTEM -> Indica o status do switch.(VERDE: Normal, AMARELO/LARANJA: Problema, VERMELHO: Falha)
  3.2 RPS (REDUNDANT POWER SUPPLY) -> Se a fonte de energia principal falhar, a fonte de energia redundante assume o controle.
  3.3 MASTER -> Indica qual é o switch master em um ambiente com varios switches conectados que funcionam como um unico switch.
  3.4 STAUTS
  3.5 DUPLEX/HALF-DUPLEX -> Indica se a conexao esta operando em modo full-duplex ou half-duplex.
  3.6 SPEED -> Indica a velocidade da conexao (10/100/1000 Mbps).
  * STACK-SWITCH
   É um sistema que faz com que varios switches se comportem com um so.
   1. STACK DATA CABLE -> Cabo utilizado para conectar os switches em um stack-switch.
   2. STACK POWER CABLE -> Cabo utilizado para fornecer energia para os switches em um stack-switch.

 * WIRELESS
  ACCESS POINTS (AP) -> LIGHTWEIGHT: DEPENDEDE DE UM CONTROLADOR PARA FUNCIONAR e AUTONOMOUS: FUNCIONA DE FORMA INDEPENDENTE, SEM A NECESSIDADE DE UM CONTROLADOR.  
  WIRELLESS CONTROLLER -> Controla os Access Points, gerenciando a conexao dos dispositivos sem fio e garantindo a segurança da rede sem fio.

 * FIREWALLS
  FIREWALLS -> Dispositivo de segurança de rede que monitora e controla o tráfego de entrada e saída com base em regras de segurança predefinidas. 
   - STATEFULL FIREWALL -> É possivel filtrar o tráfego, com base no IP de origem, IP de destino por exemplo.
   - STATLESS FIREWALL -> Filtra o tráfego com base em regras predefinidas.  

 * TOPOLOGY ARCHITECTURE
  1. WAN (Wide Area Network) -> É você ter a necessidade de chega a algum lugar, fazer a conexao (Ativa a todo momento) adquirindo o serviço de um provedor de internet.
  2. 2tier VS 3 tier _> 2 tier: É uma topologia onde temos apenas dois níveis de hierarquia, o core e o access. 3 tier: É uma topologia onde temos três níveis de hierarquia, o core, o distribution e o access.
  3. SPINER-LEAF -> É como se fosse uma arvore, onde temos um switch central (spiner) e varios switches conectados a ele (leafs). 
  4. SOHO -> Small Office Home Office -> É uma topologia onde temos um pequeno escritório ou uma casa, com poucos dispositivos conectados a internet.
  5. ON-PREMISE/CLOUD -> On-premise: É quando a infraestrutura de rede é mantida e gerenciada internamente pela empresa. 
  Cloud: É quando a infraestrutura de rede é mantida e gerenciada por um provedor de serviços em nuvem.

  * OSI MODEL
    1. Physical Layer (Camada Física) -> Responsável pela transmissão de bits através do meio físico (cabos, fibra óptica, etc.).

    2. Data Link Layer (Camada de Enlace de Dados) -> Responsável pela detecção e correção de erros na transmissão de dados, além de controlar o acesso ao meio físico.

    3. Network Layer (Camada de Rede) -> Responsável pelo roteamento dos pacotes de dados entre os dispositivos na rede.

    4. Transport Layer (Camada de Transporte) -> Responsável pelo controle de fluxo e pela entrega confiável dos dados entre os dispositivos.

    5. Session Layer (Camada de Sessão) -> Responsável por estabelecer, gerenciar e encerrar sessões entre os dispositivos.

    6. Presentation Layer (Camada de Apresentação) -> Responsável por traduzir os dados para um formato que possa ser entendido pelos aplicativos.
    
    7. Application Layer (Camada de Aplicação) -> Responsável por fornecer serviços de rede para os aplicativos, como email, transferência de arquivos, etc.