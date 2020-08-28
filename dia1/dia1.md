# Que es Docker? que hará por mi?

Permite acercarme a la infraestructura como código.
Se apoya en tecnología como LXC(Linux containers), esto a mejorado porque docker se hizo popular.
Docker es agnóstico al lenguaje.

# Docker: arquitectura

La arquitectura de docker es cliente servidor.

- El cliente de docker (Client docker CLI) se conecta al Servidor de docker, mediante REST API.
- En el nucleo tenemos el `docker daemon` o también conocido como `docker SERVER`, este se encarga de manejar todo lo que el cliente le diga.

> El cliente de docker puede estar en una maquina y el servidor en otra.

La manera usual de conectar docker es por linux sockets.

Cuando mi servidor esta remoto puedo conectarme via REST API y via sockets. Cuando un o configura el cliente ya es capaz de conectarse.
Con docker se pueden manejar volúmenes, para cosas que sean persistentes, como tal vez la app escribe un tipo de eventos o logs que deban permanecer independientemente si se reinicia el contenedor como un base de datos, un sistema de colas, o un sistema de caching.
También maneja y administra las imágenes, que imagen jala, la que es necesario volver a jalar.
También maneja los contenedores, que están corriendo.

Tambien es el encargado de manejar las redes.

Existen 3 conceptos grandes:
- Redes
- Imagenes
- Contenedores
- Volumenes

# Objetos Docker

Se les conoce como first class citicenz.
Objetos primarios de docker.

- Docker daemon: se encarga de generar y descargar imágenes, y los guarda en un Local registry.
- Las imágenes suceden a partir de un `docker build` y `docker pull`
- Cuando un container se crea o existe cuando se usa `docker run`

# Docker Core

En que esta cimentado docker para ser tan especial.

```docker run -i -t ubuntu /bin/bash``` -> hace un create y un start
`docker container run -i -t ubuntu /bin/bash` -> es un comando mas especifico al api de container
`docker top hungry_jones`-> dice los procesos que corren dentro del contenedor
`docker ps -a`-> muestra los que están corriendo y no han sido eliminados
`docker exec` -> inicia contenedores que esta corriendo.
`docker start` -> inicia contenedor que esta detenido para iniciar

```
docker ps
```

1. 
2. Docker crear  una interfaz virtual de red atachada a la red que docker le llama "default" (bridge es la red que usa docker para todos los contenedores), esto incluye dirección IP. 
3. Docker inicia el contenedor y ejecuta "/bin/bash" como un terminal interactiva.
4. Cuando escribas "exit"


## Repositorio para hacer fork
[para hacer fork](https://github.com/rpalaciosg/container-expert-scratch)