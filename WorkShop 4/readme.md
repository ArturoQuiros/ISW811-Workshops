# Habilitando la Base de Datos

1. Nos conectamos por SSH a la VM
2. Instalar la BD `sudo apt-get install mariadb-server mariadb-client` esto en caso de que no esté instalada.
3. Crear la BD y el usuario para Laravel entrando a la BD con el comand `sudo mysql`
4. Identificamos las BD's con `show databases;`
5. Si aplica creamos la BD `create database lfts_db;`
6. Creamos un usuario `create user laravel_user identified by "12345";`
7. Darle permisos al usuario nuevo `grant all privileges on lfts_db.\* to laravel_user;`
8. Refrescamos los permisos con `Flush privileges`
9. Salimos con `quit`

# Probando el user

1. Nos conectamos la BD con `mysql -u laravel_user --password="1345"`

# Creando otro sitio LARAVEL

1. En la carpeta de /sites
2. composer create-project laravel/laravel:8.6.12
3. Creamos la carpeta miblog.com y movemos el contenido de la carpeta Laravel

# Creando otro VHOST

1. Vamos a **/vhosts** y hacemos una copia del archivo **lfts.isw811.xyz.conf**
2. Renombramos el archivo **miblog.com.conf**
3. Reemplazamos el dominio **lfts.isw811.xyz** por **miblog.com** en todo el archivo .conf

# Desplegando el sitio

1. En la carpeta **/vhosts** copio el archivo a la carpeta de sitios disponibles `sudo cp miblog.com.conf /etc/apache2/sites-available`
2. Habilitamos el sitio `sudo a2ensite miblog.com.conf`
3. Validamos si hay errores `sudo apache2ctl -t`
4. Montamos el sitio `sudo sudo a2ensite miblog.com.conf`
5. Reiniciamos Apache `sudo systemctl reload`
6. Entramos al sitio **miblog.com**

# Instalado el AUTH

## Instalamos Node Version Manager NVM

1. Instalamos node.js y npm `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash`
2. Recargamos el bash `source ~/.bashrc`

## Instalamos Node.JS y NPM

1. Instalamos la version mas estable de node `nvm install --lts`

## Instalando el modulo de Auth

1. En la carpeta del proyecto **/miblog.com**
2. Descargamos Laravel UI `composer require laravel/ui`
3. Descargamos BootStrap `php artisan ui bootstrap`
4. Descargamos BootStrap `php artisan ui bootstrap --auth`
5. Instalamos los Node Modules `npm install`
6. Corremos el proyecto `npm run dev`

# Conectando Laravel a la BD

Buscamos el archivo **.env** y modificamos lo siguiente

```
APP_URL=http://miblog.com

DB_DATABASE=lfts_db
DB_USERNAME=laravel_user
DB_PASSWORD=12345
```

## Creando las tablas de Laravel

Corremos las migraciones `php artisan migrate`

# Nota!

Es importante que la maquina anfitriona tenga el dominio **miblog.com** en sus hosts
