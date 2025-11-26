# Objetivo
Esta prática tem com objetivo fazer com que nosso servidor HTTP disponibilize dois sites ao mesmo tempo, pode meio de domínios diferentes. Ou seja, ao acessar por exemplo ```http://site1``` iremos ter acesso à um site e ao acessar ```http://site2``` iremos acessar outro site, usando apenas um servidor HTTP.

# Criação de diretórios para gerenciamento dos sites

Para publicar os sites, precisamos inicialmente criar os diretórios que comportarão as nossas páginas, para isto, deveremos ingressar no diretório ```/var/www```:
```
cd /var/www
```
Neste diretório iremos criar as pastas para gerenciamento dos arquivos das nossas páginas:
```
sudo mkdir -p site1/public_html
```
```
sudo mkdir -p site2/public_html
```
O parametro ```-p``` no comando ```mkdir``` tem o intuito de criar além do diretório site1 ou site2, criar também a pasta ```public_html``` dentro delas.

Como podemos ver no print a seguir, criamos os diretórios site1 e site2, e dentro do diretório site, o public_html já está criado:
<img width="567" height="223" alt="image" src="https://github.com/user-attachments/assets/525397f9-4188-4039-a683-a48082f1d6e8" />

# Permissão para gerenciamento do diretório sem a necessidade do ```sudo```

Para que seja possível o gerenciamento dos arquivos dos diretórios criados sem a necessidade do sudo a cada comando, executaremos as seguintes instruções:
```
sudo chown -R $USER:$USER /var/www/site1/public_html
```
```
sudo chown -R $USER:$USER /var/www/site2/public_html
```

O comando acima permite que o usuário atual, no meu caso o ```otaniel``` tenha acesso de administrador nas pastas listadas e a todos os arquivos dentro delas.

# Criação das nossas páginas

Iremos neste ponto, nossos arquivos index para a exemplificação de como do procedimento de publicação de e dois sites. Para isso ingressaremos no diretório ```cd /var/www/site1/public_html``` e criar um arquivo ```index.html```:
```
nano index.html
```
Neste arquivo, para nossa prática, uma página simples será o suficiente, para isto, criaremos a seguinte página:
```
<html lang="pt-br">
<head>
    <title>Página Site 1</title>
</head>
<body>
    <center>
        <h1>Site 1 no ar!</h1>
    </center>
</body>
</html>
```
Segue um registro dos passos anteriores:

<img width="533" height="333" alt="image" src="https://github.com/user-attachments/assets/85b7e477-64c5-45b9-9536-ff69ea750828" />

Faremos o mesmo para o diretório ```cd /var/www/site2/public_html``` criando o arquivo ```index.html``` alterando seus textos para 2 ao invés do 1 do site1.

<img width="528" height="377" alt="image" src="https://github.com/user-attachments/assets/fddf05a6-6916-45e0-a436-2bd612b6f9d0" />

# Configuração dos endereços dos sites

Para a configuração dos endereços dos sites, devemos ingressar no seguinte diretório:
```
cd /etc/apache2/sites-available
```
Neste diretório encontraremos os seguintes arquivos:

<img width="428" height="68" alt="image" src="https://github.com/user-attachments/assets/254fbc95-798e-4c97-83f1-270f606d9150" />

O arquivo ```000-default.conf``` contém as configurações padrões de publicação do site default. Considerando a informação anterior, iremos fazer duas cópias desse arquivo de configurações para endereçar nossos sites usando os comandos:
```
sudo cp 000-default.conf site1.conf
```
No entanto, é necessário editar os dados deste arquivo indicando nosso diretório criado, para isto, ingressaremos no arquivo com o ```sudo nano site1.conf```, onde atualizaremos os seguintes dados:

<img width="1191" height="595" alt="image" src="https://github.com/user-attachments/assets/d5c7a40d-0c8b-449d-b507-7e38772f1ea1" />

Por:

<img width="1193" height="667" alt="image" src="https://github.com/user-attachments/assets/ffcf738e-54ac-4253-9229-73b87bdf723b" />

E faremos o mesmo para o site 2:

<img width="1190" height="641" alt="image" src="https://github.com/user-attachments/assets/587e5bfe-3c96-46af-a5fa-db42c764dd47" />

Agora que configuramos os endereços, iremos habilitar as configurações os sites no Apache2 com os seguintes comandos:
```
sudo a2ensite site1.conf
```
```
sudo a2ensite site2.conf
```

Como no site default não é mais interessante para nós, podemos desabilitá-lo utilizando o seguinte comando:
```
sudo a2dissite 000-default.conf
```

Após tantas alterações nas configurações do Apache2, será necessário reiniciar o serviço. Para reiniciar o Apache2, utilizaremos o seguinte comando:
```
sudo systemctl restart apache2
```

Além disto, precisamos configurar o nosso arquivo de hosts para apontar para nossos sites. Este apontamento é feito no arquivo localizado no endereço ```/etc/hosts``` onde para editá-lo utilizaremos ```sudo nano /etc/hosts``` :

<img width="786" height="258" alt="image" src="https://github.com/user-attachments/assets/93f58587-9c73-453f-b181-47fb070596b4" />

Após este apontamento, podemos buscar no navegador de nossa preferência pelos endereços:
```
htpp://site1
```
```
htpp://site2
```
 E encontraremos nossas páginas funcionando:

<img width="1205" height="761" alt="image" src="https://github.com/user-attachments/assets/cf32c2b1-bbc7-431f-82d4-00de746fb387" /> <img width="1202" height="757" alt="image" src="https://github.com/user-attachments/assets/74908bb0-b47f-46e0-9e36-8f7f06272285" />

# Conclusão

Com esta prática, configuramos o Apache2 para hospedar múltiplos sites em um único servidor. Passamos pela criação dos diretórios, ajuste de permissões, definição de virtual hosts e atualização do arquivo hosts. O exercício demonstrou na prática como estruturar e gerenciar diferentes páginas de forma organizada e funcional.

