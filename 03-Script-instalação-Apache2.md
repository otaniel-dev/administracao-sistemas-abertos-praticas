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

if [ ! -x /etc/init.d/apache2 ]; then                    #Verificação de existência do diretório onde o apache é instalado;
echo "Apache não encontrado. Iniciando a instalação..."  #Mensagem informativa;
sudo apt update                                          
sudo apt install apache2 -y                              #O parametro [-y] é usado para confirmar a instalação;
else
echo "Apache já está instalado"                          #Mensagem informativa caso o apache esteja instalado
fi
```

Faremos o mesmo para o Git usando:
```
if [ ! -x /usr/bin/git ]; then                               #Verificação de existência do binário principal do Git;
    echo "Git não encontrado. Iniciando a instalação..."     #Mensagem informativa;
    sudo apt update
    sudo apt install git -y                                  #O parametro [-y] é usado para confirmar a instalação;
else
    echo "Git já está instalado"                             #Mensagem informativa caso o Git esteja instalado
fi
```

Após a certeza de que os programas necessários, Apache2 e Git estão instalados no nosso servidor HTTP, iremos criar e ingressar na pasta que conterá nosso conteúdo usando os seguintes comandos:
```
sudo mkdir -p /var/www/aluno/public_html    #O parametro [-p] é usado para que caso os diretórios listados não existam, sejam criados;
cd /var/www/aluno/public_html/              #Ingressa no diretório criado;
```

Em seguida faremos o clone do GitHub do Matheus:
```
sudo git clone https://github.com/matheusmanuel/site-simples-com-html-e-css-.git
```
Iremos copiar os arquivos para o diretório ```/var/www/aluno/public_html``` e em seguida excluir o diretório e os arquivos diplicados:
```
sudo cp -r site-simples-com-html-e-css-/* .
sudo rm -rf site-simples-com-html-e-css-/
```

Chegamos ao ponto em que precisamos configurar nosso Apache2 para que ele identifique o nosso site, para isto, criaremos o arquivo.conf necessário:
```
cd /etc/apache2/sites-available/

sudo tee aluno.conf <<EOF          #O utilitário [tee] unido ao <<EOF ... EOF é utilizado para criar o arquivo e inserir o texto que está entre o <<EOF e o EOF dentro do arquivo;
<VirtualHost *:80>
        ServerAdmin admin@aluno    
        ServerName aluno
        ServerAlias www.aluno
        DocumentRoot /var/www/aluno/public_html
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
EOF
```
Em seguida habilitaremos o arquivo criado:
```
sudo a2ensite aluno.conf
```

Novamente utilizaremos o [tee] para adicionar o direcionamento do host:
```
sudo echo "127.0.0.1 aluno" | sudo tee -a /etc/hosts
```
E por fim, reiniciar o serviço do Apache2:
```
sudo /etc/init.d/apache2 restart 
```

Após concluído, nosso script terá estas instruções:
```
#! /bin/bash

if [ ! -x /etc/init.d/apache2 ]; then                    
echo "Apache não encontrado. Iniciando a instalação..."  
sudo apt update                                          
sudo apt install apache2 -y                             
else
echo "Apache já está instalado"                          
fi
if [ ! -x /usr/bin/git ]; then                               
    echo "Git não encontrado. Iniciando a instalação..."     
    sudo apt update
    sudo apt install git -y                                  
else
    echo "Git já está instalado"                             
fi
sudo mkdir -p /var/www/aluno/public_html    
cd /var/www/aluno/public_html/              
sudo git clone https://github.com/matheusmanuel/site-simples-com-html-e-css-.git
sudo cp -r site-simples-com-html-e-css-/* .
sudo rm -rf site-simples-com-html-e-css-/
cd /etc/apache2/sites-available/
sudo tee aluno.conf <<EOF          
<VirtualHost *:80>
        ServerAdmin admin@aluno    
        ServerName aluno
        ServerAlias www.aluno
        DocumentRoot /var/www/aluno/public_html
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
EOF
sudo a2ensite aluno.conf
sudo echo "127.0.0.1 aluno" | sudo tee -a /etc/hosts
sudo /etc/init.d/apache2 restart 
```

Segue um registro do script em nossa máquina virtual:
<img width="745" height="677" alt="image" src="https://github.com/user-attachments/assets/c61d3bf5-68e4-47b4-a2f0-d78e1671ea54" />

Neste ponto, podemos salvar o script.

Ao finalizar o os comandos do nosso script, precisaremos dar a permissão de execução à nosso script, para isto utilizaremos o comando:
```
sudo chmod +x sripc.sh
```

Para executá-lo e vermos ele em ação utilizaremos o seguinte comando:
```
./script.sh
```

Resultado da execução do script:

<img width="682" height="413" alt="image" src="https://github.com/user-attachments/assets/6669c937-517f-4d27-a6fb-a0960a3bf86c" />

Segue a página do Matheus publicada no endereço htpp://aluno:

<img width="1201" height="766" alt="image" src="https://github.com/user-attachments/assets/3ed84ece-202c-47a7-9494-5b8a67d55028" />





