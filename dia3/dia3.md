# dia 3

Docker compose se usa cuando tengo aplicaciones multicontenedores.

Docker compose se recomienda mas para los ambientes de desarrollo.

`docker-compose ps`
`docker-compose down --help`

Alguien hace la pregunta de si levanto 3 servicios con un docker compose y quiero solo bajar uno entonces hago un:
`docker-compose scale nodejs=0`-> escala hacia abajo
Vamos actualizar la imagen de mi "docker-compose.yml". cuando ya estoy en producción lo que hago es cambiar la imagen.
Si quiero volver a levantar el; contenedor

`docker-compose scale nodejs=1` -> escala hacia arriba los contenedores bajados en docker compose.
`docker-compose restart nodejs` -> reinicia el servidor, docker container tiene un comanado que se llama restart, reinicia el contenedor.

`docker-compose pull` -> jalar las imagenes

Debemos tener cuidado con docker compose porque es para desarollo y CI/CD
`docker-compose push`-> si ya estoy seguro que las imagenes en compose empuja a docker hub o a un repos privado

Si quisieramos escalar un mismo contenedor, como todos usan el mismo puerto, podemos usar un proxy.

PAra contrasenias, recomienda usar un vault de secretos, donde se pueda guardar las contrasenias para que las apps vayan a ver las contrasenias.
Varios archivos de configuracion, con docker compose podemos hacer esto.

## 12Factor apps

12factor.net
Las apps 12 factor tienen beneficios muy bonitos y se pueden usar las que nos convengan en un momento adecuado.
Si no se las hace a las 12 no se va a fallar. Podemos tomare las que consideremos.
Esta inspirado de Heroku que es una plataforma para plataforma como servicio y permite interactuar y publicar mis apps de manera sencilla, ye sta basado en 2 libros de MArtin Fowler que es PAtterns of enterprise application architecture y el libro Refactoring.

Es una metodologia para ahcer apps como si fueran apps como Software as a services que:
- Usan formatos declarativos para la automatizacion de la configuracion, para reducir costos y tiempos cuando un nuevo desarrollador se une.
- Tienen un contrato limpio y sencillo con el OS para ofrecer portabilidad entre ambientes.
- Estan hechas para ahcer "despliegue" a cualquier proveedor cloud.
- Minimizan la divergencia entre ambientes de desarrollo y produccion maximizando la agilidad por medio de continuos deployment.
- Escalan facilmente sin la necesidad de cambiar herramientas, ni arquitectura o alguna otra practica de desarrollo.

>> `advertencia` esta metodologia deberia servir para cualquier aplicación en cualquier lenguaje de programación y con cualquier serie de dependencias (DB, queue, cache, etc)

1. Codebase

2. Dependencies
  Declarar explicitamente y aislar dependencias
3. Config
4. Backing services
5. Build, release, run
6. Processes: Ejecutar la aplicacion como un solo proceso sin estado (stateless)
7. Port binding: Exponer servicios via port-binding
8. Concurrency
9. Disposability
10. Dev/prod parity
11. Logs
12. Admin processes

### 1. Codebase

## API Gateway
Se llama `traefik` el api gateway que vamos aprender hoy, hay tambien nginx, express-apigateway

Vamos a introducir traefic a nuestra app.

Vamos a crear un nuevo docker-compose file.

Lo nuevo que se agrego por ejemplo es el `restart: on-failure` significa que va a reiniciar siempre y cuando el exit code echo $? sea diferente de 0.

`docker-compose -f kontinu-compose.yml build`-> lee un archivo compose con otro nombre.
`docker-compose push`-> si quiero compartirlo a todos
`docker-compose up`-> para levantar
`docker-compose down`-> baja el docker-compose

## docker swarm
Orquestador de contenedores.
Funciona con nodos. Hay nodos tipo managers y nodos tipo workers.
### Featrues
- Viene instalado ya en docker engine
- Con el mismo docker compose vamos a migrarnos a docker swarn.
- La escalabilidad no viene activada por defecto.

### Conceptos

`docker swarn init`-> activar docker swarn