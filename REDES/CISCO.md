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

# LLDP (LINK LAYER DISCOVERY PROTOCOL)
Praticamente um irmao gemio do CDP, porem qualquer dispositivo pode usar.

NY_SW1(config)#lldp run -> Habilita o LLDP no switch.


NY_SW1#show lldp

Global LLDP Information:
    Status: ACTIVE
    LLDP advertisements are sent every 30 seconds
    LLDP hold time advertised is 120 seconds
    LLDP interface reinitialisation delay is 2 seconds

# BACKUP    
Normalmente se utiliza o TFTP (Trivial File Transfer Protocol) para fazer backup de configurações de roteadores e switches, mas tambpem pode ser utilizado o FTP (File Transfer Protocol).

Formas de backup:
1. Roteador mandando o backup para um servidor TFTP ou FTP.
2. KRON JOB -> O KRON é um recurso do IOS da CISCO que permite agendar tarefas, como por exemplo, fazer backup de configurações de roteadores e switches.
3. ARCHIVE  -> VARIAS CONFIGS DE BACKUP, COM DATA E HORA, PARA VOLTAR A QUALQUER MOMENTO.
