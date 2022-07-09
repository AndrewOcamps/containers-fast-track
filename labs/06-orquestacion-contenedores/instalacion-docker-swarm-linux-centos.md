## Instalación Docker Swarm

Para la instalación de Docker SWARM es necesario 3 máquinas virtuales. Utilizaremos dos nodos esclavos y 1 nodo maestro

Utilice el fichero [Vagrantfile](docker-swarm/Vagrantfile) para la instalación del cluster Docker Swarm

1. Defina su directorio de trabajo, para este ejemplo, usamos el directorio 'docker-swarm`
```
mkdir docker-swarm
```

2. Copie el fichero Vagrantfile al directorio de trabajo. Luego, inicie la instalación
```
vagrant up
```

3. Verifique que todos los nodos se encuentran iniciados
```
vagrant status
```

```yaml
Current machine states:

master                    running (virtualbox)
slave01                   running (virtualbox)
slave02                   running (virtualbox)
```

4. Ingrese por ssh al nodo `master`
```
vagrant ssh master
```

5. Dentro del servidor `master`, vamos a inicializar el servicio de docker swarm
> Especificamos la ip de nuestro servidor master

```
sudo docker swarm init --advertise-addr 192.168.33.41
```
> Al finalizar el proceso, nos va a retornar un comando, que utilizaremos para configurar los nodos esclavos. Copie ese comando y guárdelo en un archivo de texto
```yaml
To add a worker to this swarm, run the following command:
  docker swarm join --token SWMTKN-1-3nwwc1u38487mt5yio65nqqswc1pffl6zhg9wlyeaq0jqpzw1s-d7d9qscp5fuyzlqgs1rfg9seo 192.168.33.41:2377
```

> El siguiente paso es activar los nodos esclavos, vamos a iniciar sesion ssh en los siguientes nodos
6. Ingrese por ssh al nodo `slave01`
```
vagrant ssh slave01
```

7. Ingrese el comando para configurar el nodo `slave01` con el nodo `master`
> Utilice `sudo docker` para lanzar el comando
```
sudo docker swarm join --token SWMTKN-1-3nwwc1u38487mt5yio65nqqswc1pffl6zhg9wlyeaq0jqpzw1s-d7d9qscp5fuyzlqgs1rfg9seo 192.168.33.41:2377
``` 
> Retornara el siguiente mensaje
```yaml
This node joined a swarm as a worker.
```
> Vamos a repetir el proceso con el siguiente nodo

8. Ingrese por ssh al nodo `slave02`
```
vagrant ssh slave02
```

9. Ingrese el comando para configurar el nodo `slave02` con el nodo `master`
> Utilice `sudo docker` para lanzar el comando
```
sudo docker swarm join --token SWMTKN-1-3nwwc1u38487mt5yio65nqqswc1pffl6zhg9wlyeaq0jqpzw1s-d7d9qscp5fuyzlqgs1rfg9seo 192.168.33.41:2377
``` 
> Retornara el siguiente mensaje
```yaml
This node joined a swarm as a worker.
```

10. Vuelva a ingresar al nodo `master`. Y valide su configuración
```
sudo docker node ls

ID                            HOSTNAME          STATUS    AVAILABILITY   MANAGER STATUS   ENGINE VERSION
rjdr4u22zanfmt5rh9lcdug08 *   linux-master-01   Ready     Active         Leader           20.10.17      
60b0to6sej93khk9lnfe23nlz     linux-slave-01    Ready     Active                          20.10.17      
puzxlpkd6snaxr9qi799vwiq6     linux-slave-02    Ready     Active                          20.10.17
```
