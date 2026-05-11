
# REDES CISCO — MATERIAL COMPLETO

---

# SUMÁRIO

1. MODES
2. BASIC CONFIGS
   - HOSTNAME
   - ENABLE SECRET
   - CLOCK
   - BANNER MOTD
   - SALVAR CONFIGS
3. INTERFACES
   - ATIVAR INTERFACE
   - LISTAR INTERFACES
   - IP ADDRESS
4. IPV6
   - IPV6
   - IPV6 UNICAST
5. SWITCHES
6. CONEXAO REMOTA
   - TELNET
   - SSH
7. SWITCH LAYER 2
8. SWITCH LAYER 3
9. VLANS
10. MOSTRAR ENDEREÇO MAC
11. CDP (CISCO DISCOVERTY PROTOCOL)
12. LLDP (LINK LAYER DISCOVERY PROTOCOL)
13. BACKUP
14. CONSOLE CABLE
15. CABOS E FIBRA
16. FIBRA OPTICA
17. CONECTORES DE FIBRA
18. ROTEADORES
19. SWITCHES
20. STACK-SWITCH
21. WIRELESS
22. FIREWALLS
23. TOPOLOGY ARCHITECTURE
24. OSI MODEL
25. COMANDOS E SUAS FUNÇÕES


# MODES

Com '?' lista todos os comandos presentes naquele modulo

* MODES
ROUTER> - USER MODE
ROUTER# - PRIVILEGED MODE (ROOT)
ROUTER(config)# - CONFIGURATION MODE
ROUTER(config-if)# - INTERFACE CONFIGURATION MODE

---

# BASIC CONFIGS

* HOSTNAME
Router>enable 
Router#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#hostname NY_R1
NY_R1(config)#

* ENABLE SECRET (ALTERA A SENHA DE ACESSO AO MODO PRIVILEGED)
NY_R1#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
NY_R1(config)# enable secret cisco

* CLOCK (RELOGIO DO ROTEADOR)

__LOCAL__
NY_R1#show clock
*1:47:44.876 UTC Mon Mar 1 1993
NY_R1#clock set 13:27:00 02 MAY 2026
NY_R1#show clock
13:27:6.148 UTC Sat May 2 2026

__NTP__
O clock NTP é utilizado para sincronizar o relógio do roteador com um servidor NTP, garantindo que a hora esteja sempre correta.
NY_R1(config)#ntp server 2.2.2.2

NY_R1(config)#no ntp server 2.2.2.2 -> O 'no' nega a configuração feita. 

* BANNER MOTD (EXIBE UMA MENSAGEM QUANDO ALGUEM ACESSA O ROTEADOR)
NY_R1(config)#banner motd ^
Enter TEXT message.  End with the character '^'.

NY_ROUTER

^

* SALVAR CONFIGS (STARTUP CONFIG - VRAM)
NY_R1#COPY RUNNING-CONFIG STARTUP-CONFIG 
ou 
NY_R1# WR
Destination filename [startup-config]? 
Building configuration...
[OK]

---

# INTERFACES

* ATIVAR INTERFACE
NY_R1(config)#interface gigabitethernet 0/0
NY_R1(config-if)#no shutdown

* LISTAR INTERFACES
Para saber as interfaces do roteador, usamos:
NY_R1#show running-config 
ou
NY_R1#show ip interface brief
ou 
show interfaces para mais detalhes.

* IP ADDRESS

NY_R1(config)#interface gi
NY_R1(config)#interface gigabitEthernet 0/0
NY_R1(config-if)#ip address 10.1.1.1 255.255.255.0

---

# IPV6

## IPV6

NY_R1#show ipv6 interface brief - > Exibe interfaces IPV6 e seus endereços.

DEFININDO O ENDEREÇO IPV6
NY_R1(config)#interface gigabitEthernet 0/0
NY_R1(config-if)#ipv6 address 2001:0db8:3c4d:0015:0000:0000:1a2f:1a2b/64

## IPV6 UNICAST
Ativando UNICAST
IPV6 UNICAST ROUTING
IPV6 ROUTE  <IPV6 DESTINO> <PREFIXO> <IPV6 PROXIMO SALTO OU INTERFACE DE SAIDA>

---

# SWITCHES

Configurações basicas é o mesmo do ROTEADOR

* IP PARA GERENCIAMENTO
Em switches de LAYER2, é necessário configurar um IP para gerenciar o switch remotamente.
A interface VLAN, em switchers de LAYER2, é a interface normalmente utilizada para gerenciamento.

NY_SW1(config)#interface vlan 1
NY_SW1(config-if)#ip add 192.168.10.2 255.255.255.0

show version -> Exibe a versão do IOS do switch, além de outras informações como o modelo do switch, a quantidade de memória, etc.
---

# CONEXAO REMOTA

A conexao entre aparelhos ela pode ser feita remotamente, utilizando TELNET ou SSH, 
que acessam diretamente uma porta virtual, que é chamada de LINE VTY.

Dentro dessa LINE VTY, existem varias sessões que vao de 0 a 15 ou ate mais dependendo da IOS do roteador.

Para acessar o switch remotamente, é necessário configurar um protocolo de acesso remoto, como por exemplo o SSH ou Telnet.

Para acessar um outro equipamento, tem que se entrar por alguma porta(virtual) de acesso, em equipamentos CISCO damos o nome de:
 LINE VTY 015

## TELNET

 NY_SW1(config)#line vty 0 4
NY_SW1(config-line)#password cisco

NY_SW1(config-line)#transport input tel -> Permite o acesso remoto utilizando o protocolo Telnet.

## SSH

NY_SW1(config)#ip domain-name cisco.com -> Definindo dominio
NY_SW1(config)#crypto key generate rsa -> tipo RSA

NY_SW1(config)#username henrique password cisco -> SSH precisa de um usuario e senha para acessar o switch remotamente.

NY_SW1(config)#line vty 0 4

NY_SW1(config-line)#login local -> O 'login local' indica que o switch deve usar a base de dados local para autenticar os usuários que tentam acessar remotamente.

NY_SW1(config-line)#transport input ssh 

__CONEXAO NO SWITCH__

NY_R1#ssh -l henrique 192.168.10.2
          'L' USER      IP

---

# SWITCH LAYER 2 

* O switch de LAYER 2 é um dispositivo de rede que opera na camada de enlace de dados do modelo OSI. Ele é responsável por encaminhar os quadros de dados com base nos endereços MAC (Media Access Control) dos dispositivos conectados a ele.'

# SWITCH LAYER 3

* O switch de LAYER 3 é um dispositivo de rede que opera na camada de rede do modelo OSI. Ele é capaz de encaminhar pacotes de dados com base nos endereços IP, além de realizar funções de roteamento. 

---

# VLANS

show vlan brief -> Exibe as VLANs configuradas no switch, mostrando o ID da VLAN, nome, status e as portas associadas a cada VLAN.

VLAN (Virtual LAN) é uma forma de dividir um switch físico em várias redes lógicas independentes.
Dispositivos na mesma VLAN conseguem se comunicar diretamente.
Dispositivos em VLANs diferentes precisam de um roteador ou switch camada 3 para conversar.

Ela é usada para:

- separar setores,
- aumentar segurança,
- organizar a rede,
- reduzir tráfego desnecessário.

1- Criar vlan
2- Entrar na interface ou range de interface
3- Definir mode ACCESS ou TRUNK
4 - Colocar a interface na VLAN

Criando uma VLAN: 
NY_SW1(config)#vlan 
NY_SW1(config-vlan)#name RH
---
Passando interface para VLAN:
NY_SW1(config)#interface fastEthernet 0/1 ou #interface range f0/2 - 4 , f0/24
NY_SW1(config-if)#switchport access vlan 10

Access -> FINAL (COMPUTADOR, IMPRESSORA, ETC)
TRUNK -> ENTRE SWITCHES, ROTEADORES, ETC.
Conectando dois switches em uma VLAN:
Trunk é uma porta utilizada para transportar múltiplas VLANs pelo mesmo cabo entre switches, roteadores ou outros dispositivos de rede.
O DTP faz o TRUNK automaticamente entre switches.
Existem 3 tipos de DTP:
1. Dynamic Auto -> A porta fica esperando o outro switch iniciar a negociação do trunk, e se o outro switch responder, ele se torna trunk.
2. Dynamic Desirable (default) -> Envia requisições de TRUNK para o outro switch, e se o outro switch responder, ele se torna trunk.
3. No-negotiate -> Nao vai enviar e nem receber, como se fosse desabilitado.

#show interfaces gigabitEthernet 0/1 switchport -> Exibe informações sobre a porta.
#switchport mode trunk -Transforma a porta em trunk.
#switchport  trunk encapsulation dot1q -> Define o encapsulamento do trunk como dot1q, que é o mais utilizado.   


# MOSTRAR ENDEREÇO MAC

NY_SW1#show mac address-table  -> Exibe a tabela de endereços MAC do switch, mostrando quais dispositivos estão conectados a quais portas.

---

# CDP (CISCO DISCOVERTY PROTOCOL)

CDP é um protocolo proprietário da CISCO, utilizado para descobrir informações sobre os dispositivos conectados.
Funciona somente em equipamentos CISCO.

NY_SW1#show cdp neighbors 

Capability Codes: R - Router, T - Trans Bridge, B - Source Route Bridge
                  S - Switch, H - Host, I - IGMP, r - Repeater, P - Phone

Device ID    Local Intrfce   Holdtme    Capability   Platform    Port ID
NY_R1        Fas 0/24         125            R       C1900       Gig 0/0

