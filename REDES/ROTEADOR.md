Com '?' lista todos os comandos presentes naquele modulo
* MODES
ROUTER> - USER MODE
ROUTER# - PRIVILEGED MODE (ROOT)
ROUTER(config)# - CONFIGURATION MODE
ROUTER(config-if)# - INTERFACE CONFIGURATION MODE

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

## IPV6
NY_R1#show ipv6 interface brief - > Exibe interfaces IPV6 e seus endereços.

DEFININDO O ENDEREÇO IPV6
NY_R1(config)#interface gigabitEthernet 0/0
NY_R1(config-if)#ipv6 address 2001:0db8:3c4d:0015:0000:0000:1a2f:1a2b/64

## IPV6 UNICAST
Ativando UNICAST
IPV6 UNICAST ROUTING
IPV6 ROUTE  <IPV6 DESTINO> <PREFIXO> <IPV6 PROXIMO SALTO OU INTERFACE DE SAIDA>

# MOSTRAR ENDEREÇO MAC
NY_SW1#show mac address-table  -> Exibe a tabela de endereços MAC do switch, mostrando quais dispositivos estão conectados a quais portas.