# Instalação do Webmin

O intuito da prática a seguir é conseguir gerenciar graficamente os serviços disponíveis em nosso servidor, com a utilização do Webmin, veremos que isto será possível.

Inicialmente retornaremos o IP para DHCP ao invés de Estático como definido na prática anterior para que possamos instalar o arquivo compactado do Webmin.

Após isto, poderemos instalar o Webmin por meio do comando:
```
wget https://www.webmin.com/download/deb/webmin-current.deb
```

Após a instalação, será necessário descompactar o arquivo ```webmin-current.deb``` usando o seguinte comando:
```
sudo dpkg -i webmin-current.deb
```

Veja um registro deste ponto:

<img width="722" height="434" alt="image" src="https://github.com/user-attachments/assets/8d04fb60-8133-458e-b5e7-0d48199c3033" />

Agora iremos realizar a instalação do Webmin utilizando o comando:
```
sudo apt -f install -y
```

Após a conclusão, podemos verificar no navegador de nossa preferência, o painel do Webmin, que utiliza a porta ```10000``` por padrão:

<img width="1212" height="680" alt="image" src="https://github.com/user-attachments/assets/9c48674e-f2d4-4b37-a01d-fd4f184620c7" />

Obs.: Usuário e senha do Webmin, são os mesmos do nosso servidor.

No nosso Webmin, podemos encontrar graficamente o serviço do nosso Apache2:

<img width="1206" height="678" alt="image" src="https://github.com/user-attachments/assets/a15b16ec-ce1e-4b86-b49c-e0221810fefb" />

Bem como podemos verificar as Zonas do nosso servidor DNS Bind9:

<img width="1208" height="766" alt="image" src="https://github.com/user-attachments/assets/b9a6b19e-cbad-4d2c-92fa-0acbe136bb61" />

Para concluir nossa prática, é necessário retornar as configurações de IP Estático anteriores.
