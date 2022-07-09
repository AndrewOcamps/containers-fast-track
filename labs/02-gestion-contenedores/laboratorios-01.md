## Gestión de Contenedores: 01

1. Inicia la aplicación hello world

```
sudo docker run hello-world
```

> Retornara el siguiente mensaje:
```yaml
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

2. Iniciar un servicio web con NGINX
```
sudo docker run nginx
```

Para cancelar la ejecución, CTRL+Z

3. Inicie otro servicio web con la imagen `NGINX`, pero en segundo plano y especifique un nombre al contenedor
```
sudo docker run --name webserver -d nginx
```

> Retornara un identificador unico
```yaml
a67ffde4cfff4cd70ad93350be2c79661e89e2294fe341c62a16e1448fdea171
```

4. Verifique la ejecución de su contenedor
```
sudo docker ps
``` 

> Retornara la lista de contenedores en ejecución
```
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS     NAMES
70720d94db39   nginx     "/docker-entrypoint.…"   4 seconds ago   Up 4 seconds   80/tcp    webserver
```

5. Renombre su contenedor a `webapp-01`
```
sudo docker rename webserver webapp-01
```

6. Verifique la ejecución de su contenedor. Compruebe si el nombre ha cambiado
```
sudo docker ps
``` 

7. Verifique los logs de su contenedor
```
sudo docker logs webapp-01
```

8. Inicie un nuevo contenedor con el nombre `webapp-02` utilizando la imagen `NGINX`. Debe exponer el `puerto 80` para acceder al contenido de su servicio web
```
sudo docker run --name webapp-02 -p 80:80 -d nginx
```

9. Verifique la ejecución de su contenedor. Compruebe el nuevo contenedor creado
```
sudo docker ps
``` 

10. Consulte su servicio web en el `puerto 80` con el comando `curl`
```
curl http://localhost:80
```
> Retornara el mensaje de bienvenida de NGINX

```yaml
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

11. Detener el contenedor
```
sudo docker stop webapp-01

sudo docker stop webapp-02
```

12. Verifique la ejecución de su contenedor. Ya no debería estar los contenedores en ejecución
```
sudo docker ps
``` 

13. Verifique los contenedores que no se encuentran en ejecución
```
sudo docker ps -a
```

14. Elimine el contenedor `webapp-01`
```
sudo docker rm webapp-01
```

15. Inicie el contenedor `webapp-02`
```
sudo docker start webapp-02
```

16. Verifique la ejecución de su contenedor. Puede utilizar `sudo docker ps` para ver los contenedores iniciados y `sudo docker ps -a` para ver la lista de contenedores completa. Ya no debe de existir el contenedor `webapp-01`
```
sudo docker ps

sudo docker ps -a
``` 
