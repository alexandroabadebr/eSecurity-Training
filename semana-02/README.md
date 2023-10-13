# Conceito de Protocolos
    - Entendendo protocolo TCP
        - Entendendo 3Way handshake
        - Iniciando sessão TCP
        - Encerrando sessão TCP
        - Confiabilidade do protocolo TCP
    - Entendendo protocolo UDP
        - Conexão UDP
    - Portas e Serviços
    - Protocolo ICMP
    - A Camada OSI

## Entendendo Protocolo TCP

O TCP (Transmission Control Protocol) é um dos principais protocolos de comunicação da Internet. Ele faz parte da suíte de protocolos TCP/IP, que é utilizada para comunicações em redes de computadores. O TCP é responsável por fornecer uma comunicação confiável, orientada à conexão e orientada a fluxo entre dispositivos em uma rede. Aqui estão os principais aspectos do TCP que você precisa entender:

### 1. **Confiabilidade:**
- O TCP é orientado a conexão e fornece uma comunicação confiável. Ele verifica se os dados são entregues corretamente no destino. Se um pacote é perdido ou corrompido durante a transmissão, o TCP solicitará a retransmissão desse pacote.

### 2. **Orientação à Conexão:**
- Antes que os dados possam ser trocados entre dois dispositivos, uma conexão TCP deve ser estabelecida usando um procedimento chamado "handshake". Esse processo de estabelecimento de conexão é conhecido como "3-way handshake".

### 3. **Orientação ao Fluxo:**
- O TCP gerencia o fluxo de dados para evitar que um dispositivo sobrecarregue o outro com dados. Ele usa um mecanismo chamado de "janela deslizante" para controlar o fluxo de dados.

### 4. **Controle de Erros e Retransmissão:**
- O TCP verifica a integridade dos dados e, se detectar erros, solicita a retransmissão dos pacotes perdidos ou corrompidos.

### 5. **Número de Sequência:**
- O TCP atribui um número de sequência a cada pacote de dados enviado. Isso é usado para garantir que os pacotes sejam recebidos na ordem correta e para detectar pacotes duplicados.

### 6. **Acknowledgment (ACK):**
- Após receber um pacote, o dispositivo receptor envia uma confirmação (ACK) de volta ao remetente para indicar que o pacote foi recebido com sucesso.

### 7. **MSS (Maximum Segment Size):**
- O TCP permite a negociação do tamanho máximo de segmento (MSS) durante o estabelecimento da conexão. Isso ajuda a otimizar a eficiência da transmissão de dados, permitindo que pacotes de tamanho apropriado sejam enviados.

### 8. **Portas:**
- O TCP usa números de porta para distinguir diferentes serviços em um mesmo dispositivo. As portas permitem que os dispositivos saibam qual aplicação deve receber os dados recebidos.

### 9. **Encerramento de Conexão:**
- Quando a comunicação é concluída, o TCP utiliza um procedimento de encerramento de conexão chamado "4-way handshake" para encerrar a conexão de forma segura.

Em resumo, o TCP é fundamental para a comunicação confiável na Internet. Ele oferece um mecanismo robusto para a transmissão de dados, garantindo que os dados sejam entregues de forma ordenada, sem erros e de maneira eficiente entre dispositivos em uma rede.

## Entendendo 3Way Handshake

![Screenshot from 2023-10-13 17-24-27](https://github.com/alexandroabadebr/eSecurity-Training/assets/5865711/16d252bb-96c6-4a92-9f7d-0a320561f643)

O "3-way handshake" (aperto de mão de três vias) é um procedimento usado em protocolos de comunicação da Internet para estabelecer uma conexão TCP (Transmission Control Protocol) entre dois dispositivos, geralmente um cliente e um servidor. Esse processo de três etapas é fundamental para garantir uma conexão confiável e bidirecional. Vou explicar cada etapa do 3-way handshake:

### 1. **SYN (Synchronize) - Etapa 1:**
- O cliente envia um pacote TCP com a flag SYN ativada para o servidor.
- O pacote contém o número de sequência inicial (ISN - Initial Sequence Number) escolhido pelo cliente para essa conexão.
- A flag SYN indica que o cliente deseja estabelecer uma conexão.

### 2. **SYN-ACK (Synchronize-Acknowledge) - Etapa 2:**
- O servidor recebe o pacote SYN do cliente.
- O servidor responde com um pacote TCP que tem as flags SYN e ACK ativadas.
- A flag SYN indica que o servidor também deseja estabelecer uma conexão, e a flag ACK confirma que ele recebeu o pacote SYN do cliente.
- O servidor também escolhe um número de sequência inicial (ISN) para a conexão do seu lado.

### 3. **ACK (Acknowledge) - Etapa 3:**
- O cliente recebe o pacote SYN-ACK do servidor.
- O cliente então envia um pacote TCP de volta para o servidor com a flag ACK ativada.
- A flag ACK indica que o cliente recebeu o pacote SYN-ACK do servidor.
- A partir deste ponto, a conexão está estabelecida e ambos os lados podem enviar dados de forma confiável, pois ambas as partes confirmaram a intenção de estabelecer a conexão.

Após o 3-way handshake, a conexão está estabelecida e ambos os lados podem começar a trocar dados. Quando a comunicação é concluída, a conexão é encerrada usando um procedimento semelhante chamado "4-way handshake" para desconectar a conexão de forma segura.

Em resumo, o 3-way handshake é uma série de três etapas (SYN, SYN-ACK, ACK) que permite a dois dispositivos estabelecerem uma conexão TCP de maneira confiável e bidirecional. Esse procedimento é uma parte fundamental do protocolo TCP e é essencial para garantir uma comunicação estável e segura na Internet.

## Entendendo Protocolo UDP

![Screenshot from 2023-10-13 17-37-09](https://github.com/alexandroabadebr/eSecurity-Training/assets/5865711/b51e33ea-d967-44a8-9206-46cf5fe7f25e)


O UDP (User Datagram Protocol) é um protocolo de comunicação da camada de transporte, que faz parte da suíte de protocolos de internet (TCP/IP). Ao contrário do TCP, o UDP é um protocolo sem conexão e não orientado a fluxo. Isso significa que ele não estabelece uma conexão antes de enviar dados e não verifica se os dados são recebidos corretamente pelo destinatário.

Aqui estão algumas características e conceitos-chave relacionados ao UDP:

### **1. Sem Conexão:**
- O UDP não estabelece uma conexão antes de enviar dados. Ele simplesmente envia pacotes (datagramas) para o destinatário sem qualquer procedimento de handshake.

### **2. Sem Controle de Fluxo ou Correção de Erros:**
- O UDP não oferece controle de fluxo para garantir que o remetente não sobrecarregue o receptor com dados. Além disso, não há mecanismo de retransmissão para lidar com pacotes perdidos ou corrompidos.

### **3. Velocidade e Eficiência:**
- Por não ter a sobrecarga de controle de erros, confirmações de recebimento e retransmissões, o UDP é mais rápido e eficiente em termos de largura de banda do que o TCP. É adequado para aplicações onde a velocidade é mais importante do que a confiabilidade, como em transmissões de vídeo ao vivo e jogos online.

### **4. Aplicações do Protocolo UDP:**
- O UDP é frequentemente utilizado em aplicações em tempo real, como streaming de mídia, VoIP (Voice over IP), videoconferência e jogos online. Nessas situações, a latência é mais crítica do que garantir a entrega de todos os pacotes.

### **5. Estrutura de Pacotes:**
- Cada pacote UDP, chamado de datagrama, possui um cabeçalho curto que contém informações básicas, incluindo portas de origem e destino, comprimento e um campo de verificação de integridade.

### **6. Sem Garantia de Entrega:**
- Como o UDP não confirma a entrega ou a ordem dos pacotes, é responsabilidade da aplicação implementar esses mecanismos, se necessário.

### **7. Limitações do UDP:**
- Devido à sua natureza não confiável, o UDP pode não ser adequado para todas as aplicações. Se a integridade e a ordem dos dados são críticas, o TCP é uma escolha melhor, mesmo que isso signifique uma sobrecarga de desempenho.

Em resumo, o UDP é um protocolo de transporte rápido e eficiente, mas não confiável, que é adequado para aplicações em tempo real onde a latência é mais importante do que a integridade dos dados. Ele é frequentemente usado em situações onde a perda ocasional de pacotes é aceitável, como em transmissões de vídeo ao vivo e comunicações de voz.

ICMP (Internet Control Message Protocol) é um protocolo da camada de rede da suíte de protocolos TCP/IP. Ele é usado principalmente para enviar mensagens de erro e informações operacionais sobre a comunicação de dados em uma rede IP. O ICMP é fundamental para o funcionamento da Internet, sendo usado para diagnosticar problemas de rede, enviar mensagens de erro e gerenciar o tráfego de rede. Aqui estão os principais aspectos do ICMP que você precisa entender:

## Entendendo o protocolo ICMP

### 1. **Mensagens de Erro:**
- ICMP é usado para enviar mensagens de erro, como quando um pacote não pode ser entregue ao destino, quando um host ou roteador está inacessível ou quando um tempo limite de pacote é excedido.

### 2. **Ping:**
- O comando `ping` é uma aplicação comum que usa o ICMP para testar a conectividade entre dois dispositivos. Ele envia mensagens de ICMP Echo Request e aguarda por respostas Echo Reply. Isso é usado para verificar se um host está acessível na rede.

### 3. **Traceroute:**
- A ferramenta `traceroute` também utiliza o ICMP para rastrear a rota que um pacote leva de um dispositivo para outro. Ela envia pacotes ICMP com incrementos de TTL (Time to Live) para determinar os roteadores ao longo do caminho até o destino.

### 4. **Tipos de Mensagens ICMP:**
- Existem vários tipos de mensagens ICMP, incluindo Echo Request/Reply (usados no `ping`), Destination Unreachable (indicando que um host ou rota não está disponível), Time Exceeded (indicando que o tempo limite do pacote foi excedido) e Redirect (indicando que um roteador forneceu uma rota melhor).

### 5. **Controle de Congestionamento:**
- O ICMP é usado por roteadores para notificar os hosts sobre condições de congestionamento na rede. Isso ajuda os hosts a ajustar a taxa de envio de pacotes para evitar sobrecarregar a rede.

### 6. **Encapsulamento:**
- As mensagens ICMP são encapsuladas em datagramas IP para serem transmitidas pela rede.

### 7. **Firewalls e ICMP:**
- Alguns firewalls podem filtrar ou bloquear mensagens ICMP como uma medida de segurança para proteger a rede contra ataques.

### 8. **Importância para a Rede:**
- ICMP é essencial para o diagnóstico de problemas de rede, ajudando a identificar falhas de conectividade, roteamento ou congestionamento.

Em resumo, o ICMP é um protocolo fundamental para a comunicação e diagnóstico de rede. Ele fornece uma maneira para os dispositivos em uma rede se comunicarem sobre condições operacionais e erros, desempenhando um papel vital na operação e na solução de problemas em redes IP.

## A camda OSI


![Screenshot from 2023-10-13 18-03-30](https://github.com/alexandroabadebr/eSecurity-Training/assets/5865711/a7ac5b96-6a03-440a-b5e7-01b7ef4ddea0)
O modelo OSI (Open Systems Interconnection) é um modelo conceitual que padroniza as funções de uma rede ou sistema de computadores em sete camadas, permitindo que diferentes sistemas de computadores se comuniquem através de uma rede. Cada camada do modelo OSI tem um papel específico e oferece serviços para as camadas acima e abaixo dela. Aqui estão as sete camadas do modelo OSI, do mais alto ao mais baixo nível:

### 1. **Camada de Aplicação (Application Layer):**
- Esta é a camada com a qual os usuários interagem diretamente. Ela fornece serviços de rede para aplicativos de software, permitindo que eles comuniquem-se com a rede. Protocolos nesta camada incluem HTTP, FTP, SMTP, e POP3.

### 2. **Camada de Apresentação (Presentation Layer):**
- A camada de apresentação é responsável pela tradução, compressão e criptografia dos dados. Ela garante que a informação seja compreendida pelo receptor. Também é responsável por formatos de dados e codificação, como o SSL/TLS para segurança.

### 3. **Camada de Sessão (Session Layer):**
- Esta camada estabelece, mantém e finaliza sessões entre aplicativos em diferentes dispositivos. Ela gerencia o estabelecimento, manutenção e término de conexões, garantindo que os dados sejam entregues corretamente.

### 4. **Camada de Transporte (Transport Layer):**
- A camada de transporte é responsável pela entrega de dados de forma confiável e ordenada, além de controlar o fluxo de dados. Ela também lida com correção de erros e retransmissão de pacotes perdidos. Protocolos comuns nesta camada incluem TCP (Transmission Control Protocol) e UDP (User Datagram Protocol).

### 5. **Camada de Rede (Network Layer):**
- A camada de rede é responsável pelo roteamento dos dados através da rede. Ela lida com o encaminhamento dos pacotes de origem para destino, independente da topologia da rede. O protocolo IP (Internet Protocol) opera nesta camada.

### 6. **Camada de Enlace de Dados (Data Link Layer):**
- Esta camada é responsável pela comunicação entre dispositivos na mesma rede local. Ela lida com o acesso ao meio físico e a detecção de erros, garantindo que os pacotes sejam entregues apenas aos dispositivos de destino corretos. Protocolos nesta camada incluem Ethernet, Wi-Fi e PPP.

### 7. **Camada Física (Physical Layer):**
- A camada física lida com a transmissão e recepção de dados sobre um meio físico, como cabos de cobre, fibra óptica ou ondas de rádio. Ela define as características elétricas, mecânicas e funcionais do meio de transmissão.

O modelo OSI é útil para entender como diferentes partes de uma rede interagem entre si, facilitando o desenvolvimento, implementação e solução de problemas em redes de computadores. Cada camada tem uma função específica e independente, mas trabalha em conjunto para garantir a comunicação eficaz dos dados através de uma rede.
