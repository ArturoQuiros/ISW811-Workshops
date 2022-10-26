# Workshop 01

## Prerequisitos en Windows

### Habilitar Virtualizacion

Es posible que algunos equipos deban habilitar en el BIOS la virtualizacion, por lo que se debe revisar bien que el equipo tenga habilitado esto

### Instalando Virtual Box

1. Bajar el .exe de la pagina oficial
2. Ejecutar el setup y guiarse con el wizard de instalacion

### Instalando Vagrant

1. Bajar el .exe de la pagina oficial
2. Ejecutar el setup y guiarse por el wizard de instalacion

### Instalando CMDER

1. Bajar desde la pagian oficial
2. Instalar en la ruta deseada
3. Añadir la variable de entorno

---

## Levantando la VM

**Bajando la Imagen**

`vagrant init debian/bullseye64`

habilitar la red editando el archivo **Vagrantfile**

**Corriendo la Imagen**

`vagrant up`

**Conectandose a la PC**

`vagrant ssh@IP_SERVER`

**Agregar llave SSH**
`ssh-agent -s`
`ssh add <RUTA DE LA LLAVE>`

## cd .vagrant\machines\default\virtualbox\

# Comandos

---

1. Encender: `vragrant up`
2. Apagar: `vagrant halt`
3. Revisar si la pc esta corriendo: `vagrant status`
4. conectar ssh: `vagrant ssh`
5. Hacer tar.gz : `tar cvfz <nombreArchivoSalida> <directorioParaComprimir>`
