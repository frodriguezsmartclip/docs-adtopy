---
title: "Creación de Host"
linkTitle: "Creación de Host"
description: "Creación de Host en Oracle Cloud."
weight: 1
---

## Creación de host

Pasos a seguir para **crear un host con una IP permanente y asignarle almacenamiento**. Previamente hemos accedido al compartimento `smartclip_bigdata_cloud` y todas las operaciones las realizaremos en este:

### Crear la instancia

El primer paso es provisionar el host. Por defecto, las instancias se crean con un disco de arranque a partir de una imagen de sistema operativo y una IP pública que no está reservada (no es fija).

1. Desde el menú, abrimos **Recursos informáticos** e **Instancias**.
2. Pulsamos **Crear instancia**.
3. Le damos un **nombre** a la instancia.
4. Elegimos la **imagen base del SO** (p.ej.  Canonical Ubuntu 18.04 Minimal).
5. Asignar un **dominio de disponibilidad** (o dejar el que selecciona por defecto).
6. Elegir el **Shape** (características de la instancia), en el caso de *smartclip_bigdata_cloud* utilizamos **VM.Standard2.2**.
7. El resto de parámetros los podemos dejar por defecto, salvo que queramos modificar alguno.
8. Añadir la **clave pública** para acceder por *ssh*. (fichero _oracle-key.pub_)
9. Una vez pulsamos en el botón **Crear** la instancia comenzará a provisionarse.

### Asociar una IP reservada (permanente)

Si necesitamos que la IP pública de esta máquina sea permanente, primero tendremos que reservar una dirección y asociársela  a la instancia que acabamos de crear.

1. Para ello, abrimos el menú **Red** e **IP públicas**. A continuación, pulsamos **Crear IP permanente reservada**.
2. Le asignamos un **nombre** (es buena idea hacerlo coincidir con el de la instancia para identificarlo con más facilidad más adelante) y pulsamos **Crear IP permanente reservada**.
3. Volvemos a **Recursos informáticos** e **Instancias** y pulsamos en la instancia que acabamos de crear para acceder a su configuración.
4. Al final de esta, hay un menú de **Recursos**, pulsamos en **VNIC asociados**.
5. Accedemos a los detalles del VNIC pulsando en el enlace con el nombre de la instancia que aparece seguido de *(VNIC primario)*.
6. Una vez en los detalles, pulsa en **Direcciones IP**. Veremos que hay asignada una dirección IP.
7. Pulsamos el menú **...** a la derecha de los datos de la IP asignada, y después en **Editar**.
8. En el apartado **Dirección IP pública** eligiremos **IP pública reservada** y, más abajo, seleccionamos la IP que acabas de reservar para esta instancia.
9. Una vez pulses en **Actualizar**, ya estará asociada la IP permanente.

### Conectarse a la instancia

Para acceder a la máquina que acabamos de levantar, solo necesitarás la clave privada y la IP que acabamos de asociar (nota: volver a entrar en **Recursos informáticos > Instancias** y ver la IP Pública asociada al nombre de nuestra instancia creada).

{{% tabs %}}

{{% tab "Terminal" %}}
Abrimos un terminal nuevo en Linux/Mac, hacemos `ssh -i <fichero_clave_privada> ubuntu@xxx.xxx.xxx.xxx` (en caso de que la instancia utilice una distribución que no sea Ubuntu, hay que usar el usuario que corresponda).

Nota: el `fichero_clave_privada` es el llamado **oracle_key.ppk**. :key:

```bash
# Ejemplo. IP NO válida
ssh -i oracle_key.ppk ubuntu@132.145.224.211
```

Si todo está correctamente creado, tendremos acceso a un terminal que vamos a necesitar a continuación.
{{% /tab %}}

{{% tab "Putty" %}}
Desde **Putty** en Windows, nos conectamos a la IP (en _Host name_ en putty)

En el lateral izquierdo, seleccionamos las opciones: **Connection > SSH > Auth**.

En la sección llamada _Private key for authentication_, importamos la clave llamada `oracle_putty.ppk`. :key:

Una vez realizado dichos pasos, damos a `Open`, para abrir la conexión, y damos a que `Sí` para guardar el `key fingerprint`.

Si todo está correctamente, tendremos acceso a un terminal que vamos a necesitar a continuación.
{{% /tab %}}

{{% tab "MobaXterm" %}}
Desde **MobaXterm** en Windows, nos conectamos a la IP (en _Host name_ en MobaXterm)

En el lateral izquierdo, seleccionamos la sesión, hacemos click derecho sobre la sesión a conectarme, y pulsamos en `Edit session`.

Vamos a la pestaña: **SSH > Advanced SSH Settings > Use private key**. Marcamos la casilla, buscamos e importamos la clave llamada `oracle_putty.ppk`. :key:

Una vez realizado dichos pasos, damos a `OK`, y hacemos doble click sobre la sesión para abrir la conexión, y damos a que `Sí` para guardar el `key fingerprint`.

Si todo está correctamente, tendremos acceso a un terminal que vamos a necesitar a continuación.
{{% /tab %}}

{{% /tabs %}}

### Asociar un espacio de almacenamiento

Por defecto, las instancias disponen de un disco de arranque suficiente para aplicaciones del sistema y software estándar. Si queremos utilizarlas para procesar datos masivos, necesitamos añadirle un almacenamiento específico de mayor tamaño.

* Accedemos al menú **Almacenamiento de bloques** y **Volúmenes en bloque** y pulsamos **Crear volumen en bloque**.
* Le damos un **nombre** al almacenamiento, que sea fácil de asociar a la instancia a la que vamos a asignárselo.
* Elegimos el **tamaño** del almacenamiento.
* Elegimos el **rendimiento del volumen** (en nuestro caso *Alto rendimiento*). El resto de parámetros, en principio, los podemos dejar por defecto.
* Pulsamos en **Crear volumen en bloque** y se comenzará a provisionar el almacenamiento.
* Volvemos a la instancia (**Recursos informáticos**, **Instancias**, nombre de la instancia) y bajamos hasta el menú **Recursos** para abrir **Volúmenes en bloque asociados**.
* Aquí pulsamos en el botón **Asociar volúmenes en bloque**.
* **Elegimos el volumen** recién creado, seleccionamos de la opción **Ruta de acceso al dispositivo:** `/dev/oracleoci/oraclevdb`. Finalmente, pulsamos en el botón **Asociar**.

{{% alert title="Importante" color="error" %}}

Cuando haya terminado de crear la asociación, ejecute los comandos iSCSI del volumen en bloque con las herramientas del sistema operativo para conectarse y activar el volumen en bloque. Tenga en cuenta que si decide agregar este volumen a /etc/fstab, debe incluir las opciones _netdev y nofail. Si no lo hace, la instancia no se podrá iniciar en el futuro.

{{% /alert %}}

Esto lo veremos justo a continuación en el punto 1.

### Acceder al volumen desde el sistema operativo

Si hemos conectado el volumen mediante el protocolo *iSCSI*, el sistema operativo solo será capaz de conectarse cuando le especifiquemos cómo acceder a este a través de la red.

1. Dentro de nuestra instancia, y dentro de la sección: `Volúmenes en bloque asociados`, pichamos en el lateral derecho los 3 puntos **...**, para desplegar y seleccionar la opción: **Comandos e información de iSCSI**.
2. En este hay un apartado **Comandos de asociación**, **copiamos los comandos** que aparecen en él. Si más adelante necesitamos desconectar esta unidad permanentemente, usaremos los comandos que aparecen más abajo para desasociarla.
3. En el terminal que abrimos **pegamos los comandos** para asociar el dispositivo de almacenamiento al sistema.

```bash
# Ejemplo de salida:  NO copiar dichos comandos.

ubuntu@hadoop-3:~$ sudo iscsiadm -m node -o new -T iqn.2015-12.com.oracleiaas:3d5e8354-1f2e-4e75-9872-4bb72ed22fd6 -p 169.254.2.2:3260
New iSCSI node [tcp:[hw=,ip=,net_if=,iscsi_if=default] 169.254.2.2,3260,-1 iqn.2015-12.com.oracleiaas:3d5e8354-1f2e-4e75-9872-4bb72ed22fd6] added

ubuntu@hadoop-3:~$ sudo iscsiadm -m node -o update -T iqn.2015-12.com.oracleiaas:3d5e8354-1f2e-4e75-9872-4bb72ed22fd6 -n node.startup -v automatic

ubuntu@hadoop-3:~$ sudo iscsiadm -m node -T iqn.2015-12.com.oracleiaas:3d5e8354-1f2e-4e75-9872-4bb72ed22fd6 -p 169.254.2.2:3260 -l
Logging in to [iface: default, target: iqn.2015-12.com.oracleiaas:3d5e8354-1f2e-4e75-9872-4bb72ed22fd6, portal: 169.254.2.2,3260] (multiple)
Login to [iface: default, target: iqn.2015-12.com.oracleiaas:3d5e8354-1f2e-4e75-9872-4bb72ed22fd6, portal: 169.254.2.2,3260] successful.
```

* A continuación, vamos a particionar el nuevo dispositivo. Utilizaremos el comando `sudo fdisk /dev/sdb` (**Cuidado**: según el tipo de instancia creada o si ya existen más discos asociados, puede que la ruta al dispositivo sea otra).

```bash
ubuntu@hadoop-3:~$ sudo fdisk /dev/sdb

Welcome to fdisk (util-linux 2.31.1).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.
```

* Dentro del editor de particiones, usamos el comando **p** seguido de *Enter* para asegurarnos de que es un disco nuevo (no existen particiones).

```bash
Device does not contain a recognized partition table.
Created a new DOS disklabel with disk identifier 0xc839b2e7.

Command (m for help): p

Disk /dev/sdb: 1 TiB, 1099511627776 bytes, 2147483648 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 1048576 bytes
Disklabel type: dos
Disk identifier: 0xc839b2e7
```

* Escribimos el comando **n** seguido de *Enter* para crear una nueva partición primaria. Los valores por defecto asignarán a esta todo el espacio disponible.

```bash
Command (m for help): n
Partition type
   p   primary (0 primary, 0 extended, 4 free)
   e   extended (container for logical partitions)
Select (default p): p
Partition number (1-4, default 1): 1
First sector (2048-2147483647, default 2048):
Last sector, +sectors or +size{K,M,G,T,P} (2048-2147483647, default 2147483647):

Created a new partition 1 of type 'Linux' and of size 1024 GiB.
```

* Una vez que termines, escribe **w** y *Enter* para guardar la tabla de particiones en el disco.

```bash
Command (m for help): w
The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.
```

* De vuelta en el shell, escribimos `sudo mkfs.ext4 /dev/sdb1` para crear el sistema de archivos (**Cuidado**: si el disco no es */dev/sdb*, la ruta será otra).

```bash
ubuntu@hadoop-3:~$ sudo mkfs.ext4 /dev/sdb1

mke2fs 1.44.1 (24-Mar-2018)
Creating filesystem with 268435200 4k blocks and 67108864 inodes
Filesystem UUID: 52d43007-daaa-4a2b-8865-c8035f31bcf7
Superblock backups stored on blocks:
        32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
        4096000, 7962624, 11239424, 20480000, 23887872, 71663616, 78675968,
        102400000, 214990848

Allocating group tables: done
Writing inode tables: done
Creating journal (262144 blocks): done
Writing superblocks and filesystem accounting information: done
```

* Creamos una carpeta para el montaje: `sudo mkdir /opt/data` y montamos el disco en ella `sudo mount /dev/sdb1 /opt/data`.

```bash
ubuntu@hadoop-3:~$ sudo mkdir /opt/data

ubuntu@hadoop-3:~$ sudo mount /dev/sdb1 /opt/data
```

* Comprobamos que el disco está montado y tiene el tamaño correcto con **df -h**.

```bash
# Última línea

ubuntu@hadoop-3:~$ df -h
Filesystem      Size  Used Avail Use% Mounted on
udev             15G     0   15G   0% /dev
tmpfs           3.0G  964K  3.0G   1% /run
/dev/sda1        45G  977M   45G   3% /
tmpfs            15G     0   15G   0% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
tmpfs            15G     0   15G   0% /sys/fs/cgroup
/dev/sda15      105M  3.6M  101M   4% /boot/efi
/dev/loop0       92M   92M     0 100% /snap/core/8689
/dev/loop1       20M   20M     0 100% /snap/oracle-cloud-agent/6
tmpfs           3.0G     0  3.0G   0% /run/user/1001
/dev/sdb1      1007G   77M  956G   1% /opt/data
```

* Ahora, vamos a hacer que el disco se monte de forma automática al iniciarse el sistema operativo. De lo contrario, cada vez que la instancia se reinicie será necesario hacerlo manualmente. Necesitamos obtener el id del disco, por lo que hacemos `sudo blkid`.

```bash
ubuntu@hadoop-3:~$ sudo blkid

/dev/sda1: LABEL="cloudimg-rootfs" UUID="f4c837ad-72bf-4d7d-be48-e7b9c03555e8" TYPE="ext4" PARTUUID="84a56eaf-209e-49ca-8929-3011e90771b7"
/dev/sda15: LABEL="UEFI" UUID="6AB0-95A5" TYPE="vfat" PARTUUID="7cc3347c-404a-488b-8023-300bd67fe4ca"
/dev/loop0: TYPE="squashfs"
/dev/loop1: TYPE="squashfs"
/dev/sda14: PARTUUID="1060def6-8bc6-4b7d-a940-d28daab3cba0"

# Nos centramos en esta última línea
/dev/sdb1: UUID="52d43007-daaa-4a2b-8865-c8035f31bcf7" TYPE="ext4" PARTUUID="c839b2e7-01"
```

* Esta orden nos dará una lista de los discos conectados, localizamos la línea correspondiente al que estamos asociando: `/dev/sdb1: UUID="52d43007-daaa-4a2b-8865-c8035f31bcf7" TYPE="ext4" PARTUUID="c839b2e7-01"` y copiamos la parte que necesitamos **UUID=numeros-letras-numeros....** ejemplo: `UUID="52d43007-daaa-4a2b-8865-c8035f31bcf7"`.

```bash
/dev/sdb1: UUID="52d43007-daaa-4a2b-8865-c8035f31bcf7" TYPE="ext4" PARTUUID="c839b2e7-01"
```

* Ya podemos editar el archivo */etc/fstab* con `sudo vi /etc/fstab` (también se puede usar *nano* o cualquier otro editor) e incluimos una línea al final usando el id que acabamos de obtener, el punto de montaje y otros parámetros: `UUID="52d43007-daaa-4a2b-8865-c8035f31bcf7" /opt/data ext4 rw,_netdev 0 0`. El parámetro *_netdev* es muy importante: le indica al sistema que debe de esperar a que haya conexión de red para montar este recurso.
* Importante: si no está instalado vim en el servidor de ubuntu, lanzar los siguientes comandos:

```bash
# Si da error al usar Vim
ubuntu@hadoop-3:~$ sudo vi /etc/fstab
sudo: vi: command not found

# Actualizamos paquetes
ubuntu@hadoop-3:~$ sudo apt-get update

# Instalamos vim en servidor ubuntu
ubuntu@hadoop-3:~$ sudo apt-get install vim
# y le decimos que Sí (Y)
```

```bash
#sudo vi /etc/fstab
ubuntu@hadoop-3:~$ sudo vi /etc/fstab
LABEL=cloudimg-rootfs   /        ext4   defaults        0 0
LABEL=UEFI      /boot/efi       vfat    defaults        0 0

# CLOUD_IMG: This file was created/modified by the Cloud Image build process
######################################
## ORACLE CLOUD INFRASTRUCTURE CUSTOMERS
##
## If you are adding an iSCSI remote block volume to this file you MUST
## include the '_netdev' mount option or your instance will become
## unavailable after the next reboot.
## SCSI device names are not stable across reboots; please use the device UUID
## instead of /dev path.
##
## Example:
## UUID="94c5aade-8bb1-4d55-ad0c-388bb8aa716a" /data1 ext4 defaults,noatime,_netdev 0 2
##
## More information:
## https://docs.us-phoenix-1.oraclecloud.com/Content/Block/Tasks/connectingtoavolume.htm
##

# linea nueva a incluir según el UUID único
UUID="52d43007-daaa-4a2b-8865-c8035f31bcf7" /opt/data ext4 rw,_netdev 0 0

```

* Salimos guardando Vim pulsando los dos puntos, y escribiendo
  
```bash
# Salir y guardar en Vim
:wq!
```

* Comprobamos que se ha guardado correctamente el fichero con el nuevo **UUID** con `cat /etc/fstab`:

```bash
ubuntu@hadoop-3:~$ cat /etc/fstab

LABEL=cloudimg-rootfs   /        ext4   defaults        0 0
LABEL=UEFI      /boot/efi       vfat    defaults        0 0

# UUID único
UUID="52d43007-daaa-4a2b-8865-c8035f31bcf7" /opt/data ext4 rw,_netdev 0 0
```

* Finalmente, la instancia ya estaría lista para usar. Enhorabuena! :tada:
