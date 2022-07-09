## Storage en Contenedores

1. Liste los volumenes disponibles por defecto de Docker
```
sudo docker volume ls
```

> Retornara el volumen con driver local. Este volumen tiene por nombre un identificador unico. 

2. Verifique el punto de almacenamiento del volumen 
```
sudo docker inspect volume <identificador-unico>
```

> Retornara un objeto json con los datos solicitados
```json
[
    {
        "CreatedAt": "2022-07-07T12:03:53Z",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/de3a6118f1bf0f60161fc25feae2dd6e5e7bb15a4f5fd87417dfc65b900c79f4/_data",
        "Name": "de3a6118f1bf0f60161fc25feae2dd6e5e7bb15a4f5fd87417dfc65b900c79f4",
        "Options": null,
        "Scope": "local"
    }
]
```
> El almacenamiento por defecto de los volumenes docker es en el `/var/lib/docker/volumes`

3. Cree un nuevo volumen con el nombre de `datos-01`
```
sudo docker volume create datos-01
```

4. Liste los volumenes disponibles. Debe aparecer el volumen creado
```
sudo docker volume ls
```

5. Verifique el punto de almacenamiento del volumen `datos-01`
```
sudo docker inspect volume datos-01
```

> Retornara un objeto json con los datos solicitados
```json
[
    {
        "CreatedAt": "2022-07-07T14:16:33Z",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/datos-01/_data",
        "Name": "datos-01",
        "Options": {},
        "Scope": "local"
    }
]
```

6. Liste el contenido del directorio de almacenamientos `datos-01`
```
sudo ls -ltr /var/lib/docker/volumes/datos-01/_data
```

> Debe retornar un directorio vacio

7. Inicie un nuevo contenedor con la imagen `jenkins/jenkins:jdk11`. El nombre del contenedor debe ser `jenkins-server-data`. Monte el volumen creado en el contenedor en el path `/var/jenkins_home`
```
sudo docker run --name jenkins-server-data -v datos-01:/var/jenkins_home -d jenkins/jenkins:jdk11
```
6. Liste el contenido del directorio de almacenamientos `datos-01`
```
sudo ls -ltr /var/lib/docker/volumes/datos-01/_data
```
> Retornara los datos que se encuentran en el contenedor
```yaml
total 12
-rw-r--r--.  1 vagrant vagrant  50 Jul  7 14:29 copy_reference_file.log
drwxr-xr-x. 11 vagrant vagrant 196 Jul  7 14:29 war
-rw-r--r--.  1 vagrant vagrant  29 Jul  7 14:29 failed-boot-attempts.txt
-rw-r--r--.  1 vagrant vagrant  64 Jul  7 14:29 secret.key
-rw-r--r--.  1 vagrant vagrant   0 Jul  7 14:29 secret.key.not-so-secret
drwxr-xr-x.  2 vagrant vagrant   6 Jul  7 14:29 plugins
drwxr-xr-x.  2 vagrant vagrant   6 Jul  7 14:29 jobs
```