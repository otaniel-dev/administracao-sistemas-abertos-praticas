# Introdução
A prática a seguir, visa a configuração de dois serviços DNS. Para isto, será necessário subir mais uma máquina virtual e intalar o Apache2 como na prática 1.
Segue o esquema a ser criado:

<img width="832" height="366" alt="image" src="https://github.com/user-attachments/assets/68fbc321-e7a1-4e95-9d3d-ee491a75fb4c" />

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

<img width="1202" height="723" alt="image" src="https://github.com/user-attachments/assets/7303ab6f-bb80-4c31-88f7-b87dbd2a8c81" />


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

Observe que o endereço do DNS é o endereço do Servidor Inicial com final 99.

Após configurar o IP, será necesário desligar a máquina para que seja possível a alteração do tipo de placa de rede de NAT para Rede Interna:

<img width="780" height="488" alt="image" src="https://github.com/user-attachments/assets/ca11e4f1-63d5-4b02-8b0a-32e9b5963da4" />


# Configuração do DNS

Para que nosso segundo servidor consiga resolver nomes usando o nosso primeiro servidor, será necessário configura o bind para nosso outro domínio, no caso ```matriz.com```, para isso será necessário criar o arquivo de dados para a matriz usando meudominio como base. Para isso iremos ingressar no diretório ```cd /etc/bind``` e executar o seguinte comando:
```
sudo cp db.meudominio.com db.matriz.com
```

Em seguida, será necessário editar o arquivo alterando os parametros de ```meudominio.com``` para ```matriz.com``` inserindo o IP da segunda máquina o ```192.168.0.100```, veja como o arquivo ficará no registro a seguir:

<img width="1205" height="456" alt="image" src="https://github.com/user-attachments/assets/4eb4a80b-932c-4fd2-a813-ff7e19c145d6" />

Agora, iremos configurar a Zona Direta [Será necessário somente a zona direta, não precisa da reversa] para a ```matriz.com```, para isto, iremos ingressar no arquivos de zonas o ```named.conf.local``` e adicionar as zonas necessárias como na imagem a seguir:

<img width="1004" height="626" alt="image" src="https://github.com/user-attachments/assets/1d7b71fc-47fe-4761-8aef-f883c3d847da" />

Para a Zona reversa, iremos acessar o arquivo ```db.reverse99``` usando ```sudo nano db.reverse99``` para adicionar o IP nosso outro dominio o ```matriz.com```, veja como ficará o arquivo com a adição do IP 100 à lista de Zonas Reversas:

<img width="647" height="325" alt="image" src="https://github.com/user-attachments/assets/4207f96e-a31d-4697-890e-b04e6edb5436" />

Após concluir as configurações de Zona, será necessário reiniciar o Bind usando:
```
sudo /etc/init.d/named restart
```

Após a reinicialização, veja que no Servidor 1, é possível acessar o site do Servidor 2:

<img width="1284" height="874" alt="image" src="https://github.com/user-attachments/assets/f85810fe-2d89-4cee-8b99-1bd3593e429b" />

Assim como no Servidor 2 é possível acessar o site do Servidor 1:

<img width="1282" height="867" alt="image" src="https://github.com/user-attachments/assets/872cfe27-18f5-4898-917a-0f3116b1e830" />
