# Instalação do Servidor DNS

Considerando as práticas anteriores, precisaremos limpar nosso arquivo de hots, retirando os redirecionamentos que fizemos e retornando às condigurações iniciais deste arquivo.

<img width="1188" height="213" alt="image" src="https://github.com/user-attachments/assets/02b50b60-c47e-45f3-aa51-8a9e8853f1c4" />

O servidor DNS que  iremos intalar é o Bind9, para isto seguiremos com o comando para a instalação:

```
sudo apt install bind9
```

Após intalar podemos verifica a execução do serviço usando:

```
sudo /etc/init.d/named status
```

Veja que o nosso servidor DNS está instalado e ativo:

<img width="1201" height="455" alt="image" src="https://github.com/user-attachments/assets/7ba14b51-d51e-4c3e-9c26-0450c7718246" />

# Configuração do servidor DNS

Para iniciarmos a configuração do nosso servidor DNS será necessário inicialmente deixar nosso IP estático, para isto iremos ingressar nas configurações de rede do nosso SO e inserir um IP, veja como foi condigurado nosso endereço IPv4:

<img width="1277" height="794" alt="image" src="https://github.com/user-attachments/assets/c5d65f12-1d69-44f5-9789-912d06ca85d5" />

Agora com o endereço fixo, iremos fazer um backup do arquivo de configuração inicial do nosso Bind9 para que caso alguma alteração feita por nós tenha um efeito indesejado, seja fácil retornar ao estado inicial, para isto iremos ingressar no diretório do Bind9:
```
cd /etc/bind
```
E criaremos o backup usando:
```
sudo cp named.conf.local named.conf.local_bckp
```
<img width="1196" height="197" alt="image" src="https://github.com/user-attachments/assets/7244743f-3f40-4df5-b500-8fbaea3d2216" />

Após backup criado, iremos configurar nossa Zona Direta, que é responsável por traduzir nomes por IP, para isto, iremos editar o arquivo ```named.conf.local```:
```
sudo nano named.conf.local
```
O arquivo tem este layout inicialmente:

<img width="1204" height="303" alt="image" src="https://github.com/user-attachments/assets/d33fb009-b1bf-4999-ab4f-7fb175f3e9a2" />

Para configurar nossa Zona Direta iremos utilizar:
```
//Forward Zone
zone "meudominio.com" {
      type master;
      file "/etc/bind/db.meudominio.com";
};
```
Ao adicionar este trecho ao fim do arquivo, habilitamos o nosso domínio para ser utilizado e convertido em IP.

Agora é necessário configurar a Zona Reversa, que é a responsável por converter IP em nome, semelhante à Zona direta, utitilzaremos:
```
//Reverse Zone
zone "192.168.0.-in.addr.arpa" {
      type master;
      file "/etc/bind/db.reverse99";
};
```
Após a adição das Zonas, veja como o estado atual do arquivo:
 
<img width="1199" height="482" alt="image" src="https://github.com/user-attachments/assets/025304d4-08f4-4ae9-b647-ec63c1398c5f" />


Agora que configuramos nossas Zonas, é necessário criar os bancos de dados para as Zonas Direta e Reversa acessarem. Por padrão os arquivod db.local e db.127 são respectivamente responsáveis por armazenarem essas informações, por isto, iremos com base neles, criar nossos arquivos de banco de dados usando:
```
sudo cp db.local db.meudominio.com
sudo cp db.127 db.reverse99
```

Após criados os arquivos, iremos editar o ```db.meudominio.com```:
```
sudo nano db.meudominio.com
```

Ao abrir o arquivo ele estará neste estado:

<img width="1203" height="370" alt="image" src="https://github.com/user-attachments/assets/c3cde7f6-b16a-448b-bfc3-75bab29a86c1" />

Incialmente, trocaremos todos os ```localhost``` por ```meudominio.com``` e em seguida, substituiremos o IP loopback pelo IP que definimos para nosso computador, deixando nosso arquivo assim:

<img width="1202" height="334" alt="image" src="https://github.com/user-attachments/assets/c7356ad7-5b86-4fa1-8161-430a17a57be4" />

Substituiremos também os ```localhost``` por ```meudominio.com``` novamente, em seguida definiremos o final do nosso IP, o arquivo inicialmente está assim:

<img width="1207" height="330" alt="image" src="https://github.com/user-attachments/assets/989e7cc0-e954-402a-9cda-bdef87b43146" />

Ficando assim ao fim da configuração:

<img width="1208" height="314" alt="image" src="https://github.com/user-attachments/assets/a5301c09-cee5-4370-8f51-28113e39cc6b" />


Agora, irenmos adicionar nosso server no ```resolv.conf```:

<img width="1210" height="513" alt="image" src="https://github.com/user-attachments/assets/0dd1c594-140c-4bab-81a1-13f5768f631e" />



