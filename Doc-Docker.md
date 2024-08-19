<div align="center">
  <img src="https://raw.githubusercontent.com/jorgenavarroenamoradotokio/docs/feature/docker/logos/Docker-Logo.svg">
</div>

# Introducción

Docker es una plataforma de software que permite crear, implementar y ejecutar aplicaciones en contenedores. 
Los contenedores son entornos aislados y ligeros que contienen todo lo necesario para que una aplicación funcione, incluyendo el código, las dependencias y las configuraciones. Esto facilita que las aplicaciones se ejecuten de manera consistente en cualquier entorno, ya sea en una máquina local, en un servidor o en la nube.

# Conceptos claves

- Contenedor: Un contenedor es una unidad estandarizada de software que agrupa el código de una aplicación y sus dependencias para que se ejecute de manera confiable en cualquier entorno.
- Imagen: Una imagen de Docker es una plantilla de solo lectura que contiene las instrucciones para crear un contenedor. Es como una instantánea de un sistema de archivos que incluye la aplicación y todo lo necesario para ejecutarla.
- Dockerfile: Es un archivo de texto con un conjunto de instrucciones para construir una imagen de Docker. Define cómo debe ser configurado el contenedor.
- Docker Hub: Es un servicio de registro de imágenes públicas de Docker, donde los desarrolladores pueden compartir y descargar imágenes.

Las ventajas de usar docker son:
- Portabilidad: Los contenedores pueden ejecutarse en cualquier sistema operativo que tenga Docker instalado, lo que facilita mover aplicaciones entre entornos de desarrollo, prueba y producción.
- Aislamiento: Cada contenedor funciona de manera aislada, lo que significa que no interfiere con otras aplicaciones en el mismo sistema.
- Escalabilidad: Docker facilita la creación de aplicaciones escalables al permitir la implementación de múltiples contenedores en paralelo.
- Eficiencia: Los contenedores comparten el kernel del sistema operativo, lo que los hace más ligeros y eficientes en el uso de recursos que las máquinas virtuales.

# Arquitectura

Docker está compuesta por varios componentes clave que trabajan juntos para permitir la creación, administración y ejecución de contenedores, siguiendo la siguiente arquitectura:
- Usuarios interactuando con Docker CLI o API.
- Docker CLI/API comunicándose con Docker Daemon.
- Docker Daemon gestionando contenedores, imágenes, volúmenes y redes.
- Docker Daemon obteniendo imágenes de Docker Hub o un registro privado.
- Redes conectando contenedores entre sí y con el mundo exterior.
- Volúmenes almacenando datos persistentes.

## Docker Engine

El Docker Engine es el núcleo de Docker. Es el componente que permite la creación y ejecución de contenedores. Está compuesto por tres partes principales:

- Docker Daemon (dockerd): Es el proceso que se ejecuta en segundo plano en el sistema operativo y que gestiona los contenedores de Docker. Se encarga de construir, ejecutar y gestionar contenedores y es el encargado de interactuar con otros componentes de Docker.
- Docker API: Es la interfaz de programación de aplicaciones que permite a los usuarios y a las aplicaciones comunicarse con el Docker Daemon. A través de la API, se pueden enviar comandos a Docker, como la creación de contenedores o la consulta de su estado.
- Interfaz de Línea de Comandos (CLI): La CLI de Docker es la herramienta que permite a los usuarios interactuar con Docker desde la línea de comandos. Utiliza la API de Docker para enviar comandos al Docker Daemon, como docker run, docker build, etc.

## Imágenes de Docker

Las imágenes son plantillas inmutables que contienen el código de la aplicación y todas las dependencias necesarias para ejecutarla. Las imágenes se construyen a partir de un archivo llamado Dockerfile, que contiene las instrucciones para crear la imagen.

### Capas de Imagen 

Las imágenes de Docker están compuestas por capas. Cada instrucción en el Dockerfile crea una nueva capa en la imagen. Esto permite la reutilización de capas entre imágenes, lo que hace que la creación y distribución de imágenes sea más eficiente.
  - FROM: sistema/herramienta principal que permite la ejecucion de la imagen (sistema operativo, libreia de lenguaje, etc)
  - WORKDIR: estable el directorio de trabajo
  - COPY: copia archivos desde el sistema de archivos del host a la imagen
  - RUN: ejecuta comandos dentro de la imagen para instalar las dependencias 
  - CMD: define el comando que se ejecutara cuando inicie el contenedor basado en en la imagen

### Dockerfile

