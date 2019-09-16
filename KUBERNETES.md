# Kubernetes

### Resumen y comandos más importantes de Kubernetes

Los **pods** se definen en un archivo yml<br/>
**minikube ip** nos devuelve la ip del minukube para poder conectarnos a sus servicios<br/>
**kubectl get all** muestra todo lo que tenemos definido en el cluster<br/>
**kubectl apply -f name-file.yml** crea un pod en base al archivo leído<br/>
**kubectl describe pod name-of-pod** describe el pod con el nombre que especifiquemos<br/>
**kubectl -it exec webapp sh** comando utiliado para conectarnos con un pod de forma interactiva y poder ejecutar comandos directamente a ese pod<br/>
Los pods **no** se pueden ver desde afuera del cluster, o sea que no es posible acceder a un pod por su ip/puerto<br/>

### Creación de un pod

Un pod lo empezamos por definir en un archivo yml, ejemplo:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: webapp
  labels:
    label: webapp
spec:
  containers:
    - name: webapp
      image: richardchesterwood/k8s-fleetman-webapp-angular:release0-5
```
Posteriormente debemos desplegar ese pod, para lo cual usaremos el comando **kubectl apply -f mi-pod.yml**

### Creación de un servicio

Un pod no puede ser accedido desde afuera, pero un servicio sí, por ese motivo crearemos un servicio que nos permita acceder al pod creado anteriormente, esto se logra por medio de un archivo yml, ejemplo:

```yaml
apiVersion: v1
kind: Service
metadata:
  # Unique key of the Service instance
  name: fleetman-webapp

spec:
  selector:
    label: webapp

  ports:
    - port: 80
      name: http
      nodePort: 30080

  type: NodePort
```

Posteriormente desplegamos el servicio con el mismo comando que se despliega un pod **kubectl apply -f mi-servicio.yml**<br/>

Nota: es importante señalar que la _label_ del servicio debe coincider con la _label_ del pod para que tengan comunicación.

Ahora, para acceder a la aplicación y validar que todo esté bien, necesitamos la ip del minikube dado que todo lo estamos corriendo en un minikube, entonces ejecutamos: **minikube ip**, nos devielve la ip eg. 192.168.99.100 a la cual solo agregamos el puerto que definimos en el servicio y listo: http://192.168.99.100:30080/<br/>




