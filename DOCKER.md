### COMANDOS BÁSICOS
**docker run hello-world** Compreuba que Docker esté bien instalado y hace el hola mundo  
**docker ps** Nos dice todos los contenedores activos que están corriendo  
**docker ps -a** Muestra todos los contenedores en el sistema (activos o inactivos)  
**docker rm idDelContenedor** Elimina el contenedor especificado, ya sea por su id o por su nombre  

### EJEMPLO DE CONTENEDOR SENCILLO
En una terminal se comienza por crear un documento de texto con el siguiente comando:  
**nano Dockerfile**  
Ahora se ingresa el siguiente contenido:  
**FROM ubuntu:latest** # Imagen base para crear nuestro contenedor  
**CMD echo "Mi primer contenedor"** # CMD expresa 'comando'  
Posteriormente en una terminal ejecutar el siguiente comando para construir el 'Dockerfile':  
**docker build . -t nombre-de-la-imagen** Donde el punto expresa directorio actual  
Y por último se ejecuta el contenedor como tal:  
**docker run nombre-de-la-imagen**

### RESUMEN PARA CREAR UN CONTENEDOR PERSONALIZADO
1) Crea un Dockerfile con las características deseadas
2) Con el comando build se crea una imagen
3) Con run se crea un contenedor, es decir una instancia del contenedor

### PASOS PARA INSTALAR SOFTWARE EN UN CONTENEDOR
**FROM ubuntu:latest**  
**RUN apt-get update && apt-get install -y --no-install-recommends wget && apt-get clean**  
Nota: en este caso se usa Ubuntu como base para instalar wget  

### ACCEDER A LA LINEA DE COMANDOS DE UN CONTENEDOR
**-it** ejecuta el contenedor de forma interactiva  
**/bin/bash** especifica la ruta donde tomar los binarios  
**docker run -it ubuntu /bin/bash** ejemplo de ejecucion de un contenedor de forma interactiva

### MONTAR UN VOLUMEN EN UN CONTENEDOR
Ejecutamos un contenedor de forma interactiva con cualquiera de las siguientes opciones (de Windows a Linux):  
**docker run -it -v C:\Users\Oliver\Documents\personales\git\01\script.sh:/home/script.sh ubuntu /bin/bash**  
**docker run -it -v //c/Users/myScript.sh:/home/myScript.sh ubuntu /bin/bash**  
Y para realizar la misma operación de Linux a Linux:
**docker run -it -v "$(pwd)/script.sh:/home/script.sh" ubuntu /bin/bash**  
**-v** significa que montaremos un volumen, de lado izquierdo de los puntos se define el origen del elemento a montar, de lado derecho se define el destino del elemento a montar  

### ACCEDER A LOGS
**docker run -d -P --name my-docker httpd** Se ejecuta un docker, -d es Daemon y -P habilia los puertos  
**docker logs my-docker** Accesa al archivo de logs  
**docker logs -f my-docker** Obtiene logs en tiempo real  
**docker logs --tail 66 my-docker** Regresa las ultimas 66 lineas del log  
**docker logs -f --tail 8 my-docker** Regresa las ultimas 8 lineas del log y continua poleando  
Nota: Para saber mas de logs checar splunk

### HEALTHCKECKS
Se crea un nuevo contenedor con curl instalado y con HEALTHCHECK se definen los parametros:  
**FROM tomcat:latest**  
**RUN apt-get update && apt-get install -y --no-install-recommends curl && apt-get clean**  
**HEALTHCHECK --interval=20s --retries=5 --timeout=30s --start-period=5s CMD curl -I -f "http://localhost:8080" || exit 1**  
Posteriormente se construye y se corre el contenedor de la siguiente manera:  
**docker build . -t tomcat-hc**  
**docker run -d -P tomcat-hc**  
Ahora en STATUS se mostrará la salud del contenedor:  
**docker ps**  

## COMANDOS MÁS AVANZADOS EN DOCKER  
**docker ps -q** imprime todos los ids de los contenedores que están corriendo  
**docker ps -a - q** imprime todos los ids de los contenedores, tanto de los que están corriendo, como de los que no  
**docker stop idContenedror** detiene el container que se ha especificado, ya sea por nombre o por id  
**docker stop $(docker ps -q)** detiene todos los contenedores, todos  
**docker rm $(docker -a -q)** remueve todos los contenedores, incluyendo los que ya están detenidos  
**docker ps --filter status=running** Muestra los dockers filtrandolos por estatus  
**docker ps --filter status=running -q** El comando anterior se puede combinar con otras opciones, hay muchas más opciones de filtros, buscarlas en internet**docker rm $()  
**docker inspect idDelDocker** muestra toda la información del docker  en formato json  



 


### CONECTANDO CONTENEDORES
Tema en desarrollo...  