## Instalación Minikube 
Para la instalación de Minikube es necesario simplemente 1 máquina virtual

Utilice el fichero [Vagrantfile](minikube/Vagrantfile) para la instalación del componente Minikube

1. Defina su directorio de trabajo, para este ejemplo, usamos el directorio 'docker-swarm`
```
mkdir minikube
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

linux-minikube            running (virtualbox)
```

4. Ingrese por ssh al nodo `linux-minikube`
```
vagrant ssh linux-minikube
```

5. Cambie su sesión a root
```
sudo su - root
```

6. Instale la ultima versión estable de Minikube
```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-latest.x86_64.rpm
rpm -Uvh minikube-latest.x86_64.rpm
```

7. Inicie su servicio de `minikube`, utilizando como proveedor de recursos `docker`
```
minikube start --driver=docker --force
```

```yaml
😄  minikube v1.26.0 on Rocky 8.4 (vbox/amd64)
❗  minikube skips various validations when --force is supplied; this may lead to unexpected behavior
✨  Using the docker driver based on user configuration
🛑  The "docker" driver should not be used with root privileges. If you wish to continue as root, use --force.
💡  If you are running minikube within a VM, consider using --driver=none:
📘    https://minikube.sigs.k8s.io/docs/reference/drivers/none/

🧯  The requested memory allocation of 2200MiB does not leave room for system overhead (total system   memory: 2985MiB). You may face stability issues.
💡  Suggestion: Start minikube with less memory allocated: 'minikube start --memory=2200mb'

📌  Using Docker driver with root privileges
👍  Starting control plane node minikube in cluster minikube
🚜  Pulling base image ...
💾  Downloading Kubernetes v1.24.1 preload ...
```

8. Valide la correcta instalación de su servicio `kubernetes`
```
minikube status
```
```
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured
```
9. Configure el cliente `kubectl` para interactuar con la API de `kubernetes`
```
alias kubectl="minikube kubectl --"
```

10. Verifique las opciones del comando `kubectl`
```
kubectl --help
```