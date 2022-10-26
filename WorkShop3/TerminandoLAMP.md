# WorkShop 3

### Desde la maquina anfitriona

1. Me duplico el archivo _lfts.isw811.xyz.conf_ para _mibanco.com.conf_
2. Mando todos los archivos _.conf_ a la carpeta _vhosts_ (hay que crearla)
3. Creo la carpeta _mibanco.com_ en _sites_
4. modificamos el _.conf_ y austamos la ruta debido a que no usamos la ruta public
5. Copiamos el _.conf_ en _sites-available_
6. revisar sintaxis
   `sudo apache2ctl -t `

7. Montamos el sitio
   ` sudo a2ensite vagrant/lfts.isw811.xyz.conf`

8. Recargamos apache
   ` sudo systemctl reload apache2.service`

## Deshabilitar sitio por defecto

1. `sudo a2dissite 000-default.conf`
2. `sudo systemctl reload apache2`

## Instalar composer

1. Ir a https://getcomposer.org/
2. Crear carpeta composer en /opt

3. Descargar
   `sudo php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"`
4. Ejecutar
   ` php composer-setup.php`
5. Crear ruta relativa
   `sudo ln -s /opt/composer/composer.phar /usr/bin/composer`

## Descargar laravel

1. Ir a https://packagist.org/packages/laravel/laravel
2. Ir a a ruta _/vagrant/sites/_
3. Crear el proyecto `composer create-project laravel/laravel:8.6.12`

## Publicando el sitio

4. Guardamos la plantilla `tar cvfz laravel laravel.tar.gz laravel`
5. Borramos la carpeta _lfts.isw811.xyz_
6. Renombramos la carpeta _laravel_ por _lfts.isw811.xyz_

## Comenzando el curso
