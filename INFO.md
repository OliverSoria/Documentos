docker run hello-world ** Compreuba que Docker esté bien instalado y hace el hola mundo **
docker ps ** Nos dice todos los contenedores activos que están corriendo **
docker ps -a ** Muestra todos los contenedores en el sistema (activos o inactivos) **
docker rm idDelContenedor ** Elimina el contenedor especificado, ya sea por su id o por su nombre **
nano Dockerfile ** Crea un contenedor **

#### EJEMPLO DE CONTENEDOR SENCILLO
FROM ubuntu:latest # Imagen base para crear nuestro contenedor
CMD echo "Mi primer contenedor" # CMD expresa 'comando'
#### Se usa para construir el 'Dockerfile', el punto expresa directorio actual
docker build . -t nombre-de-la-imagen

#### RESUMEN PARA CREAR UN CONTENEDOR PERSONALIZADO
1) Crea un Dockerfile con las características deseadas
2) Con el comando build se crea una imagen
3) Con run se crea un contenedor, es decir una instancia del contenedor

#### PASOS PARA INSTALAR SOFTWARE EN UN CONTENEDOR
#### En este caso se usa Ubuntu como base para instalar wget
FROM ubuntu:latest
RUN apt-get update && apt-get install -y --no-install-recommends wget && apt-get clean

#### ACCEDER A LA LINEA DE COMANDOS DE UN CONTENEDOR
**-it** ejecuta el contenedor de forma interactiva  
**/bin/bash** especifica la ruta donde tomar los binarios  
**docker run -it ubuntu /bin/bash** ejemplo de ejecucion de un contenedor de forma interactiva

# ACCEDER A LOGS
docker run -d -P --name my-docker httpd # Se ejecuta un docker -d es Daemon y -P habilia los puertos
docker logs my-docker # Accesa al archivo de logs
docker logs -f my-docker # Obtiene logs en tiempo real
docker logs --tail 66 my-docker # Regresa las ultimas 66 lineas del log
docker logs -f --tail 8 my-docker # Regresa las ultimas 8 lineas del log y continua poleando
# Para saber mas de logs checar splunk

# HEALTHCKECKS
# Se crea un nuevo contenedor con curl instalado
# Con HEALTHCHECK se definen los parametros
FROM tomcat:latest
RUN apt-get update && apt-get install -y --no-install-recommends curl && apt-get clean
HEALTHCHECK --interval=20s --retries=5 --timeout=30s --start-period=5s CMD curl -I -f "http://localhost:8080" || exit 1

docker build . -t tomcat-hc # Se construye la imagen
docker run -d -P tomcat-hc # Se ejecua el contenedor
docker ps # En STATUS ahora mostrara la salud del contenedor

# CONECTANDO CONTENEDORES