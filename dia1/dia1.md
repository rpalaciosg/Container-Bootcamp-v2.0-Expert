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
- Cuando un container se crea o existe cuando se usa `docker run` es la combinación de 2 comandos `docker create` y `docker start` 

# Docker Core

En que esta cimentado docker para ser tan especial.

Este CLI a partir de la version 18.06, apareció el concepto de Management Commands.
Por ejemplo cuando hago docker run, es exactamente igual si hiciera `docker container run`, docker empezo a tener tantos comandos que era muy dificil identificar.

`docker container run -i -t ubuntu /bin/bash` -> es un comando mas especifico al api de container
`docker run -i -t ubuntu /bin/bash`-> hace un create y un start

Cuando docker hace un `docker run` hace lo siguiente:
1. Si no enecuntra l imagen en registry local, hace un pull de docker hub o registry remoto.
2. Docker crea un nuevo contenedor con `docker create`
3. Docker allocate un filesystem:rw de lectura y escritura como capa final para que podamos escribir y leer de este sistema de archivos.
4. Docker crear  una interfaz virtual de red atachada a la red que docker le llama "default" (bridge es la red que usa docker para todos los contenedores), esto incluye dirección IP. 
5. Docker inicia el contenedor y ejecuta "/bin/bash" como un terminal interactiva. que son las bandera -i(interactive) -t(tty)
6. Cuando escribas "exit" o "ctrl+d" el contenedor se detendra pero no sera removido, puedes volver a iniciarlo.

Si yo hago un `docker network ls` -> lista las redes creadas por docker a los contenedores y podremos ver la red bridge que es la red default o por defecto que utiliza docker para todos los contenedores.

`docker top magical_leakey`-> dice los procesos que corren dentro del contenedor y lo mantienen vivo

`docker ps -a`-> muestra todos los contenedores que en algun momento corrriendo y ahora estaque están corriendo y no han sido eliminados
`docker exec` -> inicia contenedores que esta corriendo.
`docker start` -> inicia contenedor que esta detenido para iniciar

```
docker ps
```




## Repositorio para hacer fork
[para hacer fork](https://github.com/rpalaciosg/container-expert-scratch)