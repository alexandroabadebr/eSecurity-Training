# Google Hacking

## Verreduras

Há 3 tipos de varreduras que podemos utilizar em nosso ambiente para detectar possíveis ataques.

+ Verreduras Passivas
    - As varreduras passivas, buscam outros métodos de coletar dados do alvo, sendo assim, tornando-se indetectáveis, porém, não tão específicos como as verreduras ativas.
+ Varreduras Ativas
    - Quando realizamos varreduras ativas, vamos direto ao alvo, com o objetivo de coletar dados precisos sobre o ambiente atual. Essa técnica é de difícil detecção pelo Firewalls/IDS/WAFs e afins.
+ Varreduras Furtivas 
    - Varreduras furtivas tem o objetivo de utilizar técnicas das varreduras ativas, porém, com a menor probabilidade de detecção.Efetuando evasões de Sistemas de detecção e confundindo os administradores de uma rede.

## Google Hacking: Entendendo
O Google hacking envolve o uso de operadores avançados no Google, motor de
busca para localizar sequências específicas de texto dentro de resultados de
pesquisa. Alguns dos exemplos mais populares são, encontrar versões específicas
de grupos vulneráveis em aplicações web.

Exemplos:
> “filetype:“ - faz uma busca em determinadas extensões de arquivos.
> Ex.: “senhas filetype:txt"

Irá buscar todos os arquivos .txt que possui palavras senhas dentro dele.
> "allinurl:" - faz uma busca por endereços de url que contem palavras especificas.
> Ex.: "allinurl:contato.asp“

Busca todos os sites contendo "contato.asp" na url.
> “inurl:” – Busca determinadas palavras dentro de um domínio

> Ex.: senhas “inurl:esecurity.com.br”
> Irá efetuar uma busca da palavra senha no dominio esecurity.com.br

> “-“ – Remove palavras ou dados que não devem ser apresentados
> Ex.: “justin -bieber"

Irá buscar todas as páginas que possuem algo relacionado a qualquer Justin, desde
que não possua nenhuma palavra que remete à Bieber, no caso, Justin Bieber não
deve aparecer (Graças a Deus)  

> “+" – Força o aparecimento de palavras ou dados que devem ser apresentados.
> Ex.: “academia +hacker“

Irá efetuar a busca em todos os sites que possui a palavra academia onde na mesma
página também encontra-se a palavra hacker.  

>“OR” – Dados booleanos, você pode optar por aparecer um ou outro. Também pode
> substituir o OR por |

> Ex.: Vodka OR Água de Côco
Irá efetuar uma busca da palavra Vodka ou a frase Água de côco

> “AND” – Você pode optar por buscar por 2 ou mais dados simultâneos.

> Ex.: Alan AND Sanches AND Security
Irá efetuar uma busca da palavra Alan Sanches e Security, caso a página não tenha
essas 3 informações, não será listada.

## Google Hacking

Exemplos de uso como ferramenta hacking:
> "allinurl:usuarios.mdb site:.com.br"
Busca por arquivos de banco de dados nomeados "usuarios.mdb" dentro do
> dominio mae ".com.br"

> "allintitle:admin panel site:.org"
Busca por supostas paginas de administracao dentro do dominio ".org"
> "allinurl:login.asp"
Lista todas as paginas com nome de "login.asp", e em alguns casos o google
exibira uma versão "cache" da pagina onde será possível ver o codigo asp.

Buscando arquivos de anotações de senha:
intitle:”index of /” senhas.txt
inurl:admin intext:username= AND email= AND password OR pass=
filetype:xls + senha + com.br
filetype:txt intext:senha

Alvo interessante: http://static.tumblr.com/eeczvca/Bi9m1gu4l/my_senhas.txt
Invadindo PhpMyAdmin sem senha
> inurl:”phpmyadmin/index.php” intext:”[ Edit ] [ Create PHP Code ] [ Refresh ]”

Buscando backup de configurações de CMSs
> intext:"~~Joomla1.txt" title:"Index of /"

Alvo interessante: http://tiagofeitosa.com/cb/
> configuration.php_ “<?php class Jconfig {“
> inurl:wp-config.old
> inurl:"configuration.php.old" class JConfig
> inurl:configuration.php.bkp

Alvo interessante: http://www.philippinedirect.com/configuration.php.bkp

Invadindo impressora remota
> intitle:”Web Image Monitor” & inurl:”/mainframe.cgi”

Buscando câmeras disponíveis na internet:
> inurl:LvAppl intitle:liveapplet
> intitle:"Live View - AXIS 211"
> inurl:"viewerframe?mode=motion“
> inurl:”/control/userimage.html”

Buscando por arquivos de VPN
> !HOST=*.* intext:enc_UserPassword=* ext:pcf

## Apresentação: Varredura com Maltego

+ Varredura passiva com Maltego
    - O que é o Maltego
    - Tipos de licenças
    - Maltego vs Casefile
    - Definições Transforms x TDS
    - Edição Community vs Comercial
    - Colocando em Prática
        - Identificando DNS Servers
        - Identificando E-mails
        - Identificando MX Servers
        - Identificando IPs

## Conhecendo o NMAP

Nmap é um software livre que realiza port scan desenvolvido pelo Gordon Lyon,
autoproclamado hacker "Fyodor". É muito utilizado para avaliar a segurança dos
computadores, e para descobrir serviços ou servidores em uma rede de
computadores. É conhecido pela sua rapidez e pelas opções que dispõe.

O Nmap é um programa CUI (Console User Interface), pelo que corre na linha de
comandos, mas este tem uma interface gráfica (GUI), o NmapFE (Nmap Front
End), que foi substituido pelo Zenmap em 11 de Outubro de 2007, por ser uma
versão portátil e prover uma interface melhor para execução e especialmente para
visualização e análise dos resultados do Nmap.


## Principais comandos NMAP:

### -p
Você pode determinar que uma porta ou sequencia de portas seja varrida, sendo
assim, ele não executa a varredura apenas em portas baixas:
> Nmap –p 22 192.168.1.1
> Nmap –p 22-90 192.168.1.0/24
> Nmap –p 22,55,90 192.168.1.1

### -g
Define a porta de origem. Como sabemos, geralmente as portas de origem são
portas altas (acima de 1024).
Com o Nmap, podemos dizer que a requisição ou o Scan está partindo de uma

porta baixa:
> Nmap –g 53 192.168.1.1
> Nmap –g 22 192.168.1.0/24


#### -sP
Ping scan: Algumas vezes é necessário saber se um determinado host ou rede está
no ar. Nmap pode enviar pacotes ICMP “echo request” para verificar se
determinado host ou rede está ativa. Hoje em dia, existem muitos filtros que
rejeitam os pacotes ICMP “echo request”, então envia um pacote TCP ACK para a
porta 80 (default) e caso receba RST o alvo está ativo. A terceira técnica envia um
pacote SYN e espera um RST ou SYN-ACK.

> Nmap –sP 192.168.1.254
> Nmap –sP 192.168.1.0/24

#### -sV
Version detection: Após as portas TCP e/ou UDP serem descobertas por algum dos
métodos, o nmap irá determinar qual o serviço está rodando atualmente. O arquivo
nmap-service-probes é utilizado para determinar tipos de protocolos, nome da
aplicação, número da versão e outros detalhes

> Nmap –sV 192.168.1.254

#### -sR
RCP scan: Este método trabalha em conjunto com várias técnicas do Nmap. Ele
considera todas as portas TCP e UDP abertas e envia comandos NULL
SunRPC,para determinar se realmente são portas RPC. É como se o comando
“rpcinfo -p” estivesse sendo utilizado, mesmo através de um firewall (ou protegidopor TCPwrappers).

#### -sn
Ping Scan: Durante o Scan, o Nmap verifica o status da porta, porém, com a opção
–sn ele verifica apenas se a máquina está viva, sem efetuar scan de portas.

> Nmap –sn 192.168.1.254
> Nmap –sn 192.168.1.0/24

#### -sL
List Scan: Com esta opção o Nmap verifica quantos IPs ele irá verificar. Com esta
opção ele não varre as máquinas, mas te retorna uma lista de IPs que podem ser
varridos em uma determinada rede.
Nmap –sL 192.168.1.0/24

#### -O
OS detection: É possível descobrir qual o sistema operacional da vítima, ou chegar
o mais próximo possível.

> Nmap –O 192.168.1.254
> Nmap –O 192.168.1.0/24
> Nmap –sR 192.168.1.254
> Nmap –sR 192.168.1.0/24

#### -sS
TCP SYN scan: Técnica também conhecida como “half-open”, pois não abre uma
conexão TCP completa. É enviado um pacote SYN, como se ele fosse uma
conexão real e aguarda uma resposta. Caso um pacote SYN-ACK seja recebido,
aporta está aberta, enquanto um como resposta indica que a porta está fechada. A
vantagem dessa abordagem é que poucos irão detectar esse scanning de portas.

> Nmap –sS 192.168.1.254
> Nmap –sS 192.168.1.0/24

#### --A
Advanced: O Nmap efetua todas as varreduras possíveis para trazer o máximo de
informações sobre o alvo, sendo assim, todas as informações possíveis.

> Nmap –A 192.168.1.254
> Nmap –A 192.168.1.0/24

#### -n
Nunca Resolver DNS: Ao efetuar a varredura em determinadas máquinas, ele não
efetua a resolução de DNS.

> Nmap –n 192.168.1.254
> Nmap –n 192.168.1.0/24

#### -R
Sempre resolver DNS: Com esta opção, ele sempre tentará resolver DNS, ou seja,
ele sempre tentará descobrir o hostname do alvo baseado em consulta DNS.

> Nmap –R 192.168.1.254
> Nmap –R 192.168.1.0/24
