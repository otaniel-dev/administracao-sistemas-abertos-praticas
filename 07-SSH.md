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


# Configurando Chave de Acesso:

