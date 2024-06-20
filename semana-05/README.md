# Apresentação: Nmap + NSE

+ Metasploitable
  - O que é o metasploitable
  - Configurando um ambiente para ataques
+ Varreduras Intrusivas
  - Conhecendo o Nmap
    - O que é o NSE
    - Conhecendo grupos de scripts
    - Valores booleanos na execução
  - Colocando em prática

## Criando uma máquina para testes
![Screenshot from 2023-11-22 14-25-43](https://github.com/alexandroabadebr/eSecurity-Training/assets/5865711/ad5c991a-3c15-4f98-a8c3-87a7c1371da6)

## Varreduras Intrusivas: Nmap

Desenvolvida pela equipe do Metasploit a máquina virtual Metasploitable foi feita
intencionalmente vulnerável para todos os tipos imagináveis de falhas de
segurança poderem ser explorados, incentivando assim os estudos e ajudando na
obtenção de novos conhecimentos para pentesters iniciantes.

Metasploitable pode ser usada em treinamentos de cursos acadêmicos ou
particulares, e é compatível com VMWare, VirtualBox ou VMFusion. O login e
senha padrão é msfadmin.


Os scripts disponibilizados pelo NSE são classificados quanto às categorias e ao
tipo. As categorias dizem respeito à natureza da funcionalidade desempenhada e
os tipos e a fase da varredura em que devem ser executados, isto é, as categorias
classificam os scripts pelo que eles fazem e os tipos, pelo momento em que o
mesmos são executados durante uma varredura.

A listagem abaixo descreve cada categoria:

• auth → Relacionados à mecanismos de autenticação e credenciais de acesso;
• broadcast → Fazem descoberta de hosts não listados como alvos através do
envio de pacotes broadcast;
• brute → Visam descobrir credenciais de acesso através de ataques de
dicionário;
• default → É a categoria padrão, em que os scripts devem fornecer respostas
rápidas, concisas e confiáveis, além de serem pouco intrusivos, de fornecerem
informações úteis para a maior parte dos usuários e de não estressarem o alvo a
ponto de ser detectado por seus administradores como um ataque;

# Conhecendo o Nmap
## Varreduras Intrusivas: Nmap

Os scripts são desenvolvidos por meio de uma linguagem de script chamada LUA, e foi criada por alunos da PUC do Rio  de Janeiro.

• discovery → Visam descobrir ativamente mais informações sobre o alvo;
• dos → Tentam causar indisponibilidade do alvo, ao provocar erros no lado do servidor;
• exploit → Exploram uma dada vulnerabilidade conhecida;
• external → Fazem consultas legítimas a recursos de terceiros, não listados como alvos;
• fuzzer → Enviam pacotes contendo aleatórios ou inesperados pela aplicação servidor
visando descobrir bugs e vulnerabilidades;
• intrusive →: Representam considerável risco de provocar erros no lado do servidor, utilizar
uma quantidade significativa de recursos ou estressar o alvo a ponto de ser detectado por
seus administradores como um ataque;
• malware → Detectam remotamente se o alvo está infectado com um dado malware;
• safe → Representam pouco risco e não devem causar erros no lado do servidor, utilizar
muitos recursos ou explorar brechas de segurança;
• version → Estendem a funcionalidade de detecção de versão do Nmap;
• vuln → Verificam se há uma dada vulnerabilidade conhecida no alvo.

# Nmap - Script Engine

Encontrar vulnerabilidades nas máquinas da rede
nmap –sS –script “(vulns)” 192.168.2.0/24
Observações:
É possível utilizar o * (asterisco) para varreduras, exemplo:

--script “http*” exceto os que estão nas caterigorias DOS, Exploit e Brute Force

Você também pode adicionar parâmetros em seus scripts, exemplo:
--script-args=‘usuario=‘’teste’,’senha=’’teste123’
--script-args-file=senhas.txt

É possível chama-los por categorias, exemplo:
--script “(broadcast or external or version)”

E também remover categorias são poderão ser usadas por varreduras padrão,
exemplo:

--script “(broadcast or external or version) and not (auth or brute)”

Exemplo de varredura em busca de falhas de segurança:
nmap –script smb-check-vulns.nse –script-args=unsafe=1 192.168.2.0/24

Checa as vulnerabilidades do serviço SMB na rede

# Nmap - Script Engine - Exemplos

Acompanhe alguns exemplos práticos
Buscar métodos HTTP de um determinado alvo:

nmap --script "http-methods" scanme.nmap.org

Buscar por Zona de transferência de DNS e Whois:
nmap --script "dns-zone-transfer,whois" scanme.nmap.org

Utilizar todos os scripts não intrusivos nos serviços HTTP e SSH:
nmap --script "http-* or ssh-* and not intrusive" scanme.nmap.org
