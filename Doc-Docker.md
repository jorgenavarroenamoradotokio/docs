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

# Ventajas

- Portabilidad: Los contenedores pueden ejecutarse en cualquier sistema operativo que tenga Docker instalado, lo que facilita mover aplicaciones entre entornos de desarrollo, prueba y producción.
- Aislamiento: Cada contenedor funciona de manera aislada, lo que significa que no interfiere con otras aplicaciones en el mismo sistema.
- Escalabilidad: Docker facilita la creación de aplicaciones escalables al permitir la implementación de múltiples contenedores en paralelo.
- Eficiencia: Los contenedores comparten el kernel del sistema operativo, lo que los hace más ligeros y eficientes en el uso de recursos que las máquinas virtuales.

# Arquitectura

Docker está compuesta por varios componentes clave que trabajan juntos para permitir la creación, administración y ejecución de contenedores

## Diagrama de la arquitectura

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

- Capas de Imagen: Las imágenes de Docker están compuestas por capas. Cada instrucción en el Dockerfile crea una nueva capa en la imagen. Esto permite la reutilización de capas entre imágenes, lo que hace que la creación y distribución de imágenes sea más eficiente.
  - FROM: sistema/herramienta principal que permite la ejecucion de la imagen (sistema operativo, libreia de lenguaje, etc)
  - WORKDIR: estable el directorio de trabajo
  - COPY: copia archivos desde el sistema de archivos del host a la imagen
  - RUN: ejecuta comandos dentro de la imagen para instalar las dependencias 
  - CMD: define el comando que se ejecutara cuando inicie el contenedor basado en en la imagen

- Dockerfile: Un archivo de texto con una serie de instrucciones que especifican cómo construir una imagen. Define la base de la imagen (por ejemplo, un sistema operativo), las dependencias, la configuración, y los comandos que deben ejecutarse dentro del contenedor.

```dockerfile
# Selecciona una imagen base
FROM centos:7
# Ejecutar la imagen
RUN yum -y install httpd
# Define el comando por defecto para ejecutar la aplicación
CMD ["apachectl", "-DFOREGROUND"]
```

## Contenedores de Docker

Un contenedor es una instancia en ejecución de una imagen de Docker. Representa una aplicación en ejecución con todo lo necesario para funcionar de manera aislada. Los contenedores son ligeros y comparten el núcleo del sistema operativo con otros contenedores, pero cada uno tiene su propio sistema de archivos, red y espacio de proceso.

- Aislamiento: Los contenedores se ejecutan de manera aislada, lo que significa que no pueden interferir con otros contenedores en el sistema.
- Persistencia: Aunque los contenedores son efímeros, los datos se pueden persistir utilizando volúmenes, que permiten almacenar datos fuera del contenedor y compartirlos entre contenedores.

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
