# Workshop 6

## Preparando el ambiente

Creamos el archivo
`touch hello.sh `

Lo editamos

```bash
#!/bin/bash

    # Hola mundo en Bash

    clear
    echo "Hola mundo"
```

Preaprando insumos en la maquina virtual:

` echo "Hola mundo" > confidencial.txt`

`chmod 600 confidencial.txt`

`echo "Hola mundo publico" > publico.txt`

Agregabdo permisos

`sudo adduser USER`

Ingresar la informacion de USER

`su USER`

`cat publico.txt`

`cat confidencial.txt`

Lo agregamos al grupo

`sudo addgroup isw811`

`sudo gpasswd -a USER isw811`

`chown vagrant:isw811 confidencial.txt`

`sudo adduser USER`

## Modificand el script hello.sh:

```bash
    #!/bin/bash

    # Hola mundo en Bash

    clear
    printf "Ingrese su nombre: "
    read name
    echo

    if [ ${#name} -eq 0 ]; then
        echo "Me hubiera gustado conocerte..."
    else
        echo "Hola $name"
    fi

    while [ true ]; do
        printf "Ingrese su año de nacimiento (yyyy): "
        read birthyear
        echo

        if [ -z `echo $birthyear | grep -E ^-\?[0-9]*$`  ]; then
            echo "Debe ingresar un numero"
        else
            if [ $birthyear -ge 1930 ] && [ $birthyear -lt 2023 ]; then
                break
            else
                echo "Debe ingresar un numero entre 1930 y 2022"
            fi
        fi
    done

    if [ $birthyear -ge 2010 ]; then
        echo "Eres de la generacion alfa"
    elif [ $birthyear -ge 1995 ] && [ $birthyear -lt 2010 ]; then
        echo "Eres un nativo digital (Z)"
    elif [ $birthyear -ge 1982 ] && [ $birthyear -lt 1995 ]; then
        echo "Eres un millenial"
    elif [ $birthyear -ge 1965 ] && [ $birthyear -lt 1982 ]; then
        echo "Eres de la generacion X"
    elif [ $birthyear -ge 1945 ] && [ $birthyear -lt 1965 ]; then
        echo "Eres de la generacion de los Baby Boomers"
    elif [ $birthyear -lt 1945 ]; then
        echo "Eres de la generacion silenciosa"
    fi
```

## En la maquina virtual:

`cd /vagrant`

` chmod 744 hello.sh`

`./hello.sh`

## Haciendo de Backup de Noriwthwind:

`cd ~`

`mysqldump northwind > northwind.sql -u user_laravel` -p

`ls -lh`

`tar cvfz northwind.tar.gz northwind.sql`

`rm northwind.sql`

## Creando el backup-northwind.sh en maquina anfitriona

` touch backup-northwind.sh`

## En backup-northwind.sh:

```bash
    #!/bin/bash

    site="northwind.isw811.xyz"
    directory="/home/vagrant/backups/"$site
    datetime=$(date +"%Y%m%d_%H%M%S")
    database="northwind"
    username="user_laravel"
    password="secret"

    if [ ! -z "$1" ]; then
        filename="$site"_"$1.sql"
    else
        filename="$site"_"$datetime.sql"
    fi

    mkdir -p $directory
    cd $directory

    echo "$filename" >> "$directory/backup_$site.log"
    echo "Inicio: "$(date +"%d/%m/%Y %H:%M:%S") >> "$directory/backup_$site.log"

    echo "Iniciando respaldo..."

    mysqldump northwind > "$directory/$filename" -u $username --password=$password

    echo "Comprimiendo respaldo..."

    tar cvfz "$filename.tar.gz" $filename

    echo "Eliminando archivo temporal..."

    rm $filename

    echo "Fin: "$(date +"%d/%m/%Y %H:%M:%S") >> "$directory/backup_$site.log"
    echo >> "$directory/backup_$site.log"
```

## En la maquina virtual:

`cd /vagrant`

`chmod 744 backup-northwind.sh`

`./backup-northwind.sh `

`cd /home/vagrant/backups/northwind.isw811.xyz `

## Programando el Backup

`cd /vagrant`
`date`
`crontab -e`

Seleccionamos nano y agregamos debajo del ultimo comentario:

`29 03 _ 11 _ /vagrant/backup-northwind.sh \* \* \* \* \* /vagrant/backup-northwind.sh`
