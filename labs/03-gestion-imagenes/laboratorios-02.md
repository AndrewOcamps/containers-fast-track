## Gestión de Imágenes: 02

Construcción de una imagen de servidor web personalizado

1. Descargue la imagen `centos` con el tag `7`
```
sudo docker pull centos:7
```

2. Verifique la lista de imágenes en su repositorio local. Compruebe que la imagen `centos` se encuentre disponible con el tag `7`
```
sudo docker images
```

La imagen `centos:7` la utilizaremos como base para crear nuestra imagen personalizada

3. En su estación de trabajo cree el fichero `Dockerfile`
```
sudo vi Dockerfile
```

4. Edite el ficher y agregue las siguientes instrucciones
```Dockerfile
FROM centos:7

LABEL description='SERVIDOR WEB CONTAINER FAST TRACK 2022'

RUN yum install -y httpd && \
    yum clean all

EXPOSE 80

CMD ["httpd", "-D", "FOREGROUND"]
```

5. Construir la imagen utilizando `sudo docker build`, definir como nombre `my-server-web` y como tag `v1-dev`
```
sudo docker build -t my-server-web:v1-dev .
```

6. Verifique la lista de imágenes en su repositorio local. Compruebe que la imagen `my-server-web` se encuentre disponible con el tag `v1-dev`
```
sudo docker images
```

7. Inicie el contenedor con el nombre `server-web-01` utilizando la imagen creada. Debe exponer el `puerto 8080` de forma externa y el `puerto 80` de forma interna al contenedor
```
sudo docker run --name server-web-01 -p 8080:80 -d my-server-web:v1-dev
```

8. Verifique la ejecución de su contenedor
```
sudo docker ps
``` 

9. Consulte su servicio web en el `puerto 8080` con el comando `curl`
```
curl http://localhost:8080
```

10. Personalice la imagen creada con un nuevo mensaje
> Editaremos el fichero Dockerfile y agregaremos la siguiente linea
```
RUN echo 'CONTAINERS FAST TRACK 2022 v1' > /var/www/html/index.html
```
> Esta linea debe ser agregada antes de la instrucción `CMD`

> Su fichero debe quedar de la siguiente forma
```Dockerfile
FROM centos:7

LABEL description='SERVIDOR WEB CONTAINER FAST TRACK 2022'

RUN yum install -y httpd && \
    yum clean all

EXPOSE 80

RUN echo 'CONTAINERS FAST TRACK 2022 v1' > /var/www/html/index.html

CMD ["httpd", "-D", "FOREGROUND"]
```

11. Construir la imagen utilizando `sudo docker build`, definir como nombre `my-server-web` y como tag `v1`
```
sudo docker build -t my-server-web:v1 .
```

12. Verifique la lista de imágenes en su repositorio local. Compruebe que la imagen `my-server-web` se encuentre disponible con los siguientes tags `v1-dev` y `v1`
```
sudo docker images
```
> Retornara el siguiente resultado
```yaml
REPOSITORY      TAG       IMAGE ID       CREATED         SIZE
my-server-web   v1        d52c26218d04   7 seconds ago   261MB
my-server-web   v1-dev    110e6eba5923   7 minutes ago   261MB
centos          7         eeb6ee3f44bd   9 months ago    204MB
```

13. Inicie el contenedor con el nombre `server-web-02` utilizando la imagen creada con el tag `v1`. Debe exponer el `puerto 8081` de forma externa y el `puerto 80` de forma interna al contenedor
```
sudo docker run --name server-web-02 -p 8081:80 -d my-server-web:v1
```

14. Verifique la ejecución de su contenedor
```
sudo docker ps
``` 

15. Consulte su servicio web en el `puerto 8081` con el comando `curl`
```
curl http://localhost:8081
```