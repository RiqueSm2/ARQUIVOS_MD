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