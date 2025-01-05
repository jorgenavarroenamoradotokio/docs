<div align="center">
  <img src="https://raw.githubusercontent.com/jorgenavarroenamoradotokio/docs/feature/git/logos/Git-Logo.svg">
</div>

## Índice
- [Introducción](#introducción)
  - [Principales funciones](#principales-funciones)
  - [Princiaples objetivos](#princiaples-objetivos)
  - [Comparacion entre Gradle, Ant y Maven](#comparacion-entre-gradle-ant-y-maven)
    - [Maven vs Ant](#maven-vs-ant)
    - [Maven vs Gradle](#maven-vs-gradle)
- [Instalacion y configuración del Entorno](#instalacion-y-configuración-del-entorno)
  - [Instalacion simple](#instalacion-simple)
    - [Requisitos Previos](#requisitos-previos)
    - [Procedimiento de Instalación](#procedimiento-de-instalación)
  - [Instalaccion avanzada Mediante gestora de paquetes](#instalaccion-avanzada-mediante-gestora-de-paquetes)
  - [Intalacion en entornos de docker](#intalacion-en-entornos-de-docker)
  - [Configuracion de multiples versiones Maven (versiones paralelas)](#configuracion-de-multiples-versiones-maven-versiones-paralelas)
  - [Configuración Maven](#configuración-maven)
    - [Ubicación predeterminada](#ubicación-predeterminada)
    - [Modificación de la ruta de Maven (repositorio local o configuración)](#modificación-de-la-ruta-de-maven-repositorio-local-o-configuración)
    - [Ejecutar Maven desde un proxy](#ejecutar-maven-desde-un-proxy)
    - [Modificar repositorio central](#modificar-repositorio-central)
- [Arquitectura Maven](#arquitectura-maven)
  - [Modelo POM](#modelo-pom)
    - [Propiedades del POM](#propiedades-del-pom)
  - [Tipos de repositorios Maven](#tipos-de-repositorios-maven)
    - [Repositorio local](#repositorio-local)
    - [Repositorio remoto](#repositorio-remoto)
    - [Repositorio central](#repositorio-central)
    - [Repositorio de empresa o privado](#repositorio-de-empresa-o-privado)
    - [dependencyManagement](#dependencymanagement)
  - [Ciclo de vida de Maven](#ciclo-de-vida-de-maven)
    - [Ciclo de vida Clean](#ciclo-de-vida-clean)
    - [Ciclo de Vida Default](#ciclo-de-vida-default)
    - [Ciclo de Vida Site](#ciclo-de-vida-site)
    - [Personalización del Ciclo de Vida](#personalización-del-ciclo-de-vida)
      - [Plugins](#plugins)
      - [Bindings](#bindings)
  - [Convenciones Predeterminadas](#convenciones-predeterminadas)
  - [Carpeta target](#carpeta-target)
- [Perfiles](#perfiles)
  - [Perfiles en POM](#perfiles-en-pom)
  - [Perfiles en settings](#perfiles-en-settings)
- [Crear un proyecto](#crear-un-proyecto)
  - [Comandos](#comandos)

# Introducción

Es una herramienta de gestion de proyectos de proyectos para multiples lenguajes de programacion como java, c#, Ruby, Scala y frameworks como spring mvc y spring boot.
Para poder realizar todas estas funciones Maven usa un archivo xml (documento pom.xml) donde describe como se va a construir y generar el proyecto software.

## Principales funciones

- La gestion de dependencias del proyecto
- Compilar el codigo fuente
- Empaquetar el codigo (war, jar, zip...)
- Instalar los paquetes de un repositorio en local
- Generar documentacion a partir del codigo fuente
- Gestionar las distintas fdases del ciclo de vida (build, validacion, generacion del codigo fuente, procesamiento, compilacion, testing)

## Princiaples objetivos

- Permitir que un desarollador comprenda el estado completo de un producto en el menor tiempo posible.
- Reducir la complejidad del proceso de construccion.
- Fomentar las mejores practicas de desarrollo.

## Comparacion entre Gradle, Ant y Maven
Aunque Maven revolucionó la gestión de proyectos en Java, otras herramientas como Gradle y Ant ofrecen alternativas según las necesidades específicas:

### Maven vs Ant

- Ant: Proporciona un enfoque imperativo basado en scripts XML, donde el desarrollador define explícitamente las tareas y su orden de ejecución.
Es extremadamente flexible, pero esta flexibilidad a menudo implica complejidad, ya que carece de un sistema integrado de gestión de dependencias.
Casos de uso óptimos: proyectos con requisitos altamente personalizados o sistemas heredados que ya dependen de scripts Ant.

- Maven: Enfoque declarativo con POM, lo que facilita la configuración y estandarización de proyectos.
Gestión automática de dependencias mediante repositorios locales, centrales y remotos.
Casos de uso óptimos: proyectos Java empresariales que buscan consistencia, mantenimiento a largo plazo y compatibilidad con prácticas modernas de CI/CD.

### Maven vs Gradle

- Gradle: Combina lo mejor de ambos mundos (imperativo y declarativo) con scripts basados en Groovy o Kotlin.
Ofrece un rendimiento superior gracias a la construcción incremental y el almacenamiento en caché de tareas.
Soporte avanzado para proyectos multilingües y multiplataforma.
Casos de uso óptimos: proyectos grandes y modernos con requisitos de rendimiento y flexibilidad, como aplicaciones móviles en Android o entornos poliglota.
- Maven: Más rígido y menos flexible que Gradle, pero esta rigidez garantiza estructuras consistentes.
Amplia documentación y una comunidad madura, lo que lo hace ideal para equipos que prefieren convenciones en lugar de configuraciones.


# Instalacion y configuración del Entorno

## Instalacion simple

### Requisitos Previos

- Java Development Kit (JDK): Es fundamental asegurarse de contar con una versión 8 o superior del JDK, dado que Maven depende directamente del entorno Java para ejecutar sus procesos. Es recomendable utilizar la última versión compatible para maximizar la estabilidad y el rendimiento.
- Variables de entorno esenciales:
  - JAVA_HOME: Representa la ruta donde se encuentra instalado el JDK.
  - MAVEN_HOME: Aunque opcional, puede ser útil para configuraciones avanzadas.
  - PATH: Incluir el directorio binario de Maven permite ejecutar comandos desde cualquier ubicación en el sistema.

### Procedimiento de Instalación

- Acceda al sitio oficial de Apache Maven (https://maven.apache.org/download.cgi) y descargue la versión más reciente disponible.
- Extraiga el archivo comprimido en un directorio específico de su elección.
- Configure las variables de entorno en función de su sistema operativo:
- En Windows: Modifique las variables de entorno desde la configuración avanzada del sistema.
- En Linux/Mac: Edite los archivos ~/.bashrc o ~/.zshrc para añadir las rutas correspondientes.
- Ejecute mvn -v para validar que Maven está correctamente instalado. Este comando debe mostrar información detallada sobre la versión de Maven y el entorno Java asociado.

## Instalaccion avanzada Mediante gestora de paquetes

Los gestores de paquetes simplifican la instalación y actualización de Maven en sistemas operativos modernos. Cada gestor tiene características específicas:
- Homebrew (macOS y Linux): Homebrew instala Maven en directorios estándar como /usr/local/Cellar. Esto facilita el acceso global y evita conflictos de versiones. Sin embargo, si se necesitan versiones específicas, se pueden emplear herramientas adicionales como brew switch o instalar Maven manualmente.
```bash
brew install maven # Instalaccion 
brew upgrade maven # Actualizacion
```
- Chocolatey (Windows): Chocolatey automatiza la gestión de dependencias y asegura compatibilidad con las configuraciones predeterminadas del sistema Windows.
```bash
choco install maven # Instalaccion 
choco upgrade maven # Actualizacion
```
- SDKMAN (Linux, macOS, Windows Subsystem for Linux - WSL): es particularmente útil en entornos de desarrollo donde se requieren múltiples versiones de Maven.
```bash
sdk install maven # Instalaccion 
sdk use maven <versión> # Cambiar entre las diferentes versiones
sdk list maven # Listar versiones disponibles
```
## Intalacion en entornos de docker

Docker permite encapsular entornos Maven reproducibles. Esto es útil para entornos de integración continua (CI/CD) y para evitar discrepancias entre sistemas de desarrollo y producción.
```dockerfile
FROM maven:3.8.6-jdk-11
WORKDIR /usr/src/app
COPY . .
RUN mvn clean install
CMD ["mvn", "exec:java"]
```
Uso con dependencias específicas: Se pueden montar volúmenes para compartir el directorio .m2 entre el host y el contenedor:
```bash
docker run -it --rm \
  -v ~/.m2:/root/.m2 \
  -v $(pwd):/usr/src/app \
  maven:3.8.6-jdk-11 mvn clean install
```

## Configuracion de multiples versiones Maven (versiones paralelas)

En equipos que trabajan con múltiples proyectos, puede ser necesario manejar varias versiones de Maven simultáneamente.
- Instalación manual de versiones paralelas:
Descargar versiones específicas desde el sitio oficial: https://maven.apache.org/download.cgi.
Descomprimir en directorios separados:
```bash
mkdir -p ~/tools/maven
tar -xzvf apache-maven-3.6.3-bin.tar.gz -C ~/tools/maven/
tar -xzvf apache-maven-3.8.6-bin.tar.gz -C ~/tools/maven/
```
- Configuración de M2_HOME y PATH:
  - En el archivo ~/.bashrc o ~/.zshrc:
  ```bash
  export M2_HOME=~/tools/maven/apache-maven-3.8.6
  export PATH=$M2_HOME/bin:$PATH
  ```
  - Para cambiar dinámicamente entre versiones, se pueden definir alias
  ```bash
  alias mvn3.6="export M2_HOME=~/tools/maven/apache-maven-3.6.3 && export PATH=$M2_HOME/bin:$PATH"
  alias mvn3.8="export M2_HOME=~/tools/maven/apache-maven-3.8.6 && export PATH=$M2_HOME/bin:$PATH"
  ```
  - Uso de SDKMAN para gestionar versiones: SDKMAN automatiza el cambio de versiones:
  ```bash
  sdk use maven <versión>
  ```

## Configuración Maven

Una de las características clave de Maven es su capacidad para gestionar dependencias y almacenar artefactos en un repositorio local. 
De forma predeterminada, Maven utiliza una ubicación específica en tu sistema para almacenar estas dependencias y configuraciones. Sin embargo, en ocasiones, 
puede ser necesario modificar esta ubicación para adaptarse a las necesidades de un entorno de desarrollo específico, ya sea por razones de rendimiento, espacio en disco, o preferencias organizativas.

Las propiedades que puedes modificar son las siguientes
- LocalRepository: Indica el path donde se almacenarán todos los repositorios y librerías que necesita nuestros proyectos para funcionar
- Offline: Indica si Maven debe de operar en modo fuera de línea, lo que permitirá si debe descargar actualizaciones o dependencias si no están disponibles
- Proxies: Se emplea para indicar la información de los servidores proxy
- Mirror: Se emplea para descagra dependencias de un repositorio espejo, esto quiere decir que evita descargar dependencias del repositorio central de Maven y lo obtiene desde otro como puede ser nexus.
- Repositories: Permite configurar los tipos de repositorios relases o snapshots
- PluginRepositories: Almacena bibliotecas de complementos y archivos asociados
- Server: Es empelado para almacenar usuarios, contraseñas, llaves privadas, etc

### Ubicación predeterminada 

La carpeta de Maven contiene los archivos que Maven usa para gestionar las dependencias y la configuración. Por defecto, estas son las ubicaciones en distintos sistemas operativos:

- En sistemas operativos basados en UNIX (Linux/macOS):
    - Repositorio local: El repositorio local, donde Maven almacena las dependencias, se encuentra en: ```~/.m2/repository```
    - Archivo de configuración: El archivo de configuración settings.xml está en:```~/.m2/settings.xml```
- En sistemas operativos Windows:
    - Repositorio local: La ubicación predeterminada del repositorio local es: ```C:\Users\<nombre_de_usuario>\.m2\repository```
    - Archivo de configuración: El archivo settings.xml se encuentra en: ```C:\Users\<nombre_de_usuario>\.m2\settings.xml```
  
### Modificación de la ruta de Maven (repositorio local o configuración)

Para ello debermos de buscar primero la carpeta .m2 y crear en ella el fichero settings.xml en el definiremos el path donde querremos que se almacenen los artefactos para los proyectos.
En caso de no estar en .m2 el documento settings.xml puede estar en la carpeta conf de la carpeta de instalación de Maven

```xml
<?xml version="1.0" encoding="UTF-8"?>
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                              http://maven.apache.org/xsd/settings-1.0.xsd">
    <localRepository>/ruta/a/tu/nueva/carpeta</localRepository>
</settings>
```
### Ejecutar Maven desde un proxy

Cuando necesites acceder a recursos en línea a través de un servidor proxy (por ejemplo, cuando trabajes en una red corporativa o detrás de un firewall que requiera un proxy). 
Simplemente añade la sección <proxies> con la configuración adecuada para tu entorno.

```xml
<proxies>
    <proxy>
        <id>my-proxy</id>
        <active>true</active>
        <protocol>http</protocol>
        <host>proxy.example.com</host>
        <port>8080</port>
        <username>proxyuser</username>
        <password>somepassword</password>
        <nonProxyHosts>www.google.com|*.example.com</nonProxyHosts>
    </proxy>
</proxies>
```
### Modificar repositorio central 

Cuando quieras que Maven acceda a repositorios específicos para obtener dependencias, plugins o artefactos. Esto es especialmente útil cuando trabajas con repositorios 
internos de tu organización o repositorios personalizados, además del repositorio central predeterminado de Maven (Maven Central).

```xml
<repositories>
  <repository>
    <id>central</id>
    <url>https://repo.maven.apache.org/maven2</url>
  </repository>
</repositories>
```

# Arquitectura Maven
La arquitectura de Maven se fundamenta en componentes clave que garantizan la gestión integral de proyectos:
- Modelo POM (Project Object Model): El archivo POM (pom.xml) es el nodo central de configuración en Maven. Contiene metadatos esenciales del proyecto, dependencias, configuraciones de plugins y definiciones específicas para la ejecución del ciclo de vida.
- Repositorios: Maven utiliza repositorios para gestionar artefactos y dependencias.
- Ciclo de Vida del Build: El proceso de construcción en Maven se organiza en fases, agrupadas en ciclos de vida estandarizados que permiten ejecutar tareas secuenciales.
  - Sistema de Plugins:Los plugins son el motor funcional de Maven. Permiten ejecutar tareas como compilación, pruebas, empaquetado y generación de reportes, entre otras.
- Convenciones Predeterminadas: Maven minimiza configuraciones manuales mediante convenciones como la estructura estándar de proyectos y la resolución automática de dependencias transativas.
- Carpeta target

## Modelo POM

El archivo POM (pom.xml) es el nodo central de configuración en Maven. Contiene metadatos esenciales del proyecto, como el identificador del proyecto, la versión, el empaquetado y las dependencias.
Esta compuesto por las siguientes partes:
- ModelVersion: ndica la versión del esquema del modelo POM que se está utilizando. Actualmente, la versión estándar es 4.0.0.
- groupId: Proporciona un identificador único para la organización o grupo al que pertenece el proyecto. Este suele reflejar la estructura inversa del dominio de la empresa (por ejemplo, com.empresa.proyecto).
- artifactId: Representa el nombre único del proyecto dentro del grupo. Es crucial para identificar el artefacto generado.
- version: Denota la versión específica del proyecto, útil para identificar instancias específicas en desarrollo o producción (e.g., 1.0-SNAPSHOT).
- packaging: Define el tipo de empaquetado del proyecto, como jar, war, pom, zip, entre otros. Por defecto, se utiliza jar.
- dependencies: Describe todas las dependencias requeridas para compilar, probar y ejecutar el proyecto, incluyendo bibliotecas de terceros y módulos internos.
- parent: Permite establecer relaciones jerárquicas entre proyectos, facilitando la herencia de configuraciones comunes desde un POM padre.
- modules: Específica los módulos hijos en proyectos modulares, habilitando la construcción conjunta y coordinada de múltiples componentes.
- properties: Introduce variables reutilizables dentro del archivo POM. Se pueden referenciar usando la sintaxis ${nombre}.
- plugins: Define herramientas adicionales que extienden las capacidades del ciclo de vida del proyecto, como compiladores, analizadores de calidad o generadores de documentación.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>advanced-project</artifactId>
    <version>1.0.0</version>
    <packaging>jar</packaging>

    <!-- 1. Propiedades dinámicas y reutilizables -->
    <properties>
        <java.version>17</java.version>
        <spring.version>3.0.0</spring.version>
        <encoding>UTF-8</encoding>
        <project.build.sourceEncoding>${encoding}</project.build.sourceEncoding>
        <project.reporting.outputEncoding>${encoding}</project.reporting.outputEncoding>
    </properties>

    <!-- 2. Dependency Management -->
    <dependencyManagement>
        <dependencies>
            <!-- Importación de BOM -->
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-dependencies</artifactId>
                <version>${spring.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>

            <!-- Dependencias centralizadas para múltiples módulos -->
            <dependency>
                <groupId>org.apache.commons</groupId>
                <artifactId>commons-lang3</artifactId>
                <version>3.12.0</version>
            </dependency>
        </dependencies>
    </dependencyManagement>

    <!-- 3. Dependencias -->
    <dependencies>
        <!-- Dependencia regular -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter</artifactId>
        </dependency>

        <!-- Dependencias específicas para entornos -->
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <!-- 4. Perfiles avanzados -->
    <profiles>
        <!-- Perfil de desarrollo -->
        <profile>
            <id>development</id>
            <activation>
                <activeByDefault>true</activeByDefault>
            </activation>
            <properties>
                <env>dev</env>
                <db.url>jdbc:h2:mem:dev</db.url>
            </properties>
        </profile>

        <!-- Perfil de pruebas -->
        <profile>
            <id>testing</id>
            <properties>
                <env>test</env>
                <db.url>jdbc:h2:mem:test</db.url>
            </properties>
        </profile>

        <!-- Perfil de producción -->
        <profile>
            <id>production</id>
            <properties>
                <env>prod</env>
                <db.url>jdbc:postgresql://prod-db-server:5432/prod</db.url>
            </properties>
        </profile>
    </profiles>

    <!-- 5. Configuración avanzada de plugins -->
    <build>
        <plugins>
            <!-- Plugin de compilación -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.10.1</version>
                <configuration>
                    <source>${java.version}</source>
                    <target>${java.version}</target>
                </configuration>
            </plugin>

            <!-- Plugin de empaquetado -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-assembly-plugin</artifactId>
                <version>3.5.0</version>
                <configuration>
                    <descriptorRefs>
                        <descriptorRef>jar-with-dependencies</descriptorRef>
                    </descriptorRefs>
                    <archive>
                        <manifest>
                            <mainClass>com.example.MainApplication</mainClass>
                        </manifest>
                    </archive>
                </configuration>
                <executions>
                    <execution>
                        <id>make-assembly</id>
                        <phase>package</phase>
                        <goals>
                            <goal>single</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```
### Propiedades del POM

Las propiedades en el POM permiten flexibilidad al habilitar la parametrización en tiempo de ejecución. Algunos tipos de propiedades incluyen:
- Variables de entorno: Prefijadas con env, permiten acceder a variables del sistema operativo.
- Variables estándar del POM: Utilizan el prefijo project para acceder a valores como la versión o el artefacto.
- Variables de configuración: Relacionadas con ajustes del entorno de Maven, prefijadas con settings.
- Propiedades personalizadas: Especificadas dentro de <properties> en el POM.

## Tipos de repositorios Maven

En Maven, un repositorio es un lugar donde se almacenan los artefactos (como JAR, WAR, EAR) generados y 
utilizados en los proyectos. Existen tres tipos principales de repositorios en Maven: local, remoto y central.
Maven utiliza estos repositorios para gestionar las dependencias de un proyecto, y cada tipo tiene un propósito específico.

### Repositorio local

El repositorio local es una carpeta en el sistema de archivos de tu máquina local, que Maven crea cuando ejecutas la primera construcción de un proyecto.
Los artefactos que descargues o instales en tu proyecto, como las dependencias y los artefactos generados, se almacenan en este repositorio. El repositorio local se encuentra en el siguiente directorio:
- En sistemas Unix o Linux: ~/.m2/repository
- En sistemas Windows: C:\Users\<usuario>\.m2\repository
- Ruta configurada ([Modificación de la ruta de Maven (repositorio local o configuración)](#modificación-de-la-ruta-de-maven-repositorio-local-o-configuración))

### Repositorio remoto

Un repositorio remoto es un servidor centralizado donde Maven almacena artefactos compartidos entre los proyectos. Los repositorios remotos más comunes son el repositorio central de Maven y los 
repositorios privados de empresas o proyectos. Cuando Maven no encuentra una dependencia en el repositorio local, buscará en los repositorios remotos. Si la dependencia está disponible, 
Maven la descargará y la almacenará en el repositorio local para su uso futuro.

### Repositorio central

El repositorio central es un repositorio público mantenido por la comunidad de Maven, que contiene millones de artefactos como bibliotecas y frameworks. Este repositorio es accesible para todos los 
desarrolladores y es la fuente principal de dependencias que Maven utiliza. El repositorio central está preconfigurado en Maven, por lo que no necesitas especificarlo en el archivo settings.xml 
a menos que desees modificar la configuración.

### Repositorio de empresa o privado

Las empresas a menudo tienen repositorios privados donde almacenan sus propias bibliotecas internas o versiones personalizadas de bibliotecas comunes.
Estos repositorios pueden estar alojados en servidores locales o en servicios como Nexus, Artifactory o GitHub Packages. Se configuran en el archivo settings.xml o pom.xml de la siguiente manera.

### dependencyManagement

El uso de <dependencyManagement> centraliza las versiones de las dependencias, evitando conflictos en proyectos multi-módulo. Por ejemplo, la versión de commons-lang3 se aplica uniformemente a todos los módulos que la utilicen.

## Ciclo de vida de Maven

El ciclo de vida de Maven o tambien conocido como Maven LifeCycle son los estados por los que pasa el proyecto hasta que genera el entregable.
Maven organiza su flujo de trabajo mediante tres ciclos de vida principales, cada uno diseñado para cubrir una etapa esencial en el desarrollo de software:

### Ciclo de vida Clean 

El ciclo de vida clean se utiliza para preparar el entorno de construcción eliminando artefactos generados en compilaciones previas.
Fases:
- pre-clean: Ejecuta tareas previas a la limpieza.
- clean: Elimina los artefactos generados en la construcción previa (por defecto, elimina el directorio target).
- post-clean: Realiza tareas después de la limpieza.

### Ciclo de Vida Default

Contiene las fases esenciales para construir, probar y empaquetar el proyecto.
Fases
- Validate: Esta fase se encarga simplemente de validar que el proyecto dispone de toda la información necesaria para ser procesado.
- Compile: Es quizás una de las fases más importante de la gestión de un proyecto Maven ya que se encarga de compilar los ficheros fuentes .java y generar en las carpetas de destino los compilados.
- Test: Esta es otra de las fases principales en las cuales una vez se ha compilado el código se ejecutan las pruebas unitarias que se han construido para él. De esta forma nos aseguramos que nuestro código es correcto y no nos llevaremos ninguna sorpresa en producción
- Package: Esta es otra de las fases que a mí me parecen fundamentales ya que se encarga de empaquetar nuestro código a un formato standard de Java que permita su ejecución o despliegue en servidor
- Verify: Esta fase del ciclo de vida se encarga de lanzar los test de integración para confirmar que todo funciona correctamente y que la calidad es la correcta.
- Install: Es otra de las fases más importantes cuando trabajas con Maven ya que se encarga de desplegar el artefacto en el repositorio local con su versionado de tal forma que otros artefactos puedan hacer uso de él. Hasta este punto se abordan las fases más habituales de trabajar con Maven ya disponemos del artefacto instalado en el repositorio y otros artefactos lo podrán añadir a sus dependencias sin ningún problema
- Deploy: Esta fase cuesta mucho entenderla a los desarrolladores ya que ejecutar un Maven Deploy muchas veces en un entorno meramento local no se realiza. Sin embargo, es una fase clave cuando disponemos de una serie de artefactos que deseamos compartir entre desarrollos ya que permite desplegar el artefacto en un servidor remoto de tal forma que otros desarrolladores puedan utilizarlo.

### Ciclo de Vida Site

Genera documentación y reportes relacionados con el proyecto.
Fases:
- pre-site: Realiza tareas previas a la generación del sitio.
- site: Genera la documentación del proyecto.
- post-site: Realiza tareas después de la generación del sitio.
- site-deploy: Publica la documentación generada en un servidor remoto.

### Personalización del Ciclo de Vida

La flexibilidad de Maven reside en su capacidad para adaptarse a las necesidades específicas de un proyecto o entorno corporativo.
Esto se logra mediante el uso de plugins y bindings personalizados, que permiten ampliar o modificar el comportamiento predeterminado de los ciclos de vida. 
Esta sección explora cómo aprovechar estas características para implementar flujos de trabajo personalizados y optimizados.

#### Plugins

Los plugins son piezas fundamentales que habilitan la ejecución de tareas específicas durante el ciclo de vida. Ejemplos destacados incluyen:
- maven-compiler-plugin: Para compilar código fuente Java.
- maven-surefire-plugin: Para ejecutar pruebas unitarias.
- maven-jar-plugin: Para empaquetar artefactos JAR.

#### Bindings

Los bindings permiten asociar la ejecución de tareas de plugins con fases específicas del ciclo de vida, habilitando así una gran flexibilidad para personalizar la construcción de proyectos.
- Por defecto, Maven define bindings implícitos para la mayoría de los plugins oficiales. Sin embargo, es posible sobrescribir o extender estos bindings para satisfacer requisitos específicos.

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-antrun-plugin</artifactId>
    <version>3.0.0</version>
    <executions>
        <execution>
            <phase>generate-sources</phase>
            <goals>
                <goal>run</goal>
            </goals>
            <configuration>
                <tasks>
                    <echo>Generando código fuente...</echo>
                </tasks>
            </configuration>
        </execution>
    </executions>
</plugin>
```

- Ejecución Condicional mediante Perfiles
En entornos donde se requiere flexibilidad basada en condiciones específicas, como el ambiente de despliegue o características del proyecto, los perfiles permiten activar plugins y bindings de manera condicional.

```xml
<profiles>
    <profile>
        <id>testing</id>
        <activation>
            <property>
                <name>env</name>
                <value>test</value>
            </property>
        </activation>
        <build>
            <plugins>
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-surefire-plugin</artifactId>
                    <configuration>
                        <skipTests>false</skipTests>
                    </configuration>
                </plugin>
            </plugins>
        </build>
    </profile>
</profiles>
```
- En escenarios donde los plugins existentes no cumplen con necesidades específicas, se pueden desarrollar plugins personalizados.
Pasos principales para crear un plugin:
  - Crear un proyecto Maven con el arquetipo maven-archetype-plugin.
  - Implementar lógica personalizada mediante código Java.
  - Empaquetar y desplegar el plugin en un repositorio accesible para todos los proyectos relevantes.

```xml
<plugin>
    <groupId>com.miempresa.plugins</groupId>
    <artifactId>mi-plugin-personalizado</artifactId>
    <version>1.0.0</version>
    <executions>
        <execution>
            <phase>validate</phase>
            <goals>
                <goal>mi-tarea</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

## Convenciones Predeterminadas

En maven existe una estructura de directorios estándar. Aunque esta estructura se puede modificar vía descriptor del proyecto (osea pom.xml mediante los elementos sourceDirectory, outputDirectory, warSourceDirectory, webXml, warName, etc.) la recomendación en la página web de maven es que nos ajustemos lo máximo que podamos a las estructura que ya viene predefinida.
- La estructura de directorio es muy importante ya que por ejemplo si quisiéramos crear un war directamente desde maven podríamos hacerlo, pero colocando antes de una aplicación web en j2ee en su correspondiente carpeta de maven. Por ejemplo, las páginas y otros recursos como tags, applets y el fichero web.xml se deben de encontrar en src/main/webapp.
  - src/main/java	Ficheros de código fuente .java.
  - src/main/resources	Todo lo que queramos que se copie cuando se cree la carpeta del proyecto en target.
  - src/main/filters *	Ficheros para los filtros.
  - src/main/assembly *	Ficheros para el ensamblaje. En proyectos que se componen de varios subproyectos.
  - src/main/config	Ficheros de configuración.
  - src/main/webapp	Páginas y otros recursos como css, imágenes, ficheros js, applets y el fichero web.xml (en webapp/WEB-INF/web.xml).
  - src/test/java	Código fuente de las pruebas del proyecto.
  - src/test/resources	Recursos para las pruebas.
  - src/test/filters *	Filtros para las pruebas.
  - src/site	Carpeta que contiene todos los ficheros necesarios para la generación automática del sitio web con la información del proyecto. La generación del sitio se explicará más adelante.
  - target	Es el directorio destino de todo build en maven. Vamos todo el código compilado el proyecto, de las pruebas, los ficheros .jar .war etc. cuando empaquetemos el proyecto, la carpeta con el sitio web generado, todo se crea bajo la carpeta target.
  - LICENSE.txt	Proyecto donde se describen las licencias usadas para el proyecto.
  - README.txt	El fichero readme de introducción al proyecto
- Gestionar dependencias de manera automática. El sistema de dependencias de Maven incluye:
  - Resolución transitiva de dependencias: Maven identifica y descarga no solo las dependencias directas del proyecto, sino también las dependencias de estas, garantizando que se disponga de todas las bibliotecas necesarias
  - Scope: El scope determina el alcance en el que las dependencias serán utilizadas en el proyecto. Dfine cuando y como esas despendencias estarán disponibles en el proceso de compilación y ejecución.
    - Compile: Este es el scope por defecto. Las dependencias con este scope están disponibles en todas las fases del proyecto (compilación, prueba, ejecución).
    - Provided: Las dependencias con este scope están disponibles en tiempo de compilación y prueba, pero se espera que estén provistas por el entorno de ejecución, por ejemplo, por el contenedor de servlets en una aplicación web.
    - Runtime: Las dependencias con este scope no son requeridas para la compilación, pero sí para la ejecución. Por lo tanto, estarán presentes en tiempo de ejecución y durante las pruebas, pero no se utilizarán durante la compilación.
    - Test: Este scope solo es relevante durante la ejecución de pruebas, no durante la compilación ni la ejecución del proyecto principal.
    - System: Las dependencias con este scope son similares a las de compile, pero deben ser proporcionadas explícitamente y se utilizan en el entorno de desarrollo. Maven no maneja estas dependencias ni las descarga del repositorio remoto.
    - Import: Este scope solo se usa en la sección <dependencyManagement>, permitiendo manejar la versión de la dependencia y la exclusión de transitorios en archivos POM separados.
  - Gestión de versiones: Permite definir versiones específicas de dependencias, evitando conflictos o inconsistencias entre bibliotecas.

## Carpeta target

Contiene todo los documentos generados durante el ciclo de vida de Maven organizados en carpetas
- carpeta classes: almacena los archivos fuente compilados
- carepta test-class: almacena los archivos fuente de prueba compilados
- carpeta surerifere-reports: almacena los informes de pruebas
- archivo .jar/.war/.ear es el artefacto generado del proyecto
- maven-archiver y maven-status contiene la informacion utilizada por maven durante la compilación.

# Perfiles 
Los perfiles permiten configurar el proyecto para diferentes entornos. Cada perfil puede contener configuraciones específicas como URLs de bases de datos, variables de entorno y otras propiedades.
Los perfiles se pueden agrupar de la siguiente manera.
- Por proyecto, definidos en el propio POM
- Por usuario, definido en la configuración de Maven (definidos en m.2/settings.xml)
- Global, definido en la configuración global de Maven (conf/settings.xml)
Como dato importante si el perfil definido en el archivo pom esta activo en el fichero de settings.xml prevalecerá la configuración definida en el settings

## Perfiles en POM

Para poder crearlo se realizará dentro de las etiqueta profile con las siguientes propiedades
- id: es un identificador único dentro de un perfil en el archivo
- activation: se usa dentro de un perfil para especificar las condiciones bajo las cuales se activa ese perfil. Las condiciones de activación pueden basarse en variables como la propiedad del sistema, la presencia de un archivo o el entorno del sistema operativo 
  Propiedades posibles dentro de <activation>
  - <activeByDefault>: Si se establece en true, el perfil se activa por defecto, a menos que se indique lo contrario en la línea de comandos.
  - <property>: Activa el perfil si una propiedad específica está definida con un valor determinado.
  - <file>: Activa el perfil si un archivo o directorio específico existe.
  - <jdk>: Activa el perfil según la versión de JDK.
  - <os>: Activa el perfil dependiendo del sistema operativo.
- properties: Permite definir propiedades específicas del perfil que sobrescribirán las propiedades globales definidas en el archivo pom.xml. Estas propiedades se pueden utilizar en el proyecto y en otros elementos de configuración de Maven, como plugins y dependencias.
- dependencies: Se pueden declarar dependencias específicas para un perfil. Estas dependencias solo se incluirán cuando el perfil esté activo
- build: define la configuración del proceso de construcción del proyecto. Dentro de esta sección se pueden incluir configuraciones de plugins de compilación, directivas de empaquetado, etc. 
- pluginRepositories: En algunos casos, puedes necesitar definir repositorios de plugins específicos para un perfil, por ejemplo, si necesitas utilizar plugins no disponibles en el repositorio central de Maven
- pluginManagement: Puedes configurar la gestión de plugins dentro de un perfil, lo que permite centralizar las versiones de los plugins y configurarlos para su uso cuando se activa el perfil.
- repositorioes: Puedes definir repositorios adicionales desde donde Maven descargará dependencias para ese perfil. Es útil cuando las dependencias no están en el repositorio central de Maven.
- distributionManagement: Define el repositorio donde los artefactos del proyecto deben ser distribuidos cuando el perfil esté activo. Esto puede incluir repositorios de artefactos o sitios de distribución.
- reporting: Define la configuración de los informes generados durante la construcción del proyecto, como los informes de calidad del código o cobertura de pruebas, específicos para el perfil.
- modules: Si tienes un proyecto multi-módulo, puedes usar <modules> dentro de un perfil para incluir módulos específicos que se deben construir o gestionar cuando se active ese perfil. 
- dependencyManagement: se utiliza para gestionar de manera centralizada las versiones de las dependencias, lo que es especialmente útil en proyectos multi-módulo. Aquí se definen las versiones, pero no se descargan directamente; las dependencias de los módulos hijos heredan estas configuraciones.

```xml
<profiles>
    <profile>
        <id>production</id>
        <activation>
            <property>
                <name>env</name>
                <value>prod</value>
            </property>
        </activation>
        <properties>
            <db.url>jdbc:mysql://prod-db-server:3306/mydb</db.url>
            <env>prod</env>
        </properties>
        <dependencies>
            <dependency>
                <groupId>org.springframework</groupId>
                <artifactId>spring-core</artifactId>
                <version>5.2.5.RELEASE</version>
            </dependency>
        </dependencies>
        <build>
            <plugins>
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-compiler-plugin</artifactId>
                    <version>3.8.1</version>
                    <configuration>
                        <source>1.8</source>
                        <target>1.8</target>
                    </configuration>
                </plugin>
            </plugins>
        </build>
        <distributionManagement>
            <repository>
                <id>releases</id>
                <url>https://example.com/releases</url>
            </repository>
        </distributionManagement>
    </profile>
</profiles>
```

## Perfiles en settings

Para poder crealo se realizará dentro de la etiqueta profile con las siguientes propiedades
- id: El identificador único del perfil. Es esencial para activar este perfil de forma explícita desde la línea de comandos o mediante condiciones de activación.
- activation: La sección <activation> define las condiciones bajo las cuales un perfil se activa automáticamente. Puedes activar un perfil en función de:
  - <activeByDefault>: Si se establece en true, el perfil se activa por defecto.
  - <property>: Activa el perfil si una propiedad del sistema tiene un valor específico.
  - <jdk>: Activa el perfil si una versión de JDK específica está siendo utilizada.
  - <os>: Activa el perfil dependiendo del sistema operativo (Linux, Windows, etc.).
  - <file>: Activa el perfil si un archivo o directorio específico existe.
- repositories: Define repositorios adicionales desde los cuales Maven descargará dependencias cuando este perfil esté activo. Esto puede ser útil si necesitas repositorios privados o externos a los predeterminados.
- pluginRepositories: Define repositorios específicos desde los cuales Maven descargará los plugins cuando este perfil esté activo. Esto es útil cuando usas plugins que no están disponibles en los repositorios predeterminados.
- properties: Permite definir propiedades específicas del perfil que sobrescribirán las propiedades definidas globalmente o en el pom.xml. Estas propiedades pueden ser utilizadas en cualquier parte de la construcción de Maven.
- servers: Contiene información sobre los servidores que pueden ser utilizados para la autenticación (por ejemplo, para repositorios privados o para despliegue de artefactos). Es muy útil para definir credenciales de autenticación en entornos privados.
- mirrors: Define mirrors alternativos para repositorios de Maven. Puedes configurar un mirror para los repositorios de Maven Central o cualquier repositorio personalizado.
- proxy: Define un proxy para Maven. Esto es útil en entornos corporativos donde el acceso a Internet está restringido y se requiere un proxy para conectarse a repositorios.
- pluginGroups: Especifica grupos de plugins adicionales. Permite que Maven busque plugins en otros grupos, lo cual es útil cuando se utilizan plugins personalizados o no estándar
```xml
<settings>
    <profiles>
        <profile>
            <id>production</id>
            <activation>
                <property>
                    <name>env</name>
                    <value>production</value>
                </property>
            </activation>
            <repositories>
                <repository>
                    <id>prod-repo</id>
                    <url>https://repo.example.com</url>
                </repository>
            </repositories>
            <pluginRepositories>
                <pluginRepository>
                    <id>prod-plugins</id>
                    <url>https://plugins.example.com</url>
                </pluginRepository>
            </pluginRepositories>
            <properties>
                <env>production</env>
                <db.url>jdbc:mysql://prod-db-server:3306/mydb</db.url>
            </properties>
            <servers>
                <server>
                    <id>prod-repo</id>
                    <username>prod-user</username>
                    <password>prod-password</password>
                </server>
            </servers>
        </profile>
    </profiles>
</settings>
```


# Crear un proyecto

Para crear un proyecto maven se pude realizar de dos maneras, la primera mediante comandos y la segunda usando un plugin del IDE de desarrollo que estemos usando

## Comandos

En caso de querer generar el proyecto mediante opciones del promt usaremos
```bash 
mvn archetype: generate 
``` 
- Si queremos crear un proyecto JAR
```bash
mvn archetype:generate -DgroupId=com.udemy.maven -DartifactId=mi-primer-proyecto-maven -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.4 -DinteractiveMode=false
``` 
- Si queremos crear un proyecto WAR
```bash
mvn archetype:generate -DgroupId=com.udemy.maven -DartifactId=my-webapp -DarchetypeGroupId=org.apache.maven.archetypes -DarchetypeArtifactId=maven-archetype-webapp -DarchetypeVersion=1.4 -DinteractiveMode=false
``` 
- Si quieremos crear un proyecto EAR
```bash
mvn archetype:generate -DgroupId=com.udemy.maven -DartifactId=my-ear-project -DarchetypeGroupId=org.jboss.spec.archetypes -DarchetypeArtifactId=jboss-javaee6-webapp-ear-blank-archetype -DinteractiveMode=false

mvn archetype:generate -DgroupId=com.udemy.maven -DartifactId=my-ear-project-wildfly -DarchetypeGroupId=wildfly-javaee7-webapp-ear-archetype -DarchetypeArtifactId=8.2.0.Final -DinteractiveMode=false
``` 