---
title: "Sintaxis Docker"
linkTitle: "Sintaxis Docker"
description: "Sintaxis de Docker en Oracle Cloud."
weight: 2
---

Usar **docker** consiste en pasarle una **cadena de opciones y comandos seguidos de argumentos**. La **sintaxis** sería la siguiente:

```bash
# Sintaxis de Docker
docker [option] [command] [arguments]
```

Para ver **todos los comandos disponibles de Docker**, escribe:

```bash
# comandos disponibles de Docker
ubuntu@hadoop-3:~$ docker
```

### Usage

```bash
Usage:  docker [OPTIONS] COMMAND

A self-sufficient runtime for containers

Options:
      --config string      Location of client config files (default "/home/ubuntu/.docker")
  -c, --context string     Name of the context to use to connect to the daemon (overrides DOCKER_HOST env var and default context set with
                           "docker context use")
  -D, --debug              Enable debug mode
  -H, --host list          Daemon socket(s) to connect to
  -l, --log-level string   Set the logging level ("debug"|"info"|"warn"|"error"|"fatal") (default "info")
      --tls                Use TLS; implied by --tlsverify
      --tlscacert string   Trust certs signed only by this CA (default "/home/ubuntu/.docker/ca.pem")
      --tlscert string     Path to TLS certificate file (default "/home/ubuntu/.docker/cert.pem")
      --tlskey string      Path to TLS key file (default "/home/ubuntu/.docker/key.pem")
      --tlsverify          Use TLS and verify the remote
  -v, --version            Print version information and quit
```

### Management commands

```bash
Management Commands:
  builder     Manage builds
  config      Manage Docker configs
  container   Manage containers
  context     Manage contexts
  engine      Manage the docker engine
  image       Manage images
  network     Manage networks
  node        Manage Swarm nodes
  plugin      Manage plugins
  secret      Manage Docker secrets
  service     Manage services
  stack       Manage Docker stacks
  swarm       Manage Swarm
  system      Manage Docker
  trust       Manage trust on Docker images
  volume      Manage volumes
```

### Comandos

La lista completa de los **comandos disponibles** para _Docker 19_ es la siguiente:

```bash
Commands:
  attach      Attach local standard input, output, and error streams to a running container
  build       Build an image from a Dockerfile
  commit      Create a new image from a container's changes
  cp          Copy files/folders between a container and the local filesystem
  create      Create a new container
  deploy      Deploy a new stack or update an existing stack
  diff        Inspect changes to files or directories on a container's filesystem
  events      Get real time events from the server
  exec        Run a command in a running container
  export      Export a container's filesystem as a tar archive
  history     Show the history of an image
  images      List images
  import      Import the contents from a tarball to create a filesystem image
  info        Display system-wide information
  inspect     Return low-level information on Docker objects
  kill        Kill one or more running containers
  load        Load an image from a tar archive or STDIN
  login       Log in to a Docker registry
  logout      Log out from a Docker registry
  logs        Fetch the logs of a container
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  ps          List containers
  pull        Pull an image or a repository from a registry
  push        Push an image or a repository to a registry
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  rmi         Remove one or more images
  run         Run a command in a new container
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  search      Search the Docker Hub for images
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  version     Show the Docker version information
  wait        Block until one or more containers stop, then print their exit codes

# Importante para aprender más sobre un comando en concreto.
Run 'docker COMMAND --help' for more information on a command.
```

### Info total sobre Docker

Si deseamos ver la **información sobre Docker de todo el sistema**, lanzar el comando vía terminal:

```bash
sudo docker info
```

Salida de ejemplo:

```bash
ubuntu@hadoop-3:~$ sudo docker info

Client:
 Debug Mode: false

Server:
 Containers: 7
  Running: 6
  Paused: 0
  Stopped: 1
 Images: 9
 Server Version: 19.03.8
 Storage Driver: overlay2
  Backing Filesystem: <unknown>
  Supports d_type: true
  Native Overlay Diff: false
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
 Swarm: inactive
 Runtimes: runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 7ad184331fa3e55e52b890ea95e65ba581ae3429
 runc version: dc9208a3303feef5b3839f4323d9beb36df0a9dd
 init version: fec3683
 Security Options:
  apparmor
  seccomp
   Profile: default
 Kernel Version: 5.0.0-1013-oracle
 Operating System: Ubuntu 18.04.4 LTS
 OSType: linux
 Architecture: x86_64
 CPUs: 4
 Total Memory: 29.44GiB
 Name: hadoop-3
 ID: AII7:Q4VO:EJPW:O3IH:7CQH:2666:SCQM:LHSD:LFMQ:7IRA:3RMR:SZ2F
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Registry: https://index.docker.io/v1/
 Labels:
 Experimental: false
 Insecure Registries: 127.0.0.0/8
 Live Restore Enabled: false

WARNING: No swap limit support
```

### Hello-world docker

Para verificar si puedes acceder y descargar imágenes desde **Docker Hub**, escribe en la terminal de la instancia:

```bash
sudo docker run hello-world
```

El resultado te indicará que Docker está funcionando correctamente. Salida:

```bash
ubuntu@hadoop-3:~$ sudo docker run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

Los contenedores Docker se forman a partir de imágenes de Docker. De forma predeterminada, Docker extrae estas imágenes de [Docker Hub](https://hub.docker.com/), un registro de Docker administrado por Docker, la empresa responsable del proyecto Docker. Cualquier persona es capaz de alojar sus imágenes Docker en Docker Hub, por lo tanto, la mayoría de las aplicaciones y distribuciones de Linux que se necesiten, tendrán las imágenes alojadas ahí mismo.

**¡¡Enhorabuena!!** Has lanzado un docker de ejemplo y aprendido sobre el uso y comandos de Docker :tada: smile:
