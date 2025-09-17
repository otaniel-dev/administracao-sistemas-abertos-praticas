# Atualização da lista de pacotes disponíveis para o sistema:

A atualização dos pacotes disponíveis é importante para que ao solicitar a instalação de um programa, o sistema consiga localizar o pacote para iniciar a instalação. Caso a atualização da lista de pacotes não seja realizada, o sistema retornará a informação de que não conseguiu encontrar o pacote para instalação.

* Para a atualização da lista de pacotes, iremos usar o comando:
```bat
sudo apt update
```

Segue um exemplo:
<img width="943" height="314" alt="image" src="https://github.com/user-attachments/assets/797c75b1-245f-4356-ade4-618234f82b49" />
<br>

# Instalação do Apache2:

O Apache2 é uma aplicação que possibilita a utilização de um computador como servidor HTTP, respondendo requisições de navegadores e disponibilizando páginas web e arquivos na internet. Para nossa prática a utilização do Apache2 tem o cunho inicial de hospedarmos uma página estática em HTML para ser acessada no navegador de nossa preferência.

* Para a instalação do Apache2, utilizaremos o comando:
```bat
sudo apt install apache2
```
Durante o processo de instalação uma permissão será solicitada, para que a instalação padrão seja realizada, confirme com **'S'** ou **'Y'** de acordo com a linguagem do seu sistema operacional. 
<br>

Como dito anteriormente, o Apache2 funcionará como um servidor HTTP, sendo assim, precisamos verificar se o servidor está ativo depois de instalado.
* Para verificar o status do servidor HTTP utilizamos o comando:
```bat
/etc/init.d/apache2 status
```
Onde obteremos o seguinte registro quando o servidor está funcionando:
<img width="1201" height="347" alt="image" src="https://github.com/user-attachments/assets/42cdd449-429a-4ced-9d8a-105b66aed01b" />
<br>

# Publicando uma página estática em HTML:
Com o Apache2 funcionando, podemos acessar a página padrão do Apache2 de duas formas pelo navegador de sua preferência:
* Por meio do *localhost*
```
http://localhost
```
Onde iremos receber uma página semelhante a esta:
<img width="1198" height="723" alt="image" src="https://github.com/user-attachments/assets/125ffebb-089f-4284-95bc-456a812bd023" />
<br>

* Por meio do IP próprio da máquina, onde precisaremos encontrar o IP utilizando o comando:
```
ip a
```
Obtendo o ip como retorno:
<img width="951" height="264" alt="image" src="https://github.com/user-attachments/assets/6433feac-f49c-4409-a1ea-fa7989097943" />

Por meio deste endereço: ```10.0.2.15``` conseguiremos acessar a página padrão do Apache2 no nosso navegador:
<img width="1195" height="714" alt="image" src="https://github.com/user-attachments/assets/06b067ea-bb56-4638-b67b-820713c0e5bf" />
<br>

Podemos ter acesso ao documento index.html exibido como padrão no caminho:
```
cd var/www/html
```
Para exibir nossas próprias páginas, podemos inserir nosso próprio documento index.html. Para esta prática, utilizaremos uma página disponibilizada no GitHub, por isso, iremos instalar o GitHub no nosso servidor Linux para podermos clonar o repositório:
* Para instalar o Git, execute:
```
sudo apt install git
```
Durante o processo de instalação uma permissão será solicitada, para que a instalação padrão seja realizada, confirme com **'S'** ou **'Y'** de acordo com a linguagem do seu sistema operacional. 

Nesta prática utilizaremos o seguinte repositório: ```https://github.com/matheusmanuel/site-simples-com-html-e-css-.git```
* Para clonar o repositório utilizaremos:
```
sudo git clone https://github.com/matheusmanuel/site-simples-com-html-e-css-.git
```
O clone, gerará uma pasta nomeada de ```site-simples-com-html-e-css-```, para que a página funcione no nosso servidor, os arquivos desta pasta deverão estar no diretório ```cd var/www/html``` para mover os arquivos executaremos os seguintes comandos:
```
sudo cp site-simples-com-html-e-css-/background.jpg .
sudo cp site-simples-com-html-e-css-/index.html .
sudo cp site-simples-com-html-e-css-/Como-Criar-um-SITE-Com-HTML-e-CSS-na-prática.png .
```