- Dockerfile: Un archivo de texto con una serie de instrucciones que especifican cómo construir una imagen. Define la base de la imagen (por ejemplo, un sistema operativo), las dependencias, la configuración, y los comandos que deben ejecutarse dentro del contenedor.

```dockerfile
# Selecciona una imagen base
FROM centos:7
# Ejecutar la imagen
RUN yum -y install httpd
# Define el comando por defecto para ejecutar la aplicación
CMD ["apachectl", "-DFOREGROUND"]
```

#### Estructura

Un Dockerfile está compuesto por una serie de instrucciones que Docker procesa secuencialmente para crear una imagen. Algunas de las instrucciones más comunes incluyen:

- FROM: Define la imagen base a partir de la cual se construirá la nueva imagen. Esta es generalmente la primera línea del Dockerfile.
```Ejemplo: FROM ubuntu:20.04```
- RUN: Ejecuta un comando en la imagen durante la construcción de la misma. Es utilizado para instalar paquetes, configurar el entorno, etc.
```Ejemplo: RUN apt-get update && apt-get install -y nginx```
- COPY: Copia archivos o directorios desde el sistema de archivos del host al sistema de archivos del contenedor.
```Ejemplo: COPY . /app```
- ADD: Similar a COPY, pero con capacidades adicionales, como descomprimir archivos tar automáticamente.
```Ejemplo: ADD app.tar.gz /app```
- ENV: Establece variables de entorno dentro del contenedor.
```Ejemplo: ENV ENVIRONMENT=production```
- WORKDIR: Establece el directorio de trabajo dentro del contenedor. Cualquier comando subsiguiente se ejecutará desde este directorio.
```Ejemplo: WORKDIR /app```
- EXPOSE: Informa a Docker que el contenedor escucha en un puerto específico en tiempo de ejecución, aunque no abre realmente el puerto.
```Ejemplo: EXPOSE 80```
- LABEL: Añade metadatos a la imagen en forma de pares clave-valor.
```Ejemplo: LABEL maintainer="admin@example.com"```
- USER: Especifica el usuario bajo el cual se ejecutarán las instrucciones RUN, CMD, y ENTRYPOINT.
```Ejemplo: USER nginx```
- VOLUME: Crea un punto de montaje para compartir datos entre el contenedor y el host, o entre contenedores.
```Ejemplo: VOLUME /data```
- CMD: Especifica el comando predeterminado que se ejecutará cuando se inicie un contenedor basado en la imagen. Solo puede haber una instrucción CMD en un Dockerfile.
```Ejemplo: CMD ["nginx", "-g", "daemon off;"]```
- ARG: Define variables que se pueden pasar como argumentos de compilación al construir la imagen.
```Ejemplo: ARG APP_VERSION=1.0```
- ENTRYPOINT: Define el comando que siempre se ejecutará cuando el contenedor inicie. A diferencia de CMD, ENTRYPOINT no se puede sobrescribir fácilmente al iniciar el contenedor.
```Ejemplo: ENTRYPOINT ["python", "app.py"]```

### .Dockerignore

Es un archivo de texto que se utiliza en Docker para especificar qué archivos y directorios deben ser excluidos cuando se construye una imagen a partir de un Dockerfile. Su funcionamiento es similar al de un archivo .gitignore en Git, donde se define una lista de patrones que indican qué contenidos deben ser ignorados durante la construcción de la imagen.

Las principales ventajas son:
- Mejora del rendimiento: Al excluir archivos innecesarios, reduces el tiempo de construcción de la imagen y el tamaño del contexto de construcción.
- Seguridad: Evita que archivos sensibles, como claves privadas o archivos de configuración, sean incluidos accidentalmente en la imagen de Docker.
- Optimización del almacenamiento: Al evitar que archivos innecesarios sean incluidos en la imagen, reduces el tamaño final de la misma.

### Tags

Son las etiquetas que nos indican la version de la imagen que nos vamos a descargar en nuestro docker
- latest: nos indica que nos vamos a descargar e instalar la ultima version disponible de la imagen que deseamos.

### Comandos

- Construir una imagen a partir de un docker file ```docker image build```
- Descargar una imagen desde un repositorio ```docker pull```
- Listar imagenes instaladas en tu maquina local ```docker images```
- Eliminar una imagen ```docker rmi``` o ```docker rm```
- Asignar una etiqueta a una imagen ```docker tag```
- Informacion detallada de una imagen ```docker image inspect```
- Historial de capas de una imagen ```docker image history```
- cargar una imagen desde un archivo guardado anteriormente ```docker image load```
- Importar una imagen desde un archivo des sistemas de archivos ```docker image import```
- Exportar una imagen ```docker image export```
- Eliminar imagenes no utilizadas ```docker image prune```
- Crear una etiqueta para una imagen ``` docker image tag```

## Contenedores de Docker

Un contenedor es una instancia en ejecución de una imagen de Docker. Representa una aplicación en ejecución con todo lo necesario para funcionar de manera aislada. Los contenedores son ligeros y comparten el núcleo del sistema operativo con otros contenedores, pero cada uno tiene su propio sistema de archivos, red y espacio de proceso.

- Aislamiento: Los contenedores se ejecutan de manera aislada, lo que significa que no pueden interferir con otros contenedores en el sistema.
- Ligereza: A diferencia de las máquinas virtuales, los contenedores no incluyen un sistema operativo completo. En su lugar, comparten el kernel del sistema operativo del host, lo que los hace más ligeros y rápidos de iniciar. Esto permite ejecutar muchos contenedores en un solo servidor sin un gran sobrecarga de recursos.
- Portabilidad: Como los contenedores incluyen todo lo necesario para ejecutar una aplicación, pueden trasladarse entre diferentes entornos (como desarrollo, pruebas y producción) sin problemas. Si una aplicación funciona en un contenedor en tu máquina local, debería funcionar de la misma manera en la nube o en cualquier otro sistema con Docker instalado.
- Ephemeralidad (carácter efímero): Los contenedores son generalmente efímeros, lo que significa que están diseñados para ser temporales. Una vez que un contenedor se detiene o se elimina, todo lo que está dentro del contenedor se pierde, a menos que se haya configurado un volumen para persistir los datos fuera del contenedor. Esto refuerza el concepto de que los contenedores deben ser reemplazables y que no deben contener datos importantes o configuraciones únicas.
- Rápida creación y eliminación: Los contenedores se pueden crear, detener y eliminar rápidamente, lo que facilita la escalabilidad y la gestión de aplicaciones. Esto permite implementar rápidamente nuevas instancias de aplicaciones en diferentes entornos.
- Persistencia: Aunque los contenedores son efímeros, los datos se pueden persistir utilizando volúmenes, que permiten almacenar datos fuera del contenedor y compartirlos entre contenedores.

### Estructura

- Sistema de archivos(Imagen): Cada contenedor tiene su propio sistema de archivos basado en la imagen desde la que se creó. Aunque los contenedores comparten el kernel del sistema operativo del host, tienen su propio espacio de archivos, lo que les permite estar aislados.
- Volúmenes: Aunque los datos dentro de un contenedor se pierden cuando el contenedor se elimina, Docker permite montar volúmenes, que son directorios compartidos entre el host y el contenedor o entre varios contenedores. Esto permite la persistencia de datos y el intercambio de información entre contenedores.
- Red: Docker proporciona varias opciones para configurar la red de un contenedor, permitiendo que los contenedores se comuniquen entre sí o con el mundo exterior. Los contenedores pueden tener su propia dirección IP y pueden estar conectados a redes definidas por el usuario.
- Procesos: Dentro de un contenedor, los procesos funcionan de manera independiente de otros procesos en el host o en otros contenedores. Aunque un contenedor puede ejecutar varios procesos, en muchos casos se recomienda que cada contenedor ejecute un solo proceso (por ejemplo, un servicio o una aplicación específica).

### Beneficios

- Consistencia: Al empaquetar la aplicación y todas sus dependencias en un contenedor, se garantiza que funcionará de la misma manera en cualquier entorno, reduciendo los problemas de configuración.
- Escalabilidad: Docker facilita la escalabilidad de aplicaciones, permitiendo crear y administrar múltiples instancias de contenedores rápidamente.
- Eficiencia: Los contenedores son ligeros y consumen menos recursos que las máquinas virtuales, permitiendo un uso más eficiente del hardware.

### Comparación con máquinas virtuales

- Máquinas virtuales: Cada VM incluye un sistema operativo completo, lo que consume más recursos y lleva más tiempo iniciar. Además, cada VM necesita su propio hipervisor para gestionar los recursos.
- Contenedores: Los contenedores comparten el mismo núcleo del sistema operativo, lo que los hace más ligeros y rápidos de iniciar. No necesitan un sistema operativo completo en cada instancia, lo que ahorra recursos.

### Comandos

