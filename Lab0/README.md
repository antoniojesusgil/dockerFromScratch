# Ediciones Docker
Dispone dos ediciones, Comunity Edition (CE) y Enterprise Edition (EE).

# Instalando docker CE
Docker está disponible para multiples plataformas, entre ellas Windows, Unix (Mac) y la gran mayoría de distribuciones linux. 
Visita la [web oficial](https://docs.docker.com/install/#supported-platforms) para conocer las disponibles.

### Crea una cuenta y registrate en [docker.com](https://store.docker.com/signup?next=%2Feditions%2Fcommunity%2Fdocker-ce-desktop-windows%3Ftab%3Dreviews)

### Windows
Visita la web oficial y [descarga Docker Community Edition](https://store.docker.com/editions/community/docker-ce-desktop-windows)

### Mac
Visita la web oficial y [descarga Docker Community Edition](https://store.docker.com/editions/community/docker-ce-desktop-mac)

### Linux
Las distribuciones linux disponen de varios métodos de instalación, los más utilizados son mediante los repositorios oficiales o descargando el paquete correspondiente e instalando manualmente.

### Cloud
Docker está disponible en los clouds de AWS y Azure.

---
# Docker CLI

Conceptos en este ejercicio:
* Docker engine
* Contenedores & Imagenes
---

Explorar comandos tanto de gestión como de servicio (imágenes y contenedores)

### 1. Ejecuta docker
```sh
docker
```
### 2. Ejecutando nuestro primer contenedor
Escribe o copia el código para ejecutar tu primer contenedor Docker:
```.term1
docker container run hello-world
```
### 3. Imágenes

Vamos a descargar una versión ligera de linux Alpine. Ejecutaremos en un terminal:
```sh
docker image pull alpine
```
El comando `pull` recupera la imagen Alpine del registro oficial de Docker y la guarda en nuestro sistema.

Ahora disponemos de imagenes en nuestro docker local. Podemos usar el comando `docker image` para ver un listado completo de las imágenes en nuestro sistema.

```
docker image ls
```
```
REPOSITORY              TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
alpine                 latest              c51f86c28340        4 weeks ago         1.109 MB
hello-world             latest              690ed74de00f        5 months ago        960 B
```

### 4. Docker Container Run
Vamos a ejecutar un **contenedor** Docker basado en la imagen alpine usando el comando `docker container run`

```
docker container run alpine ls -l
```
 
Ejecuta 
```
docker container run alpine echo "curso docker from scratch"
```

y este otro
```
cat /etc/alpine-release
```
Acabamos de ver la manera de poder pasarle parámetros al contenedor para su ejecución

### 5. Modo Interactivo

Ejecuta 
```
docker container run alpine /bin/sh
```
¿Qué ha ocurrido? Al no haber suministrado ningún otro comando adicional, ha sido ejecutada una instancia del contenedor sobre la cual una shell ha ejecutado el comando `/bin/sh`, la misma ha sido terminada y ha parado y finalizado el contenedor, es decir, hemos provocado una ejecución completa del ciclo de vida.

Docker nos facilita la posibildad de tener una shell interactiva sobre la cual se pueden escribir comandos, ejecuta
```docker
docker container run -it alpine /bin/sh
```
Prueba a ejecutar los siguientes comandos dentro de la shell `ls -l`, `uname -a`. Para salir del contenedor escribir el comando `exit`.

Lista los contenedores en ejecución.
