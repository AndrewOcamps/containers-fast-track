## Redes en Contenedores: 01

1. Liste las redes por defecto de Docker
```
sudo docker network ls
```

2. Verifique la subnet que utiliza la red `bridge`
```
sudo docker inspect network bridge
```
> Retornara el siguiente objeto JSON. Identifique la entada `subnet`
```json
[
    {
        "Name": "bridge",
        "Id": "aace529a8aea8752d98a17d0032451251a56ba057c559c93ac214aba533c58a5",
        "Created": "2022-07-06T18:39:13.875227085Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": null,
            "Config": [
                {
                    "Subnet": "172.17.0.0/16"
                }
            ]
        },
```

3. Cree una nueva red con valores por defecto con el nombre de `my-net`
```
sudo docker network create my-net
```

4. Liste las redes disponibles. Debe aparecer su red creada
```
sudo docker network ls
```

5. Verifique la subnet que utiliza la red creada `my-net`
```
sudo docker inspect network my-net
```

6. Cree una nueva red con el nombre de `my-private-net`. Indique la subnet `10.10.0.0/16` y el gateway `10.10.0.1`
```
sudo docker network create my-private-net --subnet 10.10.0.0/16 --gateway 10.10.0.1
```

7. Liste las redes disponibles. Debe aparecer su red creada
```
sudo docker network ls
```

8. Verifique la subnet que utiliza la red creada `my-private-net`
```
sudo docker inspect network my-private-net
```

10. Inicie un nuevo contenedor con la imagen `nginx`. El nombre del contenedor debe ser `private-web`. Debe utilizar la red `my-private-net`
```
sudo docker run --name private-web --network my-private-net -d nginx
```

11. Vuelva a inspeccionar la red `my-private-net` con el comando `docker inspect network`. Verifique el apartado de `Containers` e identifique el contenedor que se encuentra asociado con la red creada
```
sudo docker inspect network my-private-net
```
> Retornara el siguiente resultado. Se observa el nombre de `private-web`
```json
        "Containers": {
            "19976d2d424cd967e976a16b2829a5c8cb50d765c969754455c80a9db1354b59": {
                "Name": "private-web",
                "EndpointID": "14a6d7152ad553959682bb194b06e1cd9cf4982e22aa47fb1a9bcbe817dca890",
                "MacAddress": "02:42:0a:0a:00:02",
                "IPv4Address": "10.10.0.2/16",
                "IPv6Address": ""
            }
        }
```

