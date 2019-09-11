# Kubernetes

Resumen y comandos más importantes de Kubernetes

Los Pods se definen en un archivo yml
kubectl get all => muestra todo lo que tenemos definido en el cluster
kubectl apply -f name-file.yml => crea un pod en base al archivo leído
kubectl describe pod name-of-pod => describe el pod con el nombre que especifiquemos
kubectl -it exec webapp sh => comando utiliado para conectarnos con un pod de forma interactiva y poder ejecutar comandos directamente a ese pod

