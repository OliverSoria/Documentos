# Kubernetes

### Resumen y comandos más importantes de Kubernetes

Los **pods** se definen en un archivo yml<br/>
**kubectl get all** muestra todo lo que tenemos definido en el cluster<br/>
**kubectl apply -f name-file.yml** crea un pod en base al archivo leído<br/>
**kubectl describe pod name-of-pod** describe el pod con el nombre que especifiquemos<br/>
**kubectl -it exec webapp sh** comando utiliado para conectarnos con un pod de forma interactiva y poder ejecutar comandos directamente a ese pod<br/>
Los pods **no** se pueden ver desde afuera del cluster, o sea que no es posible acceder a un pod por su ip/puerto<br/>
