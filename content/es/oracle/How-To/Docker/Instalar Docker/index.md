---
title: "Instalar Docker"
linkTitle: "Instalar Docker"
description: "Instalar Docker en Oracle Cloud."
weight: 1
---

En este tutorial vamos a ver cómo **instalar Docker desde el repositorio oficial**.

Para ello, **importante**, previamente [conectarnos a la instancia deseada.](/oracle/how-to/creacion-host/#conectarse-a-la-instancia)

### Paso 1: Actualizar la base de datos local

Actualice la base de datos local con el comando:

```bash
sudo apt-get update
```

### Paso 2: Descargar dependencias

Ejecutar estos comandos para permitir que el sistema operativo Ubuntu/Linux acceda a los repositorios de Docker a través de HTTPS.

En la ventana de terminal, escribe:

```bash
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
```

Para aclarar, aquí hay un breve desglose de cada comando:

- **apt-transport-https** : permite que el administrador de paquetes transfiera archivos y datos a través de https.
- **certificados ca** : permite que el sistema (y el navegador web) verifiquen los certificados de seguridad.
- **curl** : esta es una herramienta para transferir datos.
- **software-properties-common** : agrega scripts para administrar software.

### Paso 3: Agregar la clave GPG de Docker

La clave GPG es una característica de seguridad.

Para asegurarse de que el software que está instalando es auténtico, escribe en la consola:

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add –
```

Si da error el anterior comando con un mensaje de error de este estilo:

```bash
# Error comando anterior
ubuntu@hadoop-3:~$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add –

gpg: can't open '–': No such file or directory
```

Se solucionaría de la siguiente forma:

```bash
# Guardamos la salida de curl en un fichero, ej: ficherossl.txt
ubuntu@hadoop-3:~$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg > ficherossl.txt

# Añadimos clave seleccionando dicho fichero
ubuntu@hadoop-3:~$ sudo apt-key add ficherossl.txt
OK
```

### Paso 4: Instalar el repositorio de Docker

Para instalar el repositorio de Docker, escribe el comando en la terminal:

```bash
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu  $(lsb_release -cs)  stable"
```

El comando "**$ (lsb_release –cs )**" escanea y devuelve el nombre en clave de su instalación de Ubuntu, en este caso, Bionic. Además, la última palabra del comando, _stable_, es el tipo de versión de Docker.

Resultado de la salida una vez ejecutado:

```bash
ubuntu@hadoop-3:~$ sudo add-apt-repository "deb [arch=amd64] https://download.doc                                                                ker.com/linux/ubuntu  $(lsb_release -cs)  stable"
Hit:1 http://eu-frankfurt-1-ad-1.clouds.archive.ubuntu.com/ubuntu bionic InReleas                                                                e
Get:2 http://security.ubuntu.com/ubuntu bionic-security InRelease [88.7 kB]
Get:3 http://eu-frankfurt-1-ad-1.clouds.archive.ubuntu.com/ubuntu bionic-updates                                                                 InRelease [88.7 kB]
Get:4 https://download.docker.com/linux/ubuntu bionic InRelease [64.4 kB]
Get:5 http://eu-frankfurt-1-ad-1.clouds.archive.ubuntu.com/ubuntu bionic-backport                                                                s InRelease [74.6 kB]
Get:6 https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages [11.0                                                                 kB]
Get:7 http://eu-frankfurt-1-ad-1.clouds.archive.ubuntu.com/ubuntu bionic-updates/                                                                main amd64 Packages [897 kB]
Get:8 http://eu-frankfurt-1-ad-1.clouds.archive.ubuntu.com/ubuntu bionic-updates/                                                                main i386 Packages [662 kB]
Get:9 http://eu-frankfurt-1-ad-1.clouds.archive.ubuntu.com/ubuntu bionic-updates/                                                                universe amd64 Packages [1060 kB]
Get:10 http://eu-frankfurt-1-ad-1.clouds.archive.ubuntu.com/ubuntu bionic-updates                                                                /universe i386 Packages [1011 kB]
Fetched 3957 kB in 1s (3120 kB/s)
Reading package lists... Done
```

{{% alert title="Nota" color="info" %}}

Una versión _stable_ se prueba y se confirma que funciona, pero las actualizaciones se lanzan con menos frecuencia. Se puede sustituir _edge_ si desea actualizaciones más frecuentes, a costa de una inestabilidad potencial. Hay otros repositorios, pero tienen más riesgo: se puede encontrar más información en la [página web de Docker](https://docs.docker.com/v17.09/engine/installation/linux/docker-ce/ubuntu/#set-up-the-repository).

{{% /alert %}}

### Paso 5: Actualizar los repositorios

Actualizar los repositorios que acabamos de instalar con el comando:

```bash
sudo apt-get update
```

### Paso 6: Instalar la última versión de Docker

Para instalar la última versión de Docker:

```bash
sudo apt-get install docker-ce
```

Ahora debes tener Docker instalado, el daemon iniciado, y el proceso habilitado para iniciar durante el arranque.

Verifica que se esté ejecutando:

```bash
sudo systemctl status docker
```

El resultado debería ser parecido al siguiente, indicando que el servicio está activo y se está ejecutando:

```bash
ubuntu@hadoop-3:~$ sudo systemctl status docker
● docker.service - Docker Application Container Engine
   Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
   Active: active (running) since Tue 2020-03-31 07:59:51 UTC; 8h ago
     Docs: https://docs.docker.com
 Main PID: 25545 (dockerd)
    Tasks: 53
   CGroup: /system.slice/docker.service
           ├─25545 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
.....
```

Para comprobar que tenemos Docker instalado, ejecutamos en la terminal:

```bash
ubuntu@hadoop-3:~$ sudo docker --version
Docker version 19.03.8, build afacb8b7f0
```

**¡¡Enhorabuena!!** Tienes **Docker instalado en tu instancia dentro de Oracle Cloud**. :tada: :smile:
