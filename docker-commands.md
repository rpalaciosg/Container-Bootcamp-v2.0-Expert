# Docker commands

`docker build` -> crea una imagen de docker
`docker pull` -> jala o trae una imagen de docker registry
`docker run` -> corre o ejecuta un contenedor
`docker run -i -t ubuntu /bin/bash` -> (hace un create y un start) corre un contenedor ubuntu con terminal interactiva y ejecuta dentro el comando bash
`docker create` -> crea contenedor
`docker start` -> inicia contenedor
`docker container run -i -t ubuntu /bin/bash` -> es un comando mas especifico al api de container
`docker ps`-> muestra los que están corriendo y están activos.
`docker ps -a`-> muestra los contenedores existentes que están corriendo o no y no han sido eliminados
`docker ps -a | grep beaver` -> esto muestra los contenedores pero
`docker exec` -> inicia contenedores que esta corriendo.
`docker start` -> inicia contenedor que esta detenido
`docker images | grep `


`docker stop [nombre-contenedor]` -> detener el contenedor.

`docker rm contenedor` -> quita completamente borra el contenedor
`docker rmi image ` -> elimina una o mas imágenes
`docker run -rm -t ubuntu` -> esta bandera -rm cuando se detenga lo va a quitar/borrar complemtamente.

`docker run --rm -d nginx:1.7` -> cuando usa la bandera -d corre contenedor en modo demonio
`docker image -a` -> lista las imagenes
`docker logs contenedor` -> muestra loslogs o mensajes de mi contenedor si corri en modo detach
`docker stats hello --no-stream` -> estadisticas
`dokcer container run --help`-> muestra las ayuda de los comandos de docker
`docker commit -m "instale make y gcc" [nombre-contenedor] [nombre-imagen-a-crear]` ->esto toma un snapshot

`docker network inspect` -> mostrar redes
`docker attach`

# docker compose commands
`docker-compose build`