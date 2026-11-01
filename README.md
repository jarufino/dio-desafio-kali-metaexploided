# dio-desafio-kali-metaexploided
Desafio de simulação de invasão em 2 máquinas virtuais (com Kali Linux a invasora, MetaExploided a vítima)

1 - Criação de WordLists (usuário e senha):
mkdir -p ~/lab-medusa/wordlists
echo -e "root\nmsfadmin\nuser\nadmin" > ~/lab-medusa/wordlists/usuarios.txt
echo -e "password\nmsfadmin\n123456\nroot\nadmin" > ~/lab-medusa/wordlists/senhas.txt


2 - Ataque simulado via ftp

medusa -h 192.168.56.4 -U ~/lab-medusa/wordlists/usuarios.txt -P ~/lab-medusa/wordlists/senhas.txt -M ftp -t 4

O comando acima serve para rodar um ataque de força bruta usando a ferramenta Medusa. Ele diz para o programa tentar adivinhar o usuário e a senha do serviço de FTP que está rodando na máquina vítima.

Destrinchando os parâmetros:

medusa: É a ferramenta de força bruta paralela que você está usando.

-h 192.168.56.4: Indica o endereço IP do alvo (host), que é a sua máquina Metasploitable 2.

-U ~/lab-medusa/wordlists/usuarios.txt: Aponta para o arquivo de texto contendo a lista de nomes de usuários que serão testados.

-P ~/lab-medusa/wordlists/senhas.txt: Aponta para o arquivo de texto contendo a lista de senhas que serão testadas.

-M ftp: Define o módulo de serviço que vai ser atacado, neste caso, o FTP (porta 21).

-t 4: Configura o número de threads paralelas (quantas tentativas simultâneas o programa vai fazer por vez para ir mais rápido).



3 - Ataque server SAMBA

medusa -h 192.168.56.4 -u msfadmin -P ~/lab-medusa/wordlists/senhas.txt -M smbnt -t 2

Esse comando serve para testar várias senhas contra um usuário específico usando o serviço SMB (Samba/compartilhamento de arquivos) da máquina vítima. É uma variação usada para testar se uma conta específica aceita alguma senha da lista.

Explicando cada parte:

medusa: É a ferramenta de força bruta que está sendo executada.

-h 192.168.56.4: Define o endereço IP da máquina alvo (host).

-u msfadmin: Informa um único nome de usuário fixo que vai ser testado (diferente do -U maiúsculo, que carrega uma lista inteira de usuários).

-P ~/lab-medusa/wordlists/senhas.txt: Aponta para o arquivo de texto contendo a lista de senhas que serão testadas contra esse usuário.

-M smbnt: Escolhe o módulo de ataque voltado para o protocolo SMB (com autenticação NT).

-t 2: Define o número de tentativas simultâneas (threads) para pegar leve no processamento e evitar derrubar o serviço muito rápido.
