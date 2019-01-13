## Contenedores & Imágenes

### Isolation

Concepto de seguridad crítico en el mundo Docker! A pesar de que cada comando de ejecución del contenedor usaba la misma imagen `alpine`, cada ejecución era un contenedor separado y aislado. Cada contenedor tiene un sistema de archivos separado y se ejecuta en un espacio de nombres diferente; por defecto, un contenedor no tiene forma de interactuar con otros contenedores, incluso los de la misma imagen. 

Veamos un ejemplo práctico para aprender más sobre aislamiento, ejecuta:
```
docker container run -it alpine /bin/ash
```

En la shell interactiva escribe:
```sh
echo "Hello docker from scratch" > /home/hello.txt

ls /home
```

Sal del contenedor con `exit`.

Para ver como funciona el aislamiento, ejecuta:
```
docker container run alpine ls /home
```

Comprobamos que el fichero `hello.txt` no existe, esto es debido a que esta ejecución se ha realizado en una nueva instancia y por tanto separada.

La cuestión es, ¿Como recupero el contenedor que contiene el archivo `hello.txt`?

Ejecutemos

```
docker container ls -a
```
```
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                      PORTS               NAMES
36171a5da744        alpine              "ls"                     2 minutes ago       Exited (0) 2 minutes ago                        distracted_bhaskara
3030c9c91e12        alpine              "/bin/ash"               5 minutes ago       Exited (0) 2 minutes ago                        fervent_newton
```

### Comando `start`
Localiza el ID del contenedor sobre el cual creaste el fichero `hello.txt` y ejecuta:
```
docker container start <container ID>
```
Haz un listado de los contenedores en ejecución.

### Comando `exec`
Para poder enviar comandos a contenedores en ejecución disponemos del comando `exec`, ejecuta:

```
docker container exec <container ID> ls
```

### Ejercicios
1. Descarga la imagen oficial de `ubuntu` y ejecuta en un contenedor interactivo una shell `bash`
2. Crea un fichero en el contenedor, puedes usar el comando `echo`o `touch`
3. Muestra los contenedores en ejecución usando los comandos `docker container`y `docker ls`
4. Muestra todos los contenedores tanto en ejecución como parados
5. Para el contenedor `ubuntu`
6. Arranca el contenedor `ubuntu` y accede al fichero creado
7. Elimina el contenedor `ubuntu`


