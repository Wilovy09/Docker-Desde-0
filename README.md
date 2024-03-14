# Docker desde 0

Seguramente has vivido que cuando tienes un proyecto que necesita distintas dependendencias y cuando lo quieres llevar a produccion o que otra persona lo ejecute "Oye pero en mi maquina si funcionaba", para esto sirve `Docker`, empaqueta todo en un `Contenedor` para evitar estos problemas.

## Indice

- [¿Qué es docker?](#qué-es-docker)
  - [¿Son máquinas virtuales?](#son-máquinas-virtuales)
  - [Alternativas](#alternativas)
  - [¿Porué usar docker?](#porqué-usar-docker)
  - [¿Cuando usar Docker?](#cuándo-usar-docker)
- [Instalación de Docker](#instalación-de-docker)
  - [Windows & Mac](#windows-y-mac)
  - [Linux](#linux)
- [Hola Mundo](#hola-mundo)
- [Docker Hub](#docker-hub)
- [Imágenes y Contenedores](#imágenes-y-contenedores)
  - [Descargar una imagen](#descargar-una-imagen)
  - [Ver imagenes descargadas](#ver-imagenes-descargadas)
  - [Crear contenedor](#crear-contenedor)
- [Etiquetas](#etiquetas)
- [Mapeo de Puertos](#mapeo-de-puertos)
- [Docker run](#docker-run)
  - [Docker run con puerto y nombre](#docker-run-con-puerto-y-nombre)
- [Docker logs](#docker-logs)
  - [Detalles](#detalles)
  - [En esucha](#en-escucha)
- [Environments](#environments)
- [Docker + springboot + postgresql](#docker--springboot--postgresql)
- [Dockerfile](#dockerfile)
- [Docker network](#docker-network)
- [Docker compose](#docker-compose)
- [Subiendo imágen a Docker Hub](#subiendo-imágen-a-docker-hub)
- [Comandos de Docker](#comandos-de-docker)
  - [Descargar una imagen](#descargar-una-imagen)
  - [Listar imagenes descargadas](#listar-imagenes)
  - [Crear un contenedor](#crear-un-contenedor)
  - [Activar un contenedor](#activar-un-contenedor)
  - [Ver contenedores activos](#ver-contenedores-activos)
  - [Ver todos los contenedores de tu computadora](#ver-todos-los-contenedores-de-tu-computadora)
  - [Eliminar un contenedor creado](#eliminar-un-contenedor-creado)
  - [Eliminar una imagen](#eliminar-una-imagen)
  - [Detener un contenedor](#detener-un-contenedor)
  - [Descargar imagen con etiqueta](#descargar-imagen-con-etiqueta)
  - [Eliminar imagen con etiqueta](#eliminar-imagen-con-etiqueta)
  - [Eliminar multiples imagenes](#eliminar-multiples-imagenes)
  - [Querys](#querys)
  - [Eliminar con querys](#eliminar-con-query)
  - [Crear contenedores más rapido](#crear-contenedores-más-rapido)
  - [Crear contenedores con nombre](#crear-contenederoes-con-nombre)
  - [Docker Run](#dockerrun)
    - [Con puerto y nombre](#con-puerto-y-nombre)
  - [Docker logs](#dockerlogs)
    - [Detalles](#detalles)
    - [En escucha](#en-escucha)
- [Recurso](#recurso)

## Qué es docker?

[Docker](https://www.docker.com/) es una plataforma de de software, empaqueta en contenedores para tener mas productividad y fácil administración.

### Son máquinas virtuales?

No, si bien docker trabaja con el kernel de linux no significa que tengamos las mismas opciones que instalando un linux en una computadora, tenemos solo una pequeño trozo de linux.

Docker esta diseñado para proporcionar una forma ligera y portatil de empaquetar y ejecutar aplicaciones en un entorno aislado y reproducible.

Docker pertenece a la empresa [Docker](https://www.linkedin.com/company/docker/?trk=public_profile_result-card_subtitle-click&originalSubdomain=mx).

### Alternativas

Una alternativa a docker es [Podman](https://podman.io/).

### Porqué usar Docker?

- Envio de software más rápido.
- Estandarización de operaciones.
- Ahorre de dinero.
- Tranferencia de manera sencilla de las aplicaciones.

### Cuándo usar Docker?

- Cuando tenemos una arquitectura orientada a [Microservicios](https://aws.amazon.com/es/microservices/#:~:text=Los%20microservicios%20son%20un%20enfoque,servicios%20son%20equipos%20peque%C3%B1os%20independientes.)
- Integración y entrega continua.
- Procesamiento de datos.
- Contenedores como servicio.

## Instalación de Docker

### Windows y Mac

Para instalar Docker en windows debemos intalar [Docker desktop](https://www.docker.com/products/docker-desktop/)

Si estamos en `Windows`:

- Seleccionamos `WSL 2`

> [!NOTE]
> En algunas configuraciones Docker necesitara que tengas activado el Hyper-V o la virtualización.

Una vez terminada la instalación, reiniciamos el ordenador.

### Linux

[Guía de instlación oficial](https://docs.docker.com/desktop/install/linux-install/)

## Hola Mundo

Abrimos la terminal y ejecutamos:

```sh
docker run hello-world
```

Esto nos mostrara algo asi

```txt
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

Si nos aparece eso, todo esta bien!

## Docker Hub

[Docker Hub](https://hub.docker.com/) es un lugar donde podremos encontrar distintas imagenes de personas y empresas de al rededor del mundo.

## Imágenes y Contenedores

Para entender esto debemos abrir [Docker Hub](https://hub.docker.com/) y buscar [Mongo](https://hub.docker.com/_/mongo), hacemos click en el resultado y nos aparecera un comando como este

### Descargar una imagen de Docker Hub

```sh
docker pull mongo
```

lo ejecutamos en nuestra terminal

Esto lo que hara sera checar si ya tenemos esta imagen descargada en nuestro ordenador, si no esta descargada la descargara.

Y a partir de esta imagen podremos crear contenedores.

### Ver imagenes descargadas

Para ver las imagenes que tenemos descargadas en nuestro ordenador, ejecutamos en una terminal:

```sh
docker images

# OUTPUT
# REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
# mongo         latest    79112eff9c89   13 days ago     756MB
# hello-world   latest    d2c94e258dcb   10 months ago   13.3kB
```

### Crear contenedor

Una vez verificado que tenemos la imagen descargada crearemos un contenedor.

Para lograr esto tenemos que ejecutar:

```sh
#                       NOMBRE DE LA IMAGEN
docker container create mongo

# OUTPUT
# af955acba00f2d1c68fd9f124bbf47e8af92b895b822b08a28778aad2cab54e9
```

Cuando ejecutemos esto nos dara un identificador, con este ejecutador podemos levantar la instancia de mongo. para esto ejecutamos

```sh
# No es necesario poner todo el identificador, basta con poner 4 caracteres en adelante
docker start af955a
```

Para verificar que nuestra instancia esta "viva", ejecutamos:

```sh
docker ps

# OUTPUT
# CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS          PORTS       NAMES
# af955acba00f   mongo     "docker-entrypoint.s…"   3 minutes ago   Up 12 seconds   27017/tcp   lucid_hopper
```

Y con esto ya creamos nuestro primer contenedor.

## Etiquetas

Las etiquetas sirven para definir que versión de imagen queremos descargar, cuando hacemos:

```sh
docker pull NOMBRE_DE_LA_IMAGEN
```

Por defecto usara la etiqueta ``:latest``

En este caso podemos ir a ver la [imagen de mongo a dockerhub](https://hub.docker.com/_/mongo) y ver que tiene un apartado de etiquetas

Para definir que etiqueta queremos descargar debemos usar ``:`` y ejecutarlo al momento de descargar la imagen.

```sh
#          IMAGEN:ETIQUETA
docker pull mongo:windowsservercore-ltsc2022
```

### Eliminar imagenes que tienen etiqueta

```sh
docker image rm IMAGEN:ETIQUETA
```

### Eliminar imagenes en una sola lina

```sh
docker rmi IMAGEN:ETIQUETA IMAGEN:ETIQUETA
```

### Eliminar imagenes sin necesidad de escribir cada una

Si nosotros hacemos:

```sh
docker images -q

# OUTPUT
# 79112eff9c89
```

Nos regresara un listado de las id de nuestras imagenes, pero nosotros queremos eliminarlas entonces hacemos:

```sh
docker rmi $(docker images -q)
```

Este comando eliminara a todas las ID que regresa el comando `docker images -q`

## Mapeo de Puertos

Seguramente si intentaste entrar a tu contenedor, en este caso a tu base de datos de mongo, no pudiste.

Y es porque aun no hemos expuesto el puerto para que podamos empezar a usarla.

```sh
docker create -p 27017:27017 --name mongodb mongo
```

Y listo con esto podremos empezar a establecer la conexion con nuestro contenedor.

## Docker run

```sh
docker run IMAGEN
```

Este comando ejecuta 3 pasos:

1. Busca la imagen y si no la encuentra la descarga
2. Crea el contenedor
3. Inicia el contenedor

### Docker run con puerto y nombre

```sh
#            PUERTO:DOCKER
docker run -p 27017:27017 --name NOMBRE -d IMAGEN
```

## Docker logs

Si queremos ver los logs del contenedor utilizamos:

```sh
docker logs IDENTIFICADOR
```

Y si queremos mas detalles:

```sh
dokcer logs IDENTIFICADOR --details
```

Y si queremos seguir el log conforme va sucediendo

```sh
docker logs --follow IDENTIFICADOR
```

Con el comando anterior, la terminar se queda "escuchando" y nos va diciendo que es lo que pasa

## Environments

Algunas imagenes van a requerir variables de entorno, para poner esta variavles de entorno usamos `-e`, esto significa que podemos agregar variables de entorno pre-establecidas.

En este caso podemos usar [Postgres](https://hub.docker.com/_/postgres) ya que esta db necesita variables de entorno.

```sh
docker run -p 5432:5432 --name postgredb -e POSTGRES_PASSWORD=123 -e POSTGRES_DB=demodb -d postgres
```

y listo ya con esto podemos conectarnos a nuestra base de datos postgres.

## Docker + springboot + postgresql

Para efectos practicos usaremos el repositorio del [video](https://youtu.be/rmty_WNvJvA?si=S-Vbc1ndoHxq00Ga&t=2595) de donde se esta sacando toda esta información.

> [!TIP]
> Recomiendo demaciado ver el video de donde se esta sacando todo los datos de este post.

- [Link del repo](https://github.com/mitocode21/dockerdesdecero.git)

Haremos un ``git clone``

```sh
git clone https://github.com/mitocode21/dockerdesdecero.git
```

Una vez terminado de clonar, eliminaremos los archivos:

- Dockerfile
- docker-compose.yml

Ya que la idea de esto es aprender docker, asi que los haremos por nosotros mismos.

## Dockerfile

> [!WARNING]
> TIENES QUE TENER INSTALADO [JAVA](https://youtu.be/L1oMLsiMusQ?si=yjkqaMCDOwKj3vJm) Y [MAVEN](https://youtu.be/1QfiyR_PWxU?si=fZcuq004uSP9GPCt) PARA PODER DOCKERIZAR ESTA APP


Ya sabemos descargar una imagen y generar contenedores con estas imagenes, pero ¿que pasa si quiero crear mi propia imagen? para asi generar los contenedores con ella.

A este proceso se le conoce como `Dockerizar`, para lograr esto debemos crear un archivo llamado ``Dockerfile`` en la raiz de nuestro proyecto.

Antes de poder dockerizar esta app tenemos que "buildearla" con el siguiente comando

```sh
mvn clean package
```

> [!WARNING]
> El nombre Dockerfile es obligatorio, no puedes usar el nombre que tu quieras.

> [!WARNING]
> Recuerda que el contenido que pondremos dentro de este archivo es porque vamos a dockerizar el repositorio que clonamos anteriormente, quiero decir que esto no sera asi siempre. El contenido de el archivo Dockerfile va a cambiar conforme cambie el proyecto.

Una vez creado nuestro archivo Dockerfile en la raiz de nuestro proyecto, vamos a escribir esto dentro de nuestro archivo

```dockerfile
# Aqui decimos desde openjdk
FROM openjdk:latest

# El autor es:
LABEL author="TUNOMBRE"

# Hacemos un copy de nuestra carpeta target/archivo y lo renombramos como app.jar
COPY target/springboot-docker-0.0.1-SNAPSHOT.jar app.jar

# Queremos que ejecutes estos comandos java -jar /app.jar
ENTRYPOINT [ "java", "-jar", "/app.jar" ]
```

Una vez tengamos este archivo ya generado vamos a ejecutar:

```sh
#                       NOMBRE:TAG
docker build -t springbootdemo:1 .
# El . significa que el archivo Dockerfile esta a la misma altura de donde ejecutamos el comando
```

Una vez terminado este proceso podemos ejecutar `docker images` para ver que nuestra imagen esta ahi.

## Docker network

En esta situacion necesitamos que ambos contenedores esten apuntando a un mismo lugar, para eso existe network

Ejecutamos:

```sh
docker network create NOMBRE
```

Y ya una vez creada nuestra network vamos a crear los contenedores

```sh
docker run -p 8080:8080 --name springbootcontainer -d --network=NOMBRE springbootdemo:1
```

```sh
docker run -p 5432:5432 --name postgredb -e POSTGRES_PASSWORD=123 -e POSTGRES_DB=demodb -d --network=NOMBRE postgres
```

## Docker compose

Para poder hacer esto debemos asegurarnos de que nuestro archivo `src/main/resources/application.properties` de nuestra app de springboot

Tenga estas variables de entorno

```s
spring.datasource.url=${DATABASE_URL}
spring.datasource.username=${DATABASE_USERNAME}
spring.datasource.password=${DATABASE_PASSWORD}
```

Y ahora en la raiz de nuestro proyecto vamos a crear un archivo con el nombre `docker-compose.yml` y agregamos lo siguiente

> [!WARNING]
> La identación en este archivo es muy importante

```yml
# Con esto le decimos que version de archivo usaremos
version: "3.8"
# declaramos los servicios
services:
  # a springboot le ponemos el nombre app
  app:
    # Que se guarde dentro de un contenedor llamado sbcontainer
    container_name: "sbcontainer"
    # Que tome lo que esta a su altura
    build: .
    # que use el puerto 8080:8080
    ports:
      - "8080:8080"
    # declaramos las variables de entorno
    environment:
      - DATABASE_URL=jdbc:postgresql://postgres_db:5432/demodb
      - DATABASE_USERNAME=postgres
      - DATABASE_PASSWORD=123
    # este contenedor tiene una dependencia al contenedor
    depends_on:
      - postgres_db

  # servicio llamado postgres_db
  postgres_db:
    # nombre del contenedor
    container_name: "postgres_db"
    # que descargue la imagen postgres
    image: "postgres"
    # que use el puerto 5432:5432
    ports:
      - "5432:5432"
    # variables de entorno
    environment:
      POSTGRES_USER: "postgres"
      POSTGRES_PASSWORD: "123"
      POSTGRES_DB: "demodb"
# aqui decimos que postgres-data necesita un volumen
volumes:
  postgres-data:
```

## Subiendo imágen a Docker Hub

Para poder subir una imagen a Docker Hub tenemos que crear una imagen usando nuestro usuario de dockerhub

```sh
# . es donde esta tu archivo Dockerfile
docker build TU_USUARIO/NOMBRE .
```

Una vez creada ejecutamos:

```sh
docker login
```

Si mo te has logeado en DockerDesktop te pedira tu usuario y contraseña de tu cuenta de Docker Hub

Ahora para subirla demos de:

```sh
docker push NOMBRE_DE_LA_IMAGEN_CREADA
```

## Comandos de docker

### Descargar una imagen

```sh
docker pull NOMBRE_DE_LA_IMAGEN
```

### Listar imagenes

```sh
docker images
```

### Crear un contenedor

```sh
docker container create NOMBRE_DE_LA_IMAGEN
```

### Activar un contenedor

```sh
docker start IDENTIFICADOR_O_NOMBRE
```

### Ver contenedores activos

```sh
docker ps
```

### Ver todos los contenedores de tu computadora

```sh
docker ps -a
```

### Eliminar un contenedor creado

```sh
docker rm IDENTIFICADOR_DEL_CONTENEDOR
```

### Detener un contenedor

```sh
docker stop IDENTIFICADOR_O_NOMBRE
```

### Eliminar una imagen

No nos permitira eliminar una imagen si es que hay algun contenedor usandola

```sh
docker rmi hello-world
```

### Descargar imagen con etiqueta

```sh
#          IMAGEN:ETIQUETA
docker pull mongo:windowsservercore-ltsc2022
```

### Eliminar imagen con etiqueta

```sh
docker image rm IMAGEN:ETIQUETA
```

### Eliminar multiples imagenes

```sh
docker image rm IMAGEN:ETIQUETA IMAGEN:ETIQUETA
```

### Querys

Esto regresa un listado de todas las ID de las imagenes que tenemos descargadas

```sh
docker images -q

# OUTPUT
# 79112eff9c89
```

### Eliminar con query

```sh
docker rmi $(docker images -q)
```

### Crear contenedores más rapido

```sh
docker create IMAGEN
```

### Crear contenederoes con nombre

```sh
docker create --name NOMBRE IMAGEN
```

### Crear contenedor con puerto expuesto

```sh
docker create -p 27017:27017 --name NOMBRE IMAGEN
```

Y listo con esto podemos conectarnos a nuestra base de datos de mongo.

Podemos usar algun gestor de bases de datos como:

- [Estudio 3T](https://studio3t.com/es/) especial para MongoDB.
- [Database Client JDBC](https://marketplace.visualstudio.com/items?itemName=cweijan.dbclient-jdbc), esta es una extension para VSCode que nos permite establecer conexiones a bases de datos.

### DockerRun

```sh
docker run IMAGEN
```

#### Con puerto y nombre

```sh
docker run -p 27017:27017 --name NOMBRE -d IMAGEN
```

### DockerLogs

```sh
docker logs IDENTIFICADOR
```

#### Detalles

```sh
dokcer logs IDENTIFICADOR --details
```

#### En escucha

```sh
docker logs --follow IDENTIFICADOR
```

### DockerNetworck

#### Crear

```sh
docker network create NOMBRE
```

#### Conectarse

```sh
docker run ... --network=NOMBRE ...
```

### aa

---

## Recurso

Toda la información de estas notas salio del Curso de docker desde 0 de MitoCode, para más detalles puedes visitar el link del video.

### Video

[Curso de Docker desde 0 | MitoCode](https://youtu.be/rmty_WNvJvA?si=HljJjG5W_vnrQGBu)
