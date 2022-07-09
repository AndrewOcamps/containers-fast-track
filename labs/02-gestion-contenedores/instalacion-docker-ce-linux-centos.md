## Instalación Docker CE Linux Centos

#### Configuración de Repositorios
```
sudo yum install -y yum-utils

sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```

#### Instalación
```
sudo yum install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

#### Iniciar Servicio
```
sudo systemctl start docker
```