# Dia 2

Como detener un contenedor? Hay que pensar como se inicio:
Si hago un `docker stop [nombre-contenedor]` -> detener el contenedor, esto envia un #SIGTERM es kill mata con gracia, gracefull shutdown.
Si hago un `docker ps -a | grep beaver` -> esto muestra los contenedores pero 
`docker ps --no-trunk`

Ctrl + C -> #SIGINT en linux es como hacer un kill -9

`docker rm contenedor` -> quita completamente el contenedor
`docker run -rm -t ubuntu` -> esta bandera -rm cuando se detenga lo va a quitar complemtamente.

## Maneras de iniciar contenedores
Ahora estoy iniciando de esta forma usando la bandera '-it', la terminal se queda colgada, en linux se conoce como que mi terminal se queda foreground.

Lo que quiero es que el contenedor se quede corriendo, para esto puedo usar la bandera '-d' que significa modo daemon o detach.

`docker run --rm -d nginx:1.7`

El nombre de la imagen es distinto al nombre del contenedor.

`docker logs contenedor` -> muestra loslogs o mensajes de mi contenedor si corri en modo detach

`docker stats hello --no-stream` -> estadisticas

`dokcer container run --help`-> muestra las ayuda de los comandos de docker

## Workflow

El workflow es idempotente, que no importando en el tiempo siempre va a devolver el mismo resultado, que cuando yo corra docker build sea idempotente el proceso.

El resultado de build ES UN DOCKER IMAGE, que es un binario, y mediante un docker image puedo compartir mi aplicación.
Yo describo mi ambiente con docker file, y pueso instanciar uno o mas contenedores porque vienen de la misma imagen.

## Lboratorio de katakoda.
https://katacoda.com/kontinu/courses/docker-bootcamp-fundamentals/docker-build


## Dockerfile Tips

- Entender el build context, son todos los archivos que están al mismo nivel que el docker file. Es importante porque docker es una arquitectura cliente servidor. Cada vez que construimos una imagen, toma el contexto y el cliente lo envía comprimido al daemon.

Por eso h ay que determiar que se necesitan en mi imagen.

- Usar .dockerignore
Existe un archivo `.dockerignore` usa el mismo formato que un .gitignore

```.dockerignore

```

- Usar multi-stage-builds de ser posible
- No instalar archivos o paquetes innecesarios
- Desacoplar aplicaciones, en cuanto un contenedor debe tener uno y un solo proposito. (Debe correr una sola app)
- Minizar cantidad de capas (RUN, COPY, ADD las crean)
- Ordenar A-Z multilines "&& \" los comandos en RUN
- Aprovechar y entender el build cache, asi

## Ejercicio katacoda
[katakoda](https://katacoda.com/kontinu/courses/docker-bootcamp-fundamentals
)

## Truco que nos ensenia Marco
Nos ensenia a tomar una foto o hacer un snapshot a nuestro contenedor para seguir trabajando dentro después, esto se traduce a una nueva imagen:
`docker commit -m "instale make y gcc" [id-o-nombre-contenedor] [nombre-imagen-a-crear]` ->esto toma un snapshot

`docker commit -m "instale make y gcc" ubuntu mi/snapshot:v0.1` 

Esto se puede usar por ejemplo cuando quiero probar instalar manualmente dentro de un contenedor ubuntu cosas y para no perder mi trabajo si es que llego a cerrar mi contenedor hago un commit en una nueva imagen. Esta imagen se guarda en /var/lib/docker que es donde se guardan las imagenes.

**Nota**: Hacer esto, es una mala practica, ya que aquí no se que instale o que descargue dentro del contenedor, es mejor reemplazar esto con el docker file.


## Vamos a dockerizar o convertir una app para que funcione con docker.

Entramos a la aplicacion que nos paso 'container-expert-scratch', luego podemos ejecutar el 'setup.sh' para crear el archivo '.env' o si no lo modificamos manualmente con nuestros datos. Esto si estoy en windows lo puedo usar git bash.

El lenguaje que ocupe de 'container-expert-scratch\src'. 
Si elejimos node debemos ver que es lo que necesitamos.

Como se que en docker hub es un repositorio que puedo confiar, en el url antes del usuario de docker hub debe haber un `/_/user-hub` para saber que es revisado.


Para compilar mi imagen desde el 'Dockerfile' uso:
`docker build -t -rm "rpalaciosg/nodejs:v0.1" .`

Correr mi app en node:
`docker run -it -p 9090:8080 nombre-imagen`

En nodejs 'pm2-docker' usa un manejador de procesos.

Para construir la de python:
`docker build -t -rm "rpalaciosg/python:v0.1" .`
Correr mi app de python:
`docker run -it -p 9091:8080 nombre-imagen`

Con esto podemos tener multiples stage o ambientes de desarrollo.

## Continuos integration
Enlazar mi cuenta de github con docker hub
http://container-expert.kontinu.io/semana1/day1/d1.docker-ci.html

Nota: gitlab ci tiene un registry de docker y permite hacer CI gratis.

## docker compose

Cuando tenemos una app con una arquitectura microservicios. Us aun archivo YAML

Permite definir y declarar un ambiente completo.
YAML es un superset de python. Usa tabulaciones para separa las secciones.

Docker compose permite renderizas variables.

Podemos poner en google 'docker compose reference'

Creamos un archivo 'container-expert-scratch\docker-compose.yml'

docker compose lee los archivos .env

`docker-compose build`

Podemos pasarle 

PROJECT_LANG:-python
`PROJECT-LANG=-nodejs docker-compose build`
`PROJECT-LANG=-nodejs docker-compose build`

`docker-compose up` -> levanta
`docker-compose up -d` -> levanta como daemon
`docker-compose ps`
`docker-compose down` -> baja
`docker-compose up --build` -> compila antes y levanta

En ambiente local es recomendable usar siempre docker compose

Hay 2 tipos de volumenes:
- Name volumenes
- Bind volumenes


Docker compose reemplaza los comandos que tipearia con docker. Docker compose usa el docker file al momento de hacer un build.

Si quiero que mi contraseña no este en el docker-compose, puedo usar docker secrets.

## Como debuguear

`docker-compose logs`
`docker-compose logs python`