# Introdução ao SSH:

 SSH (Secure Shell) é um protocolo que por padrão é acessado pela porta 22, utilizado para acessar e administrar computadores remotamente de forma segura, criando uma conexão criptografada entre o cliente e o servidor, permitindo que você execute comandos, transfira arquivos e gerencie sistemas mesmo sem ter acesso físico à máquina servidora.

Inclusive, diferente do Telnet, o SSH garante integridade e autenticação, evitando interceptações por WireShark por exemplo. 
Considerando a sua segurança, o SSH é muito usado em servidores Linux, infraestrutura em nuvem, bem como em redes corporativas, eis ai a importância desse conhecimento para nós, técnicos em Redes de Computadores. 


# Retornando acesso à Internet:
Para que consigamos instalar o SSH nas máquinas, iremos retornar as configurações do adaptador de rede para NAT e remover o IP setado inicialmente. Para isso iremos: 
 - Desligar os servidores;
 - Setar as placas de rede como NAT:

<img width="780" height="488" alt="image" src="https://github.com/user-attachments/assets/b9c2e17d-c5a6-4200-ab06-cc70f71eede7" />

- Configurar a rede para receber IP por meio do DHCP, deixar o DNS como automático e salvar as configurações:

<img width="1277" height="793" alt="image" src="https://github.com/user-attachments/assets/d78aae6c-a260-4c91-8839-3c586ff5e58e" />

- Desligue e ligue a rede para pegar o IP distribuido pelo DHCP.


# Instalando SSH:
Considerando que a máquina neste ponto já se encontra com acesso a internet, o que pode ser confirmado com uma tentativa de ping para o DNS do Google [8.8.8.8]:

<img width="733" height="263" alt="image" src="https://github.com/user-attachments/assets/c732d6e7-cece-49fc-b40e-9df393e99af7" />

Para a instalação do SSH utilizaremos o seguinte comando:
```
sudo apt install openssh-server -y
```
Replique o mesmo comando no Servidor 2.

Concluída a instalação, iremos retornar as configurações de rede iniciais:
- Desligar as máquinas;
- Retornar o modo Rede Interna das nossas placas de rede;
- Ligar as máquinas;
- Retornar os IP como inicialmente.

Após concluir os passos acima, segue o registro das configurações de rede de ambos os Servidores:

Servidor 1:

<img width="757" height="145" alt="image" src="https://github.com/user-attachments/assets/2cd87187-d56f-497f-8abd-28cee6b83bd0" />

Servidor 2:

<img width="742" height="142" alt="image" src="https://github.com/user-attachments/assets/22747b9a-328b-4639-b825-decf93790dfa" />

Neste ponto, para utilizarmos o protcolo SSH para acessar o segundo servidor por meio do primeiro, o comando a ser digitado no terminal do segundo servidor é o seguinte:
```
ssh 192.168.0.99
```
Será solicitada a confirmação de que você quer realmente se conectar ao Servidor 1 e em seguida será solicitada a senha do Servidor 1. Após se autenticar, podemos verificar por meio do IP, que estamos acessando o Servidor 1 por meio do terminal como no registro a seguir:

<img width="1179" height="747" alt="image" src="https://github.com/user-attachments/assets/28337709-a011-4e7b-bd41-45522ecb0dac" />




# Configurando Chave de Acesso:

