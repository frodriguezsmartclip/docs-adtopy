---
title: "Abrir un Puerto"
linkTitle: "Abrir un Puerto"
description: "Abrir un Puerto en Oracle Cloud."
weight: 2
---

## Abrir un puerto

Pasos a seguir para que un **puerto abierto en una instancia esté accesible públicamente desde Internet**.

### Crear la regla

Para permitir el acceso a través de un puerto:

* Abrir **Red** > **Redes virtuales**.
* Elegir la red que se quiere editar.
* Abrir el apartado **Listas de seguridad** y pulsar en **Agregar reglas de entrada**.
* Poner el origen *0.0.0.0/0* para permitir cualquier origen (o la red y máscara que corresponda).
* Elegir el protocolo, normalmente **TCP**.
* En puertos de origen, por defecto lo dejamos en blanco.
* Los puertos de destino se pueden configurar como un único puerto o un rango, separado por guión. Normalmente, se especificará un solo puerto.
* Si queremos, podemos poner una descripción del uso de esta regla.
* Pulsamos en **Agregar reglas de entrada** y ya está creada la regla.

### Desactivar el firewall de Ubuntu (oracle cloud)

Si no lo hemos hecho antes, es necesario permitir el acceso por este puerto o, directamente, permitir el acceso a todos los puertos.

Para ello, nos logueamos dentro de la instancia que queremos abrir el puerto y creamos un script llamado `flushIpTables.sh`

```bash
ubuntu@hadoop-3:~$ vim flushIpTables.sh

ubuntu@hadoop-3:~$ cat flushIpTables.sh
# CONTENIDO A COPIAR

#!/bin/sh
iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT
iptables -t nat -F
iptables -t mangle -F
iptables -F
iptables -X
```

Importante darle permisos de ejecución:

```bash
ubuntu@hadoop-3:~$ chmod u+x flushIpTables.sh

ubuntu@hadoop-3:~$ ls -la flushIpTables.sh
-rwxrw-r-- 1 ubuntu ubuntu 154 Mar 30 11:18 flushIpTables.sh
```

Si intentamos ejecutarlo sin ser `root`, dará un error:

```bash
ubuntu@hadoop-3:~$ ./flushIpTables.sh
iptables v1.6.1: can't initialize iptables table `filter': Permission denied (you must be root)
Perhaps iptables or your kernel needs to be upgraded.
iptables v1.6.1: can't initialize iptables table `filter': Permission denied (you must be root)
Perhaps iptables or your kernel needs to be upgraded.
iptables v1.6.1: can't initialize iptables table `filter': Permission denied (you must be root)
Perhaps iptables or your kernel needs to be upgraded.
iptables v1.6.1: can't initialize iptables table `nat': Permission denied (you must be root)
Perhaps iptables or your kernel needs to be upgraded.
iptables v1.6.1: can't initialize iptables table `mangle': Permission denied (you must be root)
Perhaps iptables or your kernel needs to be upgraded.
iptables v1.6.1: can't initialize iptables table `filter': Permission denied (you must be root)
Perhaps iptables or your kernel needs to be upgraded.
iptables v1.6.1: can't initialize iptables table `filter': Permission denied (you must be root)
Perhaps iptables or your kernel needs to be upgraded.
```

Para ello, es necesario ejecutarlo de alguna de las siguientes formas:

```bash
# Forma 1: son comando sudo delante
ubuntu@hadoop-3:~$ sudo ./flushIpTables.sh

# Forma 2: convirtiendonos en sudo y ejecutandolo
ubuntu@hadoop-3:~$ sudo su
root@hadoop-3:/home/ubuntu# ./flushIpTables.sh
```
