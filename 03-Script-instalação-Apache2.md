# Criação do Script

O script que será criado nesta aula tem o intuito de realizar a instalação e configuração do Apache2 por meio de um script, tornando a repetição da instalação e configuração muito mais rápida e simples.

Iremos iniciar com a criação do arquivo que conterá as instruções utilizando o seguinte comando:
```
sudo nano script.sh
```
Obs.: Por estamos usando o comando ```sudo``` será necessário fornecer a senha de administrador da máquina.

Em seguida abrirá o arquivo onde declararemos as instruções, para iniciar, iremos verificar se a instalação do Apache2 já foi executada, caso não iremos instalar, para isto utilizaremos o seguinte comando:

Obs.: Em arquivos [.sh] os comentários são feitos com o caractere #, sendo assim, o que houver após o # é apenas um comentário e será desconsiderado na execução do script, tendo somente o intuito de informar o que cada parte importante do script faz.
```
#! /bin/bash

if [ ! -x /etc/init.d/apache2 ]; then                        #Verificação de existência do diretório onde o apache é instalado;
echo "Apache não encontrado. Iniciando a instalação..."  #Mensagem informativa;
sudo apt update                                          
sudo apt install apache2 -y                              #O parametro [-y] é usado para confirmar a instalação;
else
echo "Apache já está instalado"                          #Mensagem informativa caso o apache esteja instalado
fi
```

