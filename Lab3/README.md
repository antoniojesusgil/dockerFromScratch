## Network & Volumes

1. Accede al directorio `Lab3`
2. En modo `detach` ejecuta un servidor `nginx` en el puerto 80 y mapea el directorio `webA` en la ruta `/usr/share/nginx/html:ro`
  Ayuda: `docker run --rm -v $(pwd)/xxx:/usr/share/nginx/html:ro`
3. Muestra la webA en un navegador
4. Arranca en el puerto 8000 en background un contenedor `nginx` con el contenido del directorio `webB`
5. Muestra la webB en un navegador
6. En una sesión interactiva de una imagen `ubuntu` mapea el directorio de trabajo actual (ruta absoluta) a `/root/` 
7. muestra el directorio actual del contenedor `pwd`
8. Cambia al directorio `root` y muestra un listado detallado del mismo
9. Crea un archivo llamado `file` y guardalo. Sal de la sesión del contendor. ¿Qué ha ocurrido con el fichero `file`?
10. Ejecuta el script `very-useful.py` en un contenedor python3.6-slim
11. Experimenta modificando el código fuente desde tu ordenador de webA y webB
