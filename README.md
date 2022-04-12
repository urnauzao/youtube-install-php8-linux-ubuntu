Conteúdo do Canal Dev Tech Tips Brasil 

# How to Install PHP 8 on Linux Ubuntu 20.04 LTS
In this repository, I show step by step the installation of PHP 8 in linux environment Ubuntu 20.4 Lts.. 

# Como instalar o PHP em ambiente Linux Ubuntu 20.04 LTS
[pt-BR] Neste repositório, farei a instalação passo a passo do PHP 8 em ambiente Linux Ubuntu 20.04 LTS

# GUIA PT-BR
## Preparando o ambiente Linux
- Devemos atualizar nossas dependências e repositórios do sistema
> sudo apt update 

- Agora é hora de liberarmos a instalação e configuração de outros repositórios no sistema, por isso precisamos da seguinte instalação:
> sudo apt install software-properties-common -y 

## Adicionar Repositório do Ondřej Surý
- Isso mesmo, Ondřej é o responsável por disponibilizar e manutentir os pacotes oficiais do PHP tanto para Ubuntu quanto Debian. Como ele mesmo diz, <q>você não conseguirá chegar mais próximo dos módulos do PHP se não como ele disponibiliza</q>.
- Que saber mais sobre Ondřej acesse a página oficial dele [clicando aqui](https://deb.sury.org)
> sudo apt install php8.0 

## Buscando Extensões:
- Com o PHP instalado é hora de instalarmos as extensões que iremos precisar para o desenvolvimento.
- Para isso, primeiro vamos listar as extensões disponíveis
> sudo apt search php8.0-* 


<strong>Exemplo com varias extensões diponíveis:</strong> bz2, curl, ffi, ftp, fileinfo, gd, gettext, gmp, intl, imap, ldap, mbstring, exif, mysqli, odbc, openssl, pdo_firebird, pdo_mysql, pdo_oci, pdo_odbc, pdo_pgsql, pdo_sqlite, pgsql, shmop, snmp, soap, sockets, sodium, sqlite3, tidy, xsl 
    
- Vamos instalar as extensões mais comuns de serem utilizadas, através do comando abaixo:
> sudo apt install php-8.0-curl php-8.0-fileinfo php8.0-gd php8.0-mbstring php8.0-exif

- Habilitar Mysql(8.0^)
> sudo apt install php-8.0-mysqli php-8.0-pdo_mysql

- Habilitar Postgresql
> sudo apt install php-8.0-pgsql php-8.0-pdo_pgsql

- Habilitar Sqlite
> sudo apt install php-8.0-sqlite3 php-8.0-pdo_sqlite

- Habilitar Microsoft SQL Server
> sudo apt install php-8.0-odbc php-8.0-pdo_odbc

- Habilitar Oracle DB
> sudo apt install php-8.0-oci8_12c php-8.0-oci8_19 php-8.0-pdo_oci

## Onde encontrar outras extensões
Se você precisa de extensões como o Xdebug, Php Redis, Kafka Client, ou outra, então recomendo realizar a instalação do `PHP-PEAR`, com o comando abaixo e visite os sites de repositórios de extensões que vos apresento mais abaixo:
> sudo apt-get install php-pear

- [PEAR](https://pear.php.net)
- [PECL](https://pecl.php.net)

## Testando o PHP
Um modo simples de testar o PHP é com o comando abaixo:
> php --ini

Caso ocorra erro por não encontrar o comando PHP no sistema então passe para próxima etapa e veja como criar um atalho para o comando php. Ou você também pode testar:
> php8 --ini

Outro teste que podemos fazer é criar um arquivo `index.php` e o iniciarmos com servidor local do PHP, através do comando:
> php -S localhost:8000 index.php

## Alterando entre versões do PHP
Caso você possua varias versões do PHP instaladas na maquina e deseje escolher uma principal você pode:
> sudo update-alternatives --config php  

Ou, você também pode alterar o `alias` do ambiente Linux para o comando `php`.
Para visualizar seus `alias` execute:
> alias

Para definir um alias para o PHP execute algo como o exemplo:
> alias php="/usr/local/php8/bin/php"
É importante que você se certifique-se que este é o diretório de sua instalação do PHP. 

# EXTRA

## Preparando nosso PHP para Produção
Agora, caso você deseje preparar seu ambiente para produção, então será necessário configuração de um servidor HTTP, trago aqui dois exemplos que são os mais utilizados, um deles se trata do Nginx e o outro do Apache.

### Instalando Apache
> sudo apt install libapache2-mod-php8.0 &&
> sudo a2enmod php8.0 

### Instalando Nginx
> sudo apt install php8.0-fpm && 
> sudo systemctl enable php8.0-fpm &&
> sudo systemctl start php8.0-fpm 

Feito isso, será preciso configurar os arquivos do Nginx para que consiga usar via proxy o PHP-FPM. Caso isso não seja feito o Nginx você não conseguirá acessar arquivos em formato PHP. 
Uma dica para realizar essa ação é buscar por `fastcgi_pass unix:/run/php/php8.0-fpm.sock`