- Crea y ejecutar un contendor ```docker run ```
- crear un contenedor pero sin iniciar ```docker create nbContenedor```
- Iniciar un contendor detenido ```docker start contenedor_id``` o ```docker container start contenedor_id```
- Detener un contendor en ejecucion ```docker stop contenedor_id``` o ```docker container stop contenedor_id```
- Reiniciar un contendor ```docker restart contenedor_id``` o ```docker container restart contenedor_id```
- Forzar la detencion de un contenedor inmediatamente ```docker kill contenedor_id``` o ```docker container kill contenedor_id```
- Pausar todos los procesos de un contenedor ```docker pause contenedor_id```
- Reanidar todos los procesos pausados de un contenedor ```docker unpause contenedor_id```
- Eliminar un contenedor ```docker rm contenedor_id```
- Listar los contenedores en ejecución ```docker ps``` o ```docker ls```
- Listar todos los contenedores (en ejecucion o detenidos) ```docker ps -a```
- Ejecutar comando dentro de un contenedor ```docker exec -it contenedor_id comando```
- Registros de log de un contenedor ```docker logs contenedor_id```
- Informacion detallada de un contenedor ```docker inspect contenedor_id```
- Procesos que se estan ejecutando dentro de un contenedor ```docker top contenedor_id```
- Estadisticas asociadas al contenedor ```docker stats contenedor_id```
- Ajuntar la consola del terminal al stdin, stdout y stderr ```docker attach contenedor_id```
- Mostrar los puertos mapeados a un contenedor ```docker port contenedor_id```
- Copar archivos o directorios entre contenedor y host ```docker cp contenedor_id:/path_in_container /path_in_host```
- Renombrar un contenedor ```docker rename old_name new name```
- Bloque hasta que el contenedor se detiene con codigo de salida ```docker wait contenedor_id```
- Inspecciona los cambios en el sistema de archivos de un contenedor en comparacion con la imagen base ```docker diff contenedor_id```
- Exportar el sistema de archivos de un contenedor a un archivo tar ```docker export contenedor_id > container.tar```
- Eliminar todos los contenedores detenidos ```docker container prune```
- Actualizar la configuración de recursos de un contenedor ```docker update --cpus 2 contenedor_id```


## Volúmenes de Docker (Docker Volumes)

Los volúmenes se utilizan para persistir datos generados y utilizados por contenedores. Se almacenan fuera del contenedor, en el sistema de archivos del host, lo que permite que los datos persistan incluso si el contenedor se elimina o se recrea.

- Volúmenes Compartidos: Se pueden compartir entre múltiples contenedores, permitiendo que todos accedan a los mismos datos.
- Montajes Bind: Permiten montar un directorio específico del host en un contenedor, dándole acceso directo al sistema de archivos del host.

## Red de Docker (Docker Networking)

Docker proporciona varias opciones de redes para que los contenedores se comuniquen entre sí y con el mundo exterior:

- Bridge Network: Es la red predeterminada que Docker crea para los contenedores en un solo host. Permite la comunicación entre contenedores en el mismo host.
- Host Network: En esta red, el contenedor comparte la pila de red del host, eliminando el aislamiento de red entre el contenedor y el host.
- Overlay Network: Permite la comunicación entre contenedores que se ejecutan en diferentes hosts en un entorno de clúster.
- Macvlan Network: Asigna una dirección MAC al contenedor, haciéndolo aparecer como un dispositivo físico en la red.

## Registro de Docker (Docker Registry)

El registro de Docker es un sistema para almacenar y distribuir imágenes de Docker. Los registros pueden ser públicos (como Docker Hub) o privados. Cuando se construye una imagen, se puede "empujar" a un registro, desde donde otros usuarios pueden "tirar" de la imagen para usarla en sus sistemas.

- Docker Hub: Es el registro público más popular y contiene una gran cantidad de imágenes oficiales y comunitarias.
- Registro Privado: Las organizaciones también pueden configurar sus propios registros privados para almacenar imágenes de Docker que no desean hacer públicas.

## Orquestación (Docker Swarm y Kubernetes)

Docker también tiene capacidades de orquestación para gestionar múltiples contenedores en un clúster de máquinas.

- Docker Swarm: Es la herramienta de orquestación integrada de Docker que permite gestionar un clúster de nodos y distribuir contenedores entre ellos.
- Kubernetes: Es otra popular herramienta de orquestación de contenedores que puede integrarse con Docker para gestionar contenedores en un clúster de manera más avanzada.