Device ID -> Nome do dispositivo vizinho
Local Intrfce -> Interface local do switch onde o dispositivo vizinho esta conectado.
Holdtme -> Tempo que o switch vai esperar para receber uma nova mensagem CDP do dispositivo.
Capability -> Tipo do dispositivo vizinho.
Platform -> Modelo do dispositivo vizinho.
Port ID -> Interface do dispositivo vizinho onde o switch esta conectado.

NY_SW1#show cdp neighbors detail -> Exibe informações detalhadas sobre os dispositivos vizinhos, incluindo o endereço IP do dispositivo vizinho.

NY_SW1#show cdp neighbors detail | include IP -> Apenas endereço IP. Pode usar outros como apenas o nome.

---

# LLDP (LINK LAYER DISCOVERY PROTOCOL)

Praticamente um irmao gemio do CDP, porem qualquer dispositivo pode usar.

NY_SW1(config)#lldp run -> Habilita o LLDP no switch.

NY_SW1#show lldp

Global LLDP Information:
    Status: ACTIVE
    LLDP advertisements are sent every 30 seconds
    LLDP hold time advertised is 120 seconds
    LLDP interface reinitialisation delay is 2 seconds

---

# BACKUP    

Normalmente se utiliza o TFTP (Trivial File Transfer Protocol) para fazer backup de configurações de roteadores e switches, mas tambpem pode ser utilizado o FTP (File Transfer Protocol).

Formas de backup:

1. Roteador mandando o backup para um servidor TFTP ou FTP.

2. KRON JOB -> O KRON é um recurso do IOS da CISCO que permite agendar tarefas, como por exemplo, fazer backup de configurações de roteadores e switches.

3. ARCHIVE  -> VARIAS CONFIGS DE BACKUP, COM DATA E HORA, PARA VOLTAR A QUALQUER MOMENTO.

---

# CONSOLE CABLE

 Cabo utilizado para conectar a roteadores e switches.

 Possui duas extremidades:

 1. DB9 (9 pinos) - Conectada ao computador.

 2. RJ45 - Conectada ao roteador ou switch.

 Hoje em dias os laptops não possuem mais a porta DB9, então é necessário um adaptador USB 
 para DB9 para conectar o cabo ao laptop.

---

# CABOS E FIBRA

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

---

# ROTEADORES

 __PRINCIPAIS COMPONENTES TRASEIROS__

 1. GROUND CONNECTOR -> "FIO TERRA" - evita queima e retira a eletricidade estatica. 

 2. SECURITY SLOT -> UMA TRAVA PARA EVITAR ROUBO DO ROTEADOR (CADEADO POR EXEMPLO).

 3. POE(POWER OVER ETHERNET) -> PoE (Power over Ethernet) é uma tecnologia que permite enviar energia elétrica + dados pelo mesmo cabo de rede (Ethernet).

 4. GE0/0, GE0/1.. -> GIGA ETHERNET PORTS -> Portas de rede para conexao de computadores, switches, etc.

 5. AUX PORT -> Serve para configuração do dispositivo

 6. CONSOLE PORT (PORTA AZUL) -> Serve para configuração do dispositivo, utilizando o cabo console. (Utiliza-se um RJ45 ou mini usb)

 7. SLOTS -> Para colocar placas de expansão, como por exemplo placas de fibra optica.

---

# SWITCHES

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

---

# STACK-SWITCH

É um sistema que faz com que varios switches se comportem com um so.

1. STACK DATA CABLE -> Cabo utilizado para conectar os switches em um stack-switch.

2. STACK POWER CABLE -> Cabo utilizado para fornecer energia para os switches em um stack-switch.

---

# WIRELESS

ACCESS POINTS (AP) -> LIGHTWEIGHT: DEPENDEDE DE UM CONTROLADOR PARA FUNCIONAR e AUTONOMOUS: FUNCIONA DE FORMA INDEPENDENTE, SEM A NECESSIDADE DE UM CONTROLADOR.  

WIRELLESS CONTROLLER -> Controla os Access Points, gerenciando a conexao dos dispositivos sem fio e garantindo a segurança da rede sem fio.

---

# FIREWALLS

FIREWALLS -> Dispositivo de segurança de rede que monitora e controla o tráfego de entrada e saída com base em regras de segurança predefinidas. 

 - STATEFULL FIREWALL -> É possivel filtrar o tráfego, com base no IP de origem, IP de destino por exemplo.

 - STATLESS FIREWALL -> Filtra o tráfego com base em regras predefinidas.  

---

# TOPOLOGY ARCHITECTURE

1. WAN (Wide Area Network) -> É você ter a necessidade de chega a algum lugar, fazer a conexao (Ativa a todo momento) adquirindo o serviço de um provedor de internet.

2. 2tier VS 3 tier _> 2 tier: É uma topologia onde temos apenas dois níveis de hierarquia, o core e o access. 3 tier: É uma topologia onde temos três níveis de hierarquia, o core, o distribution e o access.

3. SPINER-LEAF -> É como se fosse uma arvore, onde temos um switch central (spiner) e varios switches conectados a ele (leafs). 

4. SOHO -> Small Office Home Office -> É uma topologia onde temos um pequeno escritório ou uma casa, com poucos dispositivos conectados a internet.

5. ON-PREMISE/CLOUD -> On-premise: É quando a infraestrutura de rede é mantida e gerenciada internamente pela empresa. 
Cloud: É quando a infraestrutura de rede é mantida e gerenciada por um provedor de serviços em nuvem.

---

# OSI MODEL

1. Physical Layer (Camada Física) -> Responsável pela transmissão de bits através do meio físico (cabos, fibra óptica, etc.).

2. Data Link Layer (Camada de Enlace de Dados) -> Responsável pela detecção e correção de erros na transmissão de dados, além de controlar o acesso ao meio físico.

3. Network Layer (Camada de Rede) -> Responsável pelo roteamento dos pacotes de dados entre os dispositivos na rede.

4. Transport Layer (Camada de Transporte) -> Responsável pelo controle de fluxo e pela entrega confiável dos dados entre os dispositivos.

5. Session Layer (Camada de Sessão) -> Responsável por estabelecer, gerenciar e encerrar sessões entre os dispositivos.

6. Presentation Layer (Camada de Apresentação) -> Responsável por traduzir os dados para um formato que possa ser entendido pelos aplicativos.

7. Application Layer (Camada de Aplicação) -> Responsável por fornecer serviços de rede para os aplicativos, como email, transferência de arquivos, etc.



# COMANDOS CISCO — ORDEM ALFABÉTICA

| COMANDO | FUNÇÃO |
|---|---|
| `banner motd` | Define mensagem de login |
| `clock set` | Define horário manualmente |
| `configure terminal` | Entra no modo de configuração global |
| `copy running-config startup-config` | Salva configuração |
| `crypto key generate rsa` | Gera chave RSA |
| `enable` | Entra no modo privileged |
| `enable secret cisco` | Define senha do modo privileged |
| `hostname NY_R1` | Define o nome do equipamento |
| `interface fastEthernet 0/1` | Entra na interface FastEthernet 0/1 |
| `interface gigabitethernet 0/0` | Entra na interface |
| `interface range f0/2 - 4 , f0/24` | Seleciona várias interfaces ao mesmo tempo |
| `interface vlan 1` | Entra na VLAN de gerenciamento |
| `ip add` | Define IP da VLAN |
| `ip address` | Define endereço IPv4 |
| `ip domain-name` | Define domínio |
| `ipv6 address` | Define endereço IPv6 |
| `ipv6 route` | Cria rota IPv6 |
| `ipv6 unicast-routing` | Ativa roteamento IPv6 |
| `line vty 0 4` | Configura linhas VTY |
| `lldp run` | Ativa LLDP |
| `login local` | Usa base local de autenticação |
| `name RH` | Define nome da VLAN |
| `no ntp server 2.2.2.2` | Remove servidor NTP |
| `no shutdown` | Ativa interface |
| `ntp server 2.2.2.2` | Configura servidor NTP |
| `password cisco` | Define senha do acesso remoto |
| `show cdp neighbors` | Mostra vizinhos CDP |
| `show cdp neighbors detail` | Mostra detalhes do CDP |
| `show cdp neighbors detail \| include IP` | Mostra apenas IP no CDP |
| `show clock` | Mostra o relógio do roteador |
| `show interfaces` | Mostra detalhes das interfaces |
| `show ip interface brief` | Mostra resumo das interfaces |
| `show ipv6 interface brief` | Mostra interfaces IPv6 |
| `show lldp` | Mostra informações LLDP |
| `show mac address-table` | Mostra tabela MAC |
| `show running-config` | Mostra configuração atual |
| `show vlan brief` | Mostra VLANs |
| `show interfaces <interface> switchport` | Mostra informações sobre a porta |
| `switchport  trunk encapsulation dot1q` | Define o encapsulamento do trunk como dot1q, que é o mais utilizado. |
| `switchport mode trunk` | Define o modo da interface como trunk |
| `ssh -l henrique 192.168.10.2` | Conecta via SSH |
| `switchport access vlan 10` | Coloca a interface na VLAN 10 |
| `switchport mode` | Define o modo da interface|
| `transport input ssh` | Permite acesso SSH |
| `transport input tel` | Permite acesso Telnet |
| `username henrique password cisco` | Cria usuário local |
| `vlan 10` | Cria a VLAN 10 |
| `wr` | Salva configuração rapidamente |
```

