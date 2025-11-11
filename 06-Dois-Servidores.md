# Introdução
A prática a seguir, visa a configuração de dois serviços DNS. Para isto, será necessário subir mais uma máquina virtual e intalar o Apache2 como na prática 1.


# Definindo diretórios

Neste ponto iremos criar os diretórios no apache, onde nosso servidor será nomeado de Matriz. Para isto é necessário ingressar no diretório padrão dos arquivos para nosso servidor HTTP ```cd /var/www```, onde criaremos nosso diretório usando:
```
sudo mkdir -p matriz/public_html
```
Em seguida, iremos criar nosso arquivo html usando:
```
sudo nano index.html
```
No arquivo index.html, iremos criar nossa página simples usando este trecho em HTML:
```
<html>
<head><title>Olá seja bem vindo à Matriz</tilte>
</head>
<body>
<h1>Bem vindo ao site da Matriz</h1>
</body>
</hmtl>
```

Veja nosso progresso até aqui:

<img width="581" height="185" alt="image" src="https://github.com/user-attachments/assets/a4b4878a-c0a5-42c4-83e4-f0482093501f" />

Agora iremos ingressar nas configurações dos sites disponíveis ```cd /etc/apache2/sites-available```, onde encontraremos o arquivo de configuração default, para habilitar o site podemos criar um arquivo de configuração usando o arquivo default com o comando:
```
sudo cp 000-default.conf matriz.conf
```
Iremos editar o arquivo de configuração da seguinte maneira:

<img width="1203" height="764" alt="image" src="https://github.com/user-attachments/assets/f3d321b0-64d5-4697-8962-a35a32f3f810" />

Após editar o arquivo de configurações, iremos habilitar a configuração criada usando:
```
sudo a2ensite matriz.conf
```

Como não será necessário o arquivo de configuração default, iremos desabilitá-lo usando:
```
sudo a2dissite 000-default.conf
```

Agora, para fazer valer as configurações feitas iremos reiniciar o Apache2 usando:
```
sudo /etc/init.d/apache2 restart
```

Para que consigamos realizar a comunicação entre os servidores será necessário configurar um ip para a rede que utilizamos e definir a rede do nosso servidor 2 como rede interna. Configurando IP:

<img width="588" height="485" alt="image" src="https://github.com/user-attachments/assets/d66afeaf-d515-4f00-bf75-84a64d49a439" />

Após configurar o IP, será necesário desligar a máquina para que seja possível a alteração do tipo de placa de rede de NAT para Rede Interna:

<img width="780" height="488" alt="image" src="https://github.com/user-attachments/assets/ca11e4f1-63d5-4b02-8b0a-32e9b5963da4" />


# Configuração do 



