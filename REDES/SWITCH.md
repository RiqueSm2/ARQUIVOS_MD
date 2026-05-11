Configurações basicas é o mesmo do ROTEADOR

* IP PARA GERENCIAMENTO
Em switches de LAYER2, é necessário configurar um IP para gerenciar o switch remotamente.
A interface VLAN, em switchers de LAYER2, é a interface normalmente utilizada para gerenciamento.
NY_SW1(config)#interface vlan 1
NY_SW1(config-if)#ip add 192.168.10.2 255.255.255.0

* CONEXAO REMOTA 
A conexao entre aparelhos ela pode ser feita remotamente, utilizando TELNET ou SSH, 
que acessam diretamente uma porta virtual, que é chamada de LINE VTY.
Dentro dessa LINE VTY, existem varias sessões que vao de 0 a 15 ou ate mais dependendo da IOS do roteador.

Para acessar o switch remotamente, é necessário configurar um protocolo de acesso remoto, como por exemplo o SSH ou Telnet.

Para acessar um outro equipamento, tem que se entrar por alguma porta(virtual) de acesso, em equipamentos CISCO damos o nome de:
 LINE VTY 015

1. TELNET


 NY_SW1(config)#line vty 0 4
NY_SW1(config-line)#password cisco

NY_SW1(config-line)#transport input tel -> Permite o acesso remoto utilizando o protocolo Telnet.

2. SSH
NY_SW1(config)#ip domain-name cisco.com -> Definindo dominio
NY_SW1(config)#crypto key generate rsa -> tipo RSA

NY_SW1(config)#username henrique password cisco -> SSH precisa de um usuario e senha para acessar o switch remotamente.

NY_SW1(config)#line vty 0 4

NY_SW1(config-line)#login local -> O 'login local' indica que o switch deve usar a base de dados local para autenticar os usuários que tentam acessar remotamente.

NY_SW1(config-line)#transport input ssh 

__CONEXAO NO SWITCH__

NY_R1#ssh -l henrique 192.168.10.2
          'L' USER      IP

# SWITCH LAYER 2 
* O switch de LAYER 2 é um dispositivo de rede que opera na camada de enlace de dados do modelo OSI. Ele é responsável por encaminhar os quadros de dados com base nos endereços MAC (Media Access Control) dos dispositivos conectados a ele.'

# SWITCH LAYER 3
* O switch de LAYER 3 é um dispositivo de rede que opera na camada de rede do modelo OSI. Ele é capaz de encaminhar pacotes de dados com base nos endereços IP, além de realizar funções de roteamento. 

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