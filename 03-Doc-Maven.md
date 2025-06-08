<div align="center">
  <img src="https://raw.githubusercontent.com/jorgenavarroenamoradotokio/docs/main/logo/Maven-logo.svg">
</div>

## Índice
- [Introducción](#introducción)
  - [Principales funciones y objetivos](#principales-funciones-y-objetivos)
    - [Principales funciones](#principales-funciones)
    - [Principales objetivos](#principales-objetivos)
  - [Comparación entre Gradle, Ant y Maven](#comparación-entre-gradle-ant-y-maven)
    - [Maven vs Ant](#maven-vs-ant)
    - [Maven vs Gradle](#maven-vs-gradle)
- [Instalación](#instalación)
  - [Instalación simple](#instalación-simple)
    - [Requisitos Previos](#requisitos-previos)
    - [Procedimiento de Instalación](#procedimiento-de-instalación)
  - [Instalación avanzada](#instalación-avanzada)
    - [Mediante gestora de paquetes](#mediante-gestora-de-paquetes)
    - [En entornos de docker](#en-entornos-de-docker)
    - [Configuración de múltiples versiones Maven (versiones paralelas)](#configuración-de-múltiples-versiones-maven-versiones-paralelas)
- [Arquitectura y Ciclo de vida](#arquitectura-y-ciclo-de-vida)
  - [Arquitectura](#arquitectura)
  - [Ciclo de vida](#ciclo-de-vida)
    - [Ciclo de Vida Default](#ciclo-de-vida-default)
    - [Ciclo de Vida Site](#ciclo-de-vida-site)
    - [Personalización del Ciclo de Vida](#personalización-del-ciclo-de-vida)
      - [Plugins](#plugins)
      - [Bindings](#bindings)
- [Archivo POM](#archivo-pom)
  - [dependencyManagement](#dependencymanagement)
  - [Propiedades del POM](#propiedades-del-pom)
  - [Uso de Import para gestión dependencias a través del BOM (Bill of Materials)](#uso-de-import-para-gestión-dependencias-a-través-del-bom-bill-of-materials)
- [Plugins Esenciales y avanzados](#plugins-esenciales-y-avanzados)
  - [maven-clean](#maven-clean)
  - [maven-compiler-plugin: Ajuste de compiladores personalizados](#maven-compiler-plugin-ajuste-de-compiladores-personalizados)
  - [maven-surefire-plugin y maven-failsafe-plugin: Ejecución de pruebas unitarias e integración](#maven-surefire-plugin-y-maven-failsafe-plugin-ejecución-de-pruebas-unitarias-e-integración)
  - [maven-shade-plugin: Empaquetado de JARs con dependencias](#maven-shade-plugin-empaquetado-de-jars-con-dependencias)
  - [maven-dependency-plugin: Manejo avanzado de dependencias](#maven-dependency-plugin-manejo-avanzado-de-dependencias)
  - [maven-resource-plugin](#maven-resource-plugin)
  - [maven-jacoo](#maven-jacoo)
  - [sonar-maven-plugin](#sonar-maven-plugin)
- [Multi-Module Projects](#multi-module-projects)
  - [Beneficios de los proyectos multi-módulo](#beneficios-de-los-proyectos-multi-módulo)
  - [Diseño, organización y estrategia de proyectos multi-módulo](#diseño-organización-y-estrategia-de-proyectos-multi-módulo)
  - [Estrategias para empaquetado y despliegue de módulos relacionados](#estrategias-para-empaquetado-y-despliegue-de-módulos-relacionados)
  - [Dependencias internas entre módulos y su impacto en el ciclo de vida](#dependencias-internas-entre-módulos-y-su-impacto-en-el-ciclo-de-vida)
- [Gestión de Repositorios](#gestión-de-repositorios)
  - [Repositorio local](#repositorio-local)
  - [Repositorio remoto](#repositorio-remoto)
  - [Repositorio central](#repositorio-central)
  - [Repositorio de empresa o privado](#repositorio-de-empresa-o-privado)
- [Perfiles](#perfiles)
  - [Perfiles en POM](#perfiles-en-pom)
  - [Perfiles en settings](#perfiles-en-settings)
- [Gestión de dependencias](#gestión-de-dependencias)
  - [Análisis avanzado de conflictos de versiones (dependency:tree, dependency:analyze)](#análisis-avanzado-de-conflictos-de-versiones-dependencytree-dependencyanalyze)
    - [dependency:tree](#dependencytree)
    - [dependency:analyze](#dependencyanalyze)
  - [Dependencias opcionales y excluidas](#dependencias-opcionales-y-excluidas)
    - [Dependencias Opcionales](#dependencias-opcionales)
    - [Dependencias Excluidas](#dependencias-excluidas)
  - [Estrategias de versionado semántico en dependencias](#estrategias-de-versionado-semántico-en-dependencias)
- [Carpeta target](#carpeta-target)
- [Configuración de settings.xml](#configuración-de-settingsxml)
  - [Tipos de configuración](#tipos-de-configuración)
    - [Combinación de configuraciones globales y locales](#combinación-de-configuraciones-globales-y-locales)
    - [Uso de perfiles](#uso-de-perfiles)
  - [Ubicación predeterminada](#ubicación-predeterminada)
  - [Modificación de la ruta de Maven (repositorio local o configuración)](#modificación-de-la-ruta-de-maven-repositorio-local-o-configuración)
  - [Ejecutar Maven desde un proxy](#ejecutar-maven-desde-un-proxy)
  - [Modificar repositorio central](#modificar-repositorio-central)
- [Documentación y Reportes](#documentación-y-reportes)
  - [JavaDoc](#javadoc)
  - [Informes de Cobertura de Pruebas](#informes-de-cobertura-de-pruebas)
  - [Informes personalizados](#informes-personalizados)
  - [Publicar documentación de mi sitio](#publicar-documentación-de-mi-sitio)
  - [FindBugs/PMD](#findbugspmd)
    - [FindBugs en Maven](#findbugs-en-maven)
    - [PMD](#pmd)
    - [Integración de FindBugs y PMD en un Solo Reporte](#integración-de-findbugs-y-pmd-en-un-solo-reporte)
- [Diagnóstico y Resolución de Problemas en Maven](#diagnóstico-y-resolución-de-problemas-en-maven)
  - [Estrategias depuracion](#estrategias-depuracion)
    - [Uso de -X (modo debug)](#uso-de--x-modo-debug)
    - [Análisis de logs generados por Maven](#análisis-de-logs-generados-por-maven)
  - [Resolución de Dependencias Faltantes o Corruptas](#resolución-de-dependencias-faltantes-o-corruptas)
- [Fichero mvnw (mvnw.cmd)](#fichero-mvnw-mvnwcmd)
  - [Cómo Funciona el Maven Wrapper](#cómo-funciona-el-maven-wrapper)
- [Comandos maven](#comandos-maven)
  

# Introducción
Es una herramienta de gestión de proyectos de proyectos para múltiples lenguajes de programación como java, c#, Ruby, Scala y frameworks como spring mvc y spring boot.
Para poder realizar todas estas funciones Maven usa un archivo xml (documento pom.xml) donde describe cómo se va a construir y generar el proyecto software.

## Principales funciones y objetivos
### Principales funciones
- La gestión de dependencias del proyecto
- Compilar el código fuente
- Empaquetar el código (war, jar, zip...)
- Instalar los paquetes de un repositorio en local
- Generar documentación a partir del código fuente
- Gestionar las distintas fases del ciclo de vida (build, validacion, generacion del código fuente, procesamiento, compilacion, testing)

### Principales objetivos
- Permitir que un desarrollador comprenda el estado completo de un producto en el menor tiempo posible.
- Reducir la complejidad del proceso de construcción.
- Fomentar las mejores prácticas de desarrollo.

## Comparación entre Gradle, Ant y Maven
Aunque Maven revolucionó la gestión de proyectos en Java, otras herramientas como Gradle y Ant ofrecen alternativas según las necesidades específicas:

### Maven vs Ant
- Maven: Enfoque declarativo con POM, lo que facilita la configuración y estandarización de proyectos.
Gestión automática de dependencias mediante repositorios locales, centrales y remotos.
Casos de uso óptimos: proyectos Java empresariales que buscan consistencia, mantenimiento a largo plazo y compatibilidad con prácticas modernas de CI/CD.

- Ant: Proporciona un enfoque imperativo basado en scripts XML, donde el desarrollador define explícitamente las tareas y su orden de ejecución.
Es extremadamente flexible, pero esta flexibilidad a menudo implica complejidad, ya que carece de un sistema integrado de gestión de dependencias.
Casos de uso óptimos: proyectos con requisitos altamente personalizados o sistemas heredados que ya dependen de scripts Ant.

### Maven vs Gradle
- Maven: Más rígido y menos flexible que Gradle, pero esta rigidez garantiza estructuras consistentes.
Amplia documentación y una comunidad madura, lo que lo hace ideal para equipos que prefieren convenciones en lugar de configuraciones.

- Gradle: Combina lo mejor de ambos mundos (imperativo y declarativo) con scripts basados en Groovy o Kotlin.
Ofrece un rendimiento superior gracias a la construcción incremental y el almacenamiento en caché de tareas.
Soporte avanzado para proyectos multilingües y multiplataforma.
Casos de uso óptimos: proyectos grandes y modernos con requisitos de rendimiento y flexibilidad, como aplicaciones móviles en Android o entornos poliglota.

# Instalación
## Instalación simple
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

## Instalación avanzada 
### Mediante gestora de paquetes
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

### En entornos de docker
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

### Configuración de múltiples versiones Maven (versiones paralelas)
En equipos que trabajan con múltiples proyectos, puede ser necesario manejar varias versiones de Maven simultáneamente.
- Instalación manual de versiones paralelas:
Descargar versiones específicas desde el sitio oficial: https://maven.apache.org/download.cgi.
Descomprimir en directorios separados:
```bash
mkdir -p ~/tools/maven
tar -xzvf apache-maven-3.6.3-bin.tar.gz -C ~/tools/maven/
tar -xzvf apache-maven-3.8.6-bin.tar.gz -C ~/tools/maven/
```
Configuración de M2_HOME y PATH:
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

# Arquitectura y Ciclo de vida
## Arquitectura
La arquitectura de Maven se fundamenta en componentes clave que garantizan la gestión integral de proyectos:
- Modelo POM (Project Object Model): El archivo POM (pom.xml) es el nodo central de configuración en Maven. Contiene metadatos esenciales del proyecto, dependencias, configuraciones de plugins y definiciones específicas para la ejecución del ciclo de vida.
- Repositorios: Maven utiliza repositorios para gestionar artefactos y dependencias.
- Ciclo de Vida del Build: El proceso de construcción en Maven se organiza en fases, agrupadas en ciclos de vida estandarizados que permiten ejecutar tareas secuenciales.
- Sistema de Plugins: Los plugins son el motor funcional de Maven. Permiten ejecutar tareas como compilación, pruebas, empaquetado y generación de reportes, entre otras.
- Convenciones Predeterminadas: Maven minimiza configuraciones manuales mediante convenciones como la estructura estándar de proyectos y la resolución automática de dependencias transitivas.
- Carpeta target
  
## Ciclo de vida
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
- Deploy: Esta fase cuesta mucho entenderla a los desarrolladores ya que ejecutar un Maven Deploy muchas veces en un entorno meramente local no se realiza. Sin embargo, es una fase clave cuando disponemos de una serie de artefactos que deseamos compartir entre desarrollos ya que permite desplegar el artefacto en un servidor remoto de tal forma que otros desarrolladores puedan utilizarlo.

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

# Archivo POM
El archivo POM (pom.xml) es el nodo central de configuración en Maven. Contiene metadatos esenciales del proyecto, como el identificador del proyecto, la versión, el empaquetado y las dependencias.
Esta compuesto por las siguientes partes:
- modelVersion: Indica la versión del esquema del modelo POM que se está utilizando. Actualmente, la versión estándar es 4.0.0.
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

## dependencyManagement
El uso de <dependencyManagement> centraliza las versiones de las dependencias, evitando conflictos en proyectos multi-módulo. Por ejemplo, la versión de commons-lang3 se aplica uniformemente a todos los módulos que la utilicen.
- Gestión de versiones centralizada:
  - Sincronización de versiones: Si tienes múltiples módulos en un proyecto y varios de ellos utilizan una misma biblioteca, dependencyManagement asegura que todos los módulos usen la misma versión de esa biblioteca, lo cual es clave para evitar problemas de compatibilidad y mantener la consistencia.
  - Herencia y dependencias transitivas: Maven resuelve las dependencias transitivas (dependencias de dependencias) y las versiones de estas pueden ser gestionadas de forma centralizada en un único bloque de dependencyManagement, sin necesidad de especificar la versión en cada módulo que las declare.
- Declaración sin resolución inmediata:
  - Al declarar una dependencia dentro de dependencyManagement, Maven no la incluirá automáticamente en el proyecto. Esto es útil cuando quieres asegurarte de que una dependencia esté disponible para los módulos del proyecto sin que afecte al comportamiento de la compilación de inmediato.
  - La verdadera resolución de la dependencia (es decir, agregarla al classpath) ocurre cuando un módulo individual del proyecto tiene una referencia explícita a esa dependencia. Esto hace posible que una dependencia centralizada sea compartida entre todos los módulos sin repetirse.
- Herencia y propagación:
  - Los proyectos de Maven permiten la herencia de configuraciones. Si tienes una estructura de varios módulos (proyecto principal y módulos hijos), puedes definir las versiones de las dependencias en el dependencyManagement del proyecto principal y estos se propagarán a los módulos hijos. Así, cada módulo heredará las mismas versiones de las dependencias sin tener que declararlas explícitamente en cada uno.
  - Evitar conflictos de versiones (Version Conflict Management)

## Propiedades del POM
Las propiedades en el POM permiten flexibilidad al habilitar la parametrización en tiempo de ejecución. Algunos tipos de propiedades incluyen:
- Variables de entorno: Prefijadas con env, permiten acceder a variables del sistema operativo.
- Variables estándar del POM: Utilizan el prefijo project para acceder a valores como la versión o el artefacto.
- Variables de configuración: Relacionadas con ajustes del entorno de Maven, prefijadas con settings.
- Propiedades personalizadas: Especificadas dentro de <properties> en el POM.

## Uso de Import para gestión dependencias a través del BOM (Bill of Materials)
Es un enfoque particularmente importante en el contexto de la gestión de proyectos y dependencias en lenguajes de programación como Java o Kotlin, especialmente en proyectos que utilizan Maven o Gradle como herramientas de construcción (build tools). El BOM, en este contexto, es una lista que describe las dependencias que un proyecto necesita para funcionar correctamente, y se utiliza para centralizar y gestionar las versiones de estas dependencias de manera eficiente.

Consiste en declarar el BOM dentro del archivo de configuración de tu proyecto, como pom.xml (para Maven) o build.gradle (para Gradle). Esta declaración permite que el proyecto "importe" un conjunto de versiones específicas de las bibliotecas sin tener que especificarlas individualmente en cada dependencia.
En Maven, se puede importar un BOM utilizando el elemento <dependencyManagement> y la directiva <dependency> dentro de él.
```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-dependencies</artifactId>
            <version>2.5.0</version>
            <scope>import</scope>
            <type>pom</type>
        </dependency>
    </dependencies>
</dependencyManagement>
```

# Plugins Esenciales y avanzados
Los plugins de Maven son herramientas que permiten ejecutar tareas específicas durante el ciclo de vida de Maven. Cada plugin tiene un conjunto de objetivos que realizan tareas como compilar código, ejecutar pruebas, empaquetar archivos, entre otras. Aquí te explico cómo configurar algunos de los plugins más comunes de Maven de manera avanzada.

## maven-clean
La principal función es eliminar el contenido de la carpeta target, gracias a que activa el ciclo de vida clean que lo compone el goal clean

## maven-compiler-plugin: Ajuste de compiladores personalizados
maven-compiler-plugin: Ajuste de compiladores personalizados (como Lombok o AspectJ)
Este plugin se utiliza para compilar el código fuente de un proyecto. Si bien el comportamiento predeterminado de Maven es utilizar el compilador estándar de Java, es posible configurar el plugin para usar compiladores personalizados, como Lombok o AspectJ, que permiten añadir características adicionales al código en tiempo de compilación.
```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.8.1</version>
            <configuration>
                <source>1.8</source>
                <target>1.8</target>
                <compilerArgument>-Xlint:all</compilerArgument> <!-- Para usar las advertencias del compilador -->
                <annotationProcessorPaths>
                    <annotationProcessorPath>
                        <groupId>org.projectlombok</groupId>
                        <artifactId>lombok</artifactId>
                        <version>1.18.20</version>
                    </annotationProcessorPath>
                </annotationProcessorPaths>
            </configuration>
        </plugin>
    </plugins>
</build>
```
## maven-surefire-plugin y maven-failsafe-plugin: Ejecución de pruebas unitarias e integración
- maven-surefire-plugin: Se utiliza para ejecutar pruebas unitarias dentro del ciclo de vida de Maven, normalmente en la fase test. Este plugin puede ejecutarse para pruebas de unidad utilizando frameworks como JUnit o TestNG.
- maven-failsafe-plugin: Similar al surefire-plugin, pero se usa para ejecutar pruebas de integración, que son aquellas que involucran el sistema completo y no solo componentes aislados.

La diferencia principal es que Surefire es para pruebas unitarias y Failsafe se usa para pruebas que dependen de una infraestructura más compleja (por ejemplo, servicios en red, bases de datos).

```xml
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-surefire-plugin</artifactId>
      <version>2.22.2</version>
      <configuration>
        <includes>
          <include>**/Test*.java</include>
        </includes>
      </configuration>
    </plugin>

    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-failsafe-plugin</artifactId>
      <version>2.22.2</version>
      <configuration>
        <includes>
          <include>**/IT*.java</include>
        </includes>
      </configuration>
    </plugin>
  </plugins>
</build>
```
## maven-shade-plugin: Empaquetado de JARs con dependencias
Este plugin permite crear un archivo JAR que contiene tanto el código del proyecto como todas las dependencias necesarias para ejecutar el programa. Esto es útil cuando se quiere distribuir una aplicación como un archivo JAR autónomo.

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>3.2.1</version>
            <executions>
                <execution>
                    <phase>package</phase> <!-- Ejecutar en la fase 'package' -->
                    <goals>
                        <goal>shade</goal>
                    </goals>
                </execution>
            </executions>
            <configuration>
                <createDependencyReducedPom>false</createDependencyReducedPom> <!-- No generar un POM reducido -->
                <filters>
                    <filter>
                        <artifact>*:*</artifact>
                        <includes>
                            <include>**/*.class</include>
                        </includes>
                    </filter>
                </filters>
            </configuration>
        </plugin>
    </plugins>
</build>
```

## maven-dependency-plugin: Manejo avanzado de dependencias
permite gestionar dependencias de manera avanzada, como copiar dependencias a un directorio específico, analizar dependencias, y verificar si todas las dependencias están disponibles.

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-dependency-plugin</artifactId>
            <version>3.1.2</version>
            <executions>
                <execution>
                    <phase>prepare-package</phase>
                    <goals>
                        <goal>copy-dependencies</goal>
                    </goals>
                    <configuration>
                        <outputDirectory>${project.build.directory}/lib</outputDirectory>
                    </configuration>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

## maven-resource-plugin
Es utilizado para copiar los recursos del proyecto en el directorio de salida, los recursos pueden ser para ejecución del programa o para testing. Al usar este plugin se lanza el ciclo de vida default con los goals resource. Mueve/copia los recursos a la carpeta target.
Para ejecutar este plugin lo podemos hacer usando mvn process-resources o mvn resources:resources o cualquier fase que invoque de manera automática a este plugin.
Para los recursos de test sucede lo mismo se lanza de manera automática, usando el comando mvn resources:testResources

## maven-jacoo
Se encarga de revisar si tu código cumple los estándares de calidad

## sonar-maven-plugin
El sonar-maven-plugin permite integrar SonarQube, una herramienta de análisis estático de código, en el proceso de construcción de Maven. SonarQube analiza el código para detectar problemas de calidad, vulnerabilidades de seguridad, y seguir las métricas del código.

```xml
<build>
  <plugins>
    <plugin>
      <groupId>org.codehaus.mojo</groupId>
      <artifactId>sonar-maven-plugin</artifactId>
      <version>3.9.0.1228</version>
      <executions>
        <execution>
          <goals>
            <goal>sonar</goal>
          </goals>
        </execution>
      </executions>
    </plugin>
  </plugins>
</build>
```

# Multi-Module Projects
Un proyecto multi-módulo es un enfoque de desarrollo de software en el cual una única aplicación o sistema está dividido en múltiples módulos que se gestionan por separado, pero que están estrechamente relacionados entre sí. Cada módulo representa una parte específica de la funcionalidad o de la lógica de negocio de la aplicación, y todos los módulos juntos conforman el producto final. Este enfoque es común en proyectos de gran escala, ya que facilita la modularización, la reutilización del código y una mejor organización.
Estos módulos pueden ser compilados, probados y desplegados de forma independiente, lo que ofrece varias ventajas:

## Beneficios de los proyectos multi-módulo
- Modularidad: Cada módulo puede desarrollarse, probarse y mantenerse de forma independiente, lo que facilita el trabajo en equipo y reduce la complejidad.
- Escalabilidad: Los módulos pueden ser escalados y actualizados independientemente, lo que es útil para proyectos que evolucionan con el tiempo.
- Reutilización de código: Los módulos pueden reutilizarse en otros proyectos o en otras partes del mismo proyecto.
- Gestión de dependencias: Los módulos pueden especificar sus propias dependencias, lo que facilita la actualización de librerías o la integración de nuevos módulos sin afectar al proyecto en su totalidad.

## Diseño, organización y estrategia de proyectos multi-módulo
El diseño de un proyecto multi-módulo debe ser cuidadosamente estructurado para garantizar que todos los módulos sean fáciles de gestionar y mantener
La estructura típica de un proyecto multi-módulo incluye:
- Módulo principal: Este es el módulo que contiene la configuración central y gestiona la ejecución del sistema.
- Módulos de funcionalidad: Son módulos independientes que implementan características específicas del sistema.
- Módulo de utilidades: Puede contener funciones o herramientas comunes que se utilizan a través de diferentes módulos.
- Módulo de pruebas: A menudo se separa en un módulo independiente que contiene las pruebas unitarias y de integración para cada módulo del proyecto.

Estrategias de diseño:
- Separación de preocupaciones: Es recomendable que cada módulo tenga una responsabilidad clara y bien definida.
- Dependencias bien definidas: Asegurarse de que los módulos no dependan innecesariamente de otros módulos. Mantener las dependencias al mínimo ayudará a reducir el acoplamiento.
- Documentación: Cada módulo debe tener una documentación clara sobre su propósito, las interfaces que ofrece y sus dependencias externas.

## Estrategias para empaquetado y despliegue de módulos relacionados
El empaquetado y despliegue de un proyecto multi-módulo es crucial para asegurar que los módulos se desplieguen de manera correcta y eficiente. Existen varias estrategias para gestionar el empaquetado y el despliegue:

Estrategias comunes:
- Empaquetado individual de módulos: Cada módulo se empaqueta de manera independiente y se despliega por separado. Esto permite actualizaciones y despliegues más ágiles. Sin embargo, este enfoque puede requerir que los módulos dependientes se gestionen adecuadamente para garantizar que el sistema final funcione correctamente.
- Empaquetado como un solo artefacto: Algunos proyectos eligen empaquetar todos los módulos juntos en un único archivo o artefacto (como un archivo WAR, JAR, o EAR en Java), lo que facilita el despliegue, pero puede hacer que el sistema sea menos flexible y más difícil de mantener.
- Versionado de módulos: Los módulos deben tener un sistema de versionado claro para evitar problemas de compatibilidad. Si un módulo cambia, el sistema debe asegurarse de que la nueva versión del módulo no rompa la compatibilidad con los módulos dependientes.

Automatización del despliegue:
- CI/CD: Los pipelines de Integración Continua y Despliegue Continuo (CI/CD) son esenciales en proyectos multi-módulo. Herramientas como Jenkins, GitLab CI o Travis CI pueden automatizar la construcción, prueba y despliegue de los módulos.
- Contenedores: Los contenedores (como Docker) permiten empaquetar los módulos y sus dependencias en entornos aislados, facilitando el despliegue en diferentes entornos sin problemas de configuración.

## Dependencias internas entre módulos y su impacto en el ciclo de vida
En un proyecto multi-módulo, los módulos pueden tener dependencias entre sí. Estas dependencias internas son cruciales para la funcionalidad del sistema y deben ser gestionadas cuidadosamente para evitar problemas en el ciclo de vida del proyecto.

Impacto en el ciclo de vida:
- Desarrollo: Cuando un módulo A depende de un módulo B, cualquier cambio en B puede afectar a A. Esto implica que el ciclo de desarrollo de un módulo está ligado al ciclo de desarrollo de los módulos de los cuales depende. Cambios en la API de un módulo pueden obligar a realizar modificaciones en otros módulos.
- Pruebas: Las dependencias internas entre módulos pueden complicar las pruebas. Es necesario asegurarse de que los módulos dependientes se prueben en conjunto para garantizar la correcta integración de las partes del sistema.
- Despliegue y versiones: Si un módulo se actualiza, los módulos dependientes deben ser compatibles con la nueva versión. Si no se gestionan correctamente las versiones, los módulos pueden ser incompatibles entre sí, lo que podría causar fallos en la ejecución.

Estrategias para manejar dependencias internas:
- Desacoplamiento: Siempre que sea posible, es recomendable reducir las dependencias entre módulos. El uso de interfaces o servicios desacoplados puede mitigar el impacto de cambios en los módulos.
- Control de versiones: Establecer una política clara para el control de versiones de los módulos y sus dependencias, de modo que los módulos dependientes puedan adaptarse fácilmente a nuevas versiones sin romper la funcionalidad.
- Pruebas de integración: Implementar pruebas de integración que aseguren que los módulos interactúan correctamente antes de ser desplegados.

# Gestión de Repositorios
En Maven, un repositorio es un lugar donde se almacenan los artefactos (como JAR, WAR, EAR) generados y 
utilizados en los proyectos. Existen tres tipos principales de repositorios en Maven: local, remoto y central.
Maven utiliza estos repositorios para gestionar las dependencias de un proyecto, y cada tipo tiene un propósito específico.

## Repositorio local
El repositorio local es una carpeta en el sistema de archivos de tu máquina local, que Maven crea cuando ejecutas la primera construcción de un proyecto.
Los artefactos que descargues o instales en tu proyecto, como las dependencias y los artefactos generados, se almacenan en este repositorio. El repositorio local se encuentra en el siguiente directorio:
- En sistemas Unix o Linux: ~/.m2/repository
- En sistemas Windows: C:\Users\<usuario>\.m2\repository
- Ruta configurada ([Modificación de la ruta de Maven (repositorio local o configuración)](#modificación-de-la-ruta-de-maven-repositorio-local-o-configuración))

## Repositorio remoto
Un repositorio remoto es un servidor centralizado donde Maven almacena artefactos compartidos entre los proyectos. Los repositorios remotos más comunes son el repositorio central de Maven y los 
repositorios privados de empresas o proyectos. Cuando Maven no encuentra una dependencia en el repositorio local, buscará en los repositorios remotos. Si la dependencia está disponible, 
Maven la descargará y la almacenará en el repositorio local para su uso futuro.

## Repositorio central
El repositorio central es un repositorio público mantenido por la comunidad de Maven, que contiene millones de artefactos como bibliotecas y frameworks. Este repositorio es accesible para todos los 
desarrolladores y es la fuente principal de dependencias que Maven utiliza. El repositorio central está preconfigurado en Maven, por lo que no necesitas especificarlo en el archivo settings.xml 
a menos que desees modificar la configuración.

## Repositorio de empresa o privado
Las empresas a menudo tienen repositorios privados donde almacenan sus propias bibliotecas internas o versiones personalizadas de bibliotecas comunes.
Estos repositorios pueden estar alojados en servidores locales o en servicios como Nexus, Artifactory o GitHub Packages. Se configuran en el archivo settings.xml o pom.xml de la siguiente manera.

# Perfiles
Los perfiles permiten configurar el proyecto para diferentes entornos. Cada perfil puede contener configuraciones específicas como URLs de bases de datos, variables de entorno y otras propiedades.
Los perfiles se pueden agrupar de la siguiente manera.
- Por proyecto, definidos en el propio POM
- Por usuario, definido en la configuración de Maven (definidos en m.2/settings.xml)
- Global, definido en la configuración global de Maven (conf/settings.xml)
Como dato importante si el perfil definido en el archivo pom esta activo en el fichero de settings.xml prevalecerá la configuración definida en el settings

## Perfiles en POM
Para poder crearlo se realizará dentro de las etiquetas profile con las siguientes propiedades
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
Para poder créalo se realizará dentro de la etiqueta profile con las siguientes propiedades
- id: El identificador único del perfil. Es esencial para activar este perfil de forma explícita desde la línea de comandos o mediante condiciones de activación.
- activation: La sección activation define las condiciones bajo las cuales un perfil se activa automáticamente. Puedes activar un perfil en función de:
  - activeByDefault: Si se establece en true, el perfil se activa por defecto.
  - property: Activa el perfil si una propiedad del sistema tiene un valor específico.
  - jdk: Activa el perfil si una versión de JDK específica está siendo utilizada.
  - os: Activa el perfil dependiendo del sistema operativo (Linux, Windows, etc.).
  - file: Activa el perfil si un archivo o directorio específico existe.
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

# Gestión de dependencias
Las dependencias son librerías o bibliotecas de terceros que necesitamos para que nuestro proyecto pueda ejecutar algunas lógicas de negocio o para realizar pruebas unitarias.
Pero existen casos en las que ciertas dependencias necesitan de otras dependencias, (las denominadas dependencias transitivas), necesitamos importarlas también en nuestro sistema para que funcionen correctamente

Para declara una dependencia en nuestro pom deberemos de incluirlas en el apartado de dependecies y crear una etiqueta dependency en la que poseerá el groupId, el artifactId y la versión y como valor opcional el scope.
- Scope: El scope determina el alcance en el que las dependencias serán utilizadas en el proyecto. Dfine cuando y como esas despendencias estarán disponibles en el proceso de compilación y ejecución.
Los Scope que ofrece Maven son:
  - Compile: Este es el scope por defecto. Las dependencias con este scope están disponibles en todas las fases del proyecto (compilación, prueba, ejecución).
  - Provided: Las dependencias con este scope están disponibles en tiempo de compilación y prueba, pero se espera que estén provistas por el entorno de ejecución, por ejemplo, por el contenedor de servlets en una aplicación web.
  - Runtime: Las dependencias con este scope no son requeridas para la compilación, pero sí para la ejecución. Por lo tanto, estarán presentes en tiempo de ejecución y durante las pruebas, pero no se utilizarán durante la compilación.
  - Test: Este scope solo es relevante durante la ejecución de pruebas, no durante la compilación ni la ejecución del proyecto principal.
  - System: Las dependencias con este scope son similares a las de compile, pero deben ser proporcionadas explícitamente y se utilizan en el entorno de desarrollo. Maven no maneja estas dependencias ni las descarga del repositorio remoto.
  -	Import: Este scope solo se usa en la sección <dependencyManagement>, permitiendo manejar la versión de la dependencia y la exclusión de transitorios en archivos POM separados.

## Análisis avanzado de conflictos de versiones (dependency:tree, dependency:analyze)
Cuando se manejan dependencias en un proyecto, es común que ocurran conflictos de versiones. Estos conflictos surgen cuando diferentes dependencias requieren diferentes versiones de una misma biblioteca, lo que puede generar incompatibilidades.

### dependency:tree
En herramientas como Maven o Gradle, el comando dependency:tree permite visualizar el árbol de dependencias de un proyecto. Este comando muestra todas las dependencias de un proyecto y sus respectivas dependencias transitivas. De esta forma, se puede ver cómo se resuelven las versiones de las dependencias en un sistema jerárquico.
```bash
mvn dependency:tree
```
Esto devuelve una representación en árbol de todas las dependencias y las versiones que se están utilizando. Si se presentan varios conflictos de versiones, pueden identificarse rápidamente.

### dependency:analyze
Es útil para detectar dependencias que están en el proyecto pero que no se utilizan (dependencias no referenciadas), así como dependencias que son necesarias pero que no están declaradas (dependencias faltantes). En Maven, esto es útil para limpiar el proyecto y asegurar que todas las dependencias necesarias estén declaradas correctamente.
```bash
mvn dependency:analyze
```

## Dependencias opcionales y excluidas
En muchas ocasiones, no todas las dependencias que un proyecto utiliza son estrictamente necesarias para todas las configuraciones posibles. Aquí entran en juego las dependencias opcionales y excluidas.

### Dependencias Opcionales
Son aquellas que no son esenciales para la ejecución del proyecto, pero que pueden ser útiles en ciertos casos. Se definen en el archivo de configuración de dependencias (como pom.xml en Maven) y pueden ser utilizadas por los desarrolladores si lo desean, pero no afectan al proyecto si no se incluyen.
```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>some-library</artifactId>
    <version>1.0.0</version>
    <optional>true</optional>
</dependency>
```

### Dependencias Excluidas
Las dependencias excluidas son aquellas que están incluidas transitivamente a través de otras dependencias pero que no se quieren utilizar en el proyecto. Excluir dependencias puede ser útil cuando se quiere evitar conflictos de versiones o incluir una versión específica de una dependencia que sobrescribe la transitiva.
```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>parent-library</artifactId>
    <version>2.0.0</version>
    <exclusions>
        <exclusion>
            <groupId>com.unwanted</groupId>
            <artifactId>unwanted-library</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

## Estrategias de versionado semántico en dependencias
El versionado semántico (SemVer) es una estrategia para definir la versión de las dependencias de forma clara y coherente, ayudando a los desarrolladores a entender los cambios que podrían afectar el comportamiento del software.

Las versiones semánticas siguen el formato: MAJOR.MINOR.PATCH
- MAJOR: Se incrementa cuando se realizan cambios incompatibles en la API.
- MINOR: Se incrementa cuando se añaden funcionalidades de manera compatible hacia atrás.
- PATCH: Se incrementa cuando se corrigen errores de manera compatible hacia atrás.

Ejemplo de uso de versiones semánticas:
- Una actualización MAJOR podría significar que la biblioteca ha cambiado significativamente y algunas funcionalidades podrían no funcionar como antes.
- Una actualización MINOR podría agregar nuevas funcionalidades sin romper la compatibilidad con versiones anteriores.
- Una actualización PATCH debería ser solo correcciones de errores sin modificar la funcionalidad.
Para mantener un control adecuado de las versiones en las dependencias, es importante seguir las reglas del versionado semántico. El uso adecuado de las versiones ayuda a reducir el riesgo de introducir incompatibilidades entre las dependencias.

# Carpeta target
La carpeta target es un directorio comúnmente utilizado en proyectos de programación, especialmente en aquellos que emplean herramientas de construcción como Maven, Gradle, o entornos de desarrollo como Spring Boot en Java, entre otros. Este directorio es generado automáticamente durante el proceso de construcción (compilación) del proyecto y tiene un propósito fundamental en cuanto a la organización y almacenamiento de los artefactos generados durante dicho proceso.
tiene la siguiente estructura
```perl
target/
    ├── classes/          # Archivos de clases compiladas (.class)
    ├── test-classes/     # Clases de pruebas compiladas
    ├── my-project-1.0-SNAPSHOT.jar  # Artefacto final empaquetado
    ├── maven-status/     # Estado de la construcción (Maven)
    ├── generated-sources/ # Archivos generados automáticamente
    └── logs/             # Archivos de log generados durante la construcción
```

# Configuración de settings.xml
Una de las características clave de Maven es su capacidad para gestionar dependencias y almacenar artefactos en un repositorio local. 
De forma predeterminada, Maven utiliza una ubicación específica en tu sistema para almacenar estas dependencias y configuraciones. Sin embargo, en ocasiones, 
puede ser necesario modificar esta ubicación para adaptarse a las necesidades de un entorno de desarrollo específico, ya sea por razones de rendimiento, espacio en disco, o preferencias organizativas.

Las propiedades que puedes modificar son las siguientes
- LocalRepository: Indica el path donde se almacenarán todos los repositorios y librerías que necesita nuestros proyectos para funcionar
- Offline: Indica si Maven debe de operar en modo fuera de línea, lo que permitirá si debe descargar actualizaciones o dependencias si no están disponibles
- Proxies: Se emplea para indicar la información de los servidores proxy
- Mirror: Se emplea para descarga dependencias de un repositorio espejo, esto quiere decir que evita descargar dependencias del repositorio central de Maven y lo obtiene desde otro como puede ser nexus.
- Repositories: Permite configurar los tipos de repositorios relases o snapshots
- PluginRepositories: Almacena bibliotecas de complementos y archivos asociados
- Server: Es empelado para almacenar usuarios, contraseñas, llaves privadas, etc

## Tipos de configuración
En Maven, la configuración global y local se refiere a las diferentes ubicaciones donde puedes configurar los parámetros y propiedades que afectarán a tu proyecto. Maven tiene dos tipos principales de configuración:

- Configuración global: Se encuentra en el archivo settings.xml global de Maven. Este archivo se encuentra en la carpeta conf del directorio de instalación de Maven (por ejemplo, C:\Program Files\Apache\Maven\conf\settings.xml en Windows) y afecta a todos los proyectos en la máquina.
- Configuración local: Esta se encuentra en el archivo settings.xml ubicado en el directorio .m2 de tu usuario (por ejemplo, C:\Users\<tu_usuario>\.m2\settings.xml en Windows) y es específico para ese usuario, pudiendo sobrescribir la configuración global.

### Combinación de configuraciones globales y locales
Configuración global: Si una propiedad no está definida en la configuración local, Maven la tomará de la configuración global.
Configuración local: Si una propiedad está definida tanto en la configuración global como en la local, la configuración local tiene prioridad.

### Uso de perfiles
Puedes definir perfiles tanto a nivel global como local. Los perfiles te permiten configurar diferentes comportamientos según el entorno.
- Perfil global: Se puede activar usando el comando mvn -P <nombre_del_perfil>.
- Perfil local: Se configura en el archivo local settings.xml, y se activa automáticamente si está configurado como predeterminado.

## Ubicación predeterminada 
La carpeta de Maven contiene los archivos que Maven usa para gestionar las dependencias y la configuración. Por defecto, estas son las ubicaciones en distintos sistemas operativos:
- En sistemas operativos basados en UNIX (Linux/macOS):
    - Repositorio local: El repositorio local, donde Maven almacena las dependencias, se encuentra en: ```~/.m2/repository```
    - Archivo de configuración: El archivo de configuración settings.xml está en:```~/.m2/settings.xml```
- En sistemas operativos Windows:
    - Repositorio local: La ubicación predeterminada del repositorio local es: ```C:\Users\<nombre_de_usuario>\.m2\repository```
    - Archivo de configuración: El archivo settings.xml se encuentra en: ```C:\Users\<nombre_de_usuario>\.m2\settings.xml```

## Modificación de la ruta de Maven (repositorio local o configuración)
Para ello deberemos de buscar primero la carpeta .m2 y crear en ella el fichero settings.xml en el definiremos el path donde querremos que se almacenen los artefactos para los proyectos.
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

## Ejecutar Maven desde un proxy
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

## Modificar repositorio central 
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

# Documentación y Reportes
Los informes y la documentación generada por Maven tienen varios propósitos importantes en el desarrollo de software, para poder generarlo usaremos el plugin mvn site:
- Comunicación y comprensión del proyecto:
  - Documentación del código fuente: Maven puede generar documentación automáticamente a partir del código fuente, como Javadoc para proyectos Java. Esta documentación proporciona una guía clara sobre cómo utilizar las clases y métodos del código.
  - Informes de dependencias: Los informes de dependencias, como el árbol de dependencias, ayudan a entender la estructura del proyecto, las relaciones entre las distintas partes y las dependencias transitivas.
- Mantenimiento y gestión del proyecto:
  - Control de versiones y auditoría: Los informes generados pueden facilitar la gestión de versiones, permitiendo identificar fácilmente qué versiones de las dependencias están siendo utilizadas en el proyecto y si existen posibles conflictos.
  - Detección de dependencias obsoletas o no utilizadas: Los informes pueden ayudar a identificar dependencias que ya no se usan o que han quedado obsoletas, permitiendo su eliminación para reducir la complejidad del proyecto.
- Automatización de tareas y revisión de calidad:
  - Análisis estático del código: Algunos informes pueden incluir análisis estático del código, como la detección de errores o el cumplimiento de estándares de codificación.
  - Cobertura de pruebas: Maven puede generar informes sobre la cobertura de pruebas, indicando qué partes del código están siendo probadas y en qué medida. Esto es crucial para evaluar la calidad del código y las áreas que necesitan más pruebas.
- Facilitar la integración y entrega continua
  - Documentación para desarrolladores y usuarios: La documentación generada puede servir como una guía para desarrolladores que se unen al proyecto o para usuarios que necesitan comprender cómo utilizar una API o aplicación.
  - Informes de construcción: En un entorno de integración continua, los informes generados por Maven proporcionan información detallada sobre el proceso de construcción, errores, pruebas y otros aspectos relevantes para el equipo de desarrollo.

## JavaDoc
Maven no solo genera informes sobre la estructura del proyecto, sino que también puede generar el JavaDoc correspondiente al código fuente. Para ello, se debe configurar el plugin javadoc como un reporte en el archivo pom.xml. Luego, para ejecutar el proceso y generar la documentación, se utiliza el siguiente comando:
```bash
mvn site
mvn javadoc:javadoc
```

## Informes de Cobertura de Pruebas
Para generar informes de cobertura de pruebas, se puede integrar el plugin JaCoCo en el pom.xml. Este plugin analiza la cobertura de pruebas en el código, proporcionando métricas detalladas sobre qué tan exhaustivas son las pruebas. 
```xml
<plugin>
  <groupId>org.jacoco</groupId>
  <artifactId>jacoco-maven-plugin</artifactId>
  <version>0.8.7</version>
  <executions>
    <execution>
      <goals>
        <goal>prepare-agent</goal>
        <goal>report</goal>
      </goals>
    </execution>
  </executions>
</plugin>
```

## Informes personalizados
Una de las mayores ventajas de Maven es la capacidad de personalizar los informes generados para adaptarlos a las necesidades del proyecto. Utilizando el Maven Site Plugin, es posible configurar las opciones de informes dentro del pom.xml para generar un sitio web de documentación más completo o personalizado.
Esto es útil si se requiere incluir informes adicionales como análisis de seguridad, métricas de rendimiento, o cualquier otro informe que no esté cubierto por los informes predeterminados de Maven. Los desarrolladores pueden definir qué informes se incluyen en el sitio web, organizar los informes y aplicar configuraciones predeterminadas para hacer más eficiente la generación de la documentación.

## Publicar documentación de mi sitio
Para publicar la documentación generada por Maven en un servidor web, se debe configurar el parámetro distributionManagement dentro del pom.xml y agregar la configuración del servidor en el archivo settings.xml. Después de configurar correctamente la distribución, el siguiente comando se utiliza para desplegar la documentación en el servidor
Si se desea comprobar la apariencia de la documentación antes de su despliegue final, se puede utilizar el siguiente comando, que ejecuta un servidor local con Jetty y muestra cómo quedará el sitio

```bash
mvn site-deploy
mvn site:run
```
## FindBugs/PMD
### FindBugs en Maven
FindBugs es una herramienta de análisis estático que busca errores potenciales en el código Java. Los errores que detecta incluyen bugs comunes, como el uso incorrecto de los objetos, referencias nulas, posibles errores de concurrencia y otros problemas que pueden ser difíciles de identificar durante las pruebas. FindBugs clasifica los errores según su gravedad, ayudando a los desarrolladores a priorizar los problemas a resolver.

Para integrar FindBugs en un proyecto Maven y generar los informes correspondientes, debes seguir estos pasos:
- Configuración del Plugin FindBugs
Para habilitar FindBugs en Maven, primero debes agregar el plugin findbugs-maven-plugin al archivo pom.xml de tu proyecto
```xml
<build>
  <plugins>
    <plugin>
      <groupId>org.codehaus.mojo</groupId>
      <artifactId>findbugs-maven-plugin</artifactId>
      <version>3.0.5</version>
      <executions>
        <execution>
          <goals>
            <goal>findbugs</goal>
            <goal>html</goal> <!-- Para generar un reporte en formato HTML -->
          </goals>
        </execution>
      </executions>
    </plugin>
  </plugins>
</build>
```

Para generar el informe de FindBugs, ejecuta el siguiente comando:
```bash
mvn site
```

### PMD
PMD es otra herramienta de análisis estático que ayuda a identificar posibles problemas en el código, como violaciones de buenas prácticas, código redundante, violaciones de estilo y otros problemas de calidad. A diferencia de FindBugs, que se centra más en bugs potenciales, PMD se enfoca en la legibilidad y el mantenimiento del código, identificando patrones de diseño inadecuados o código innecesario.

Configuración del Plugin PMD
Para integrar PMD en un proyecto Maven y generar los informes correspondientes, debes agregar el plugin pmd-maven-plugin al archivo pom.xml del proyecto.
```xml
<build>
  <plugins>
    <plugin>
      <groupId>org.codehaus.mojo</groupId>
      <artifactId>pmd-maven-plugin</artifactId>
      <version>3.13.0</version>
      <executions>
        <execution>
          <goals>
            <goal>pmd</goal> <!-- Análisis de código -->
            <goal>cpd</goal> <!-- Detección de duplicados de código -->
          </goals>
        </execution>
      </executions>
    </plugin>
  </plugins>
</build>
```
Para generar el informe de PMD, ejecuta el siguiente comando:
```bash
mvn site
```

### Integración de FindBugs y PMD en un Solo Reporte
Es posible combinar los informes de FindBugs y PMD en un solo sitio web de Maven, lo que te permite ver toda la información relevante sobre la calidad del código en un solo lugar. Esto se logra configurando ambos plugins dentro del pom.xml y ejecutando el comando mvn site.

Configuración Combinada:
```xml
<build>
  <plugins>
    <!-- Plugin FindBugs -->
    <plugin>
      <groupId>org.codehaus.mojo</groupId>
      <artifactId>findbugs-maven-plugin</artifactId>
      <version>3.0.5</version>
      <executions>
        <execution>
          <goals>
            <goal>findbugs</goal>
            <goal>html</goal>
          </goals>
        </execution>
      </executions>
    </plugin>

    <!-- Plugin PMD -->
    <plugin>
      <groupId>org.codehaus.mojo</groupId>
      <artifactId>pmd-maven-plugin</artifactId>
      <version>3.13.0</version>
      <executions>
        <execution>
          <goals>
            <goal>pmd</goal>
            <goal>cpd</goal>
          </goals>
        </execution>
      </executions>
    </plugin>
  </plugins>
</build>
```

```bash
mvn site
```

# Diagnóstico y Resolución de Problemas en Maven
Cuando trabajamos con Maven, es común encontrarse con problemas que afectan el proceso de construcción y ejecución de proyectos. Estos problemas pueden ser causados por una serie de factores, como dependencias corruptas, configuraciones incorrectas o plugins mal configurados.

## Estrategias depuracion
### Uso de -X (modo debug)
El modo de depuración (-X) es una herramienta muy útil para obtener información detallada sobre el proceso de construcción de Maven. Al ejecutar Maven con esta opción, se activan mensajes de depuración adicionales que pueden ayudar a identificar problemas profundos en la resolución de dependencias, ejecución de plugins, y otros pasos dentro del ciclo de vida de Maven.
```bash
mvn clean install -X
```
Este comando generará una salida detallada con la información sobre cada paso de la construcción, incluyendo detalles de cada plugin ejecutado, cada archivo descargado, y cualquier problema encontrado durante el proceso.
Lo que proporciona el modo debug:
Información detallada de la configuración de Maven: Incluye detalles sobre el pom.xml, perfiles activos, variables de entorno y más.
Detección de conflictos de dependencias: Puede ayudarte a identificar qué versiones de dependencias están siendo resueltas y si hay algún conflicto.
Detalles sobre plugins: Muestra información acerca de qué plugins se están ejecutando y con qué parámetros.

### Análisis de logs generados por Maven
Maven genera logs detallados que pueden contener información vital sobre el ciclo de vida de la construcción, advertencias o errores. Además del modo debug (-X), Maven también permite la configuración de los niveles de log a través de la opción -l para guardar la salida en un archivo específico.
```bash
mvn clean install -l maven-log.txt
```
Al revisar el archivo de log, podemos observar:
Errores de compilación: Cualquier error en la compilación de los módulos.
Problemas de dependencias: Si Maven no puede encontrar o resolver una dependencia, esto se registrará en el log.
Fallos de plugins: Si algún plugin falla en su ejecución, se detallará el error y el stack trace en el log.
Es importante buscar mensajes clave, como "Could not find" (para dependencias faltantes), "Plugin execution not covered by lifecycle" (para problemas con la configuración de plugins) o cualquier "Exception" que indique un fallo en el proceso.

## Resolución de Dependencias Faltantes o Corruptas
Uno de los problemas más comunes al usar Maven es la falta de dependencias o dependencias corruptas en el repositorio local (~/.m2/repository). Estos problemas pueden ocurrir por varias razones:

Dependencias no encontradas en los repositorios remotos.
Archivos corruptos descargados de un repositorio remoto.
Pasos para resolver dependencias faltantes o corruptas:

Eliminar el caché local de Maven: Si una dependencia se ha descargado de manera incorrecta o está corrupta, puedes eliminarla de tu repositorio local para forzar a Maven a descargarla de nuevo.
```bash
rm -rf ~/.m2/repository/<group-id>/<artifact-id>/<version>
```
Limpiar el repositorio local: También puedes limpiar todo el repositorio local, lo que eliminará todas las dependencias almacenadas en caché, y obligará a Maven a descargar nuevamente todas las dependencias:
```bash
mvn dependency:purge-local-repository
```
Forzar una actualización: Si las dependencias no se actualizan automáticamente, puedes forzar que Maven descargue las versiones más recientes con el comando:
```bash
mvn clean install -U
```
La opción -U obliga a Maven a actualizar las dependencias incluso si ya existen en el repositorio local.

# Fichero mvnw (mvnw.cmd)
tiene una utilidad clave relacionada con la automatización de la construcción del proyecto sin necesidad de tener Maven instalado globalmente en el sistema. Este fichero es parte de un mecanismo llamado Maven Wrapper, que facilita la gestión de las versiones de Maven en un proyecto y asegura que el entorno de construcción sea consistente para todos los desarrolladores del equipo, sin importar la versión de Maven que cada uno tenga instalada.

## Cómo Funciona el Maven Wrapper
Cuando un desarrollador ejecuta el script mvnw (en sistemas Unix o macOS) o mvnw.cmd (en Windows), el wrapper realiza las siguientes acciones:
- Verifica si Maven está instalado: Si Maven no está instalado en el sistema, el Maven Wrapper descarga automáticamente la versión de Maven especificada en el archivo maven-wrapper.properties.
- Descarga la versión de Maven: Si Maven no está disponible o si la versión requerida no está presente, el wrapper descarga la versión de Maven especificada y la utiliza para ejecutar las tareas necesarias (como compilar el proyecto, ejecutar pruebas, etc.).
- Ejecuta el comando Maven: Después de descargar Maven (si es necesario), el wrapper ejecuta el comando Maven correspondiente en el proyecto, como si fuera un script normal de Maven (mvn).
Esto asegura que todos los miembros del equipo de desarrollo usen la misma versión de Maven, incluso si tienen diferentes versiones instaladas en sus máquinas locales.

# Comandos maven
- mvn clean: Elimina los archivos generados en el ciclo de vida anterior (como los archivos compilados o empaquetados). Este comando es útil para asegurarse de que la próxima compilación sea completamente nueva, sin artefactos de compilaciones anteriores
- mvn compile: Compila el código fuente del proyecto en el directorio src/main/java y lo coloca en el directorio target/classes
- mvn test:Ejecuta las pruebas unitarias del proyecto utilizando un framework como JUnit. Se realiza sobre el código fuente que está en src/test/java
- mvn package: Toma el código compilado y lo empaqueta en un archivo (por ejemplo, JAR, WAR) según la configuración del proyecto en el archivo pom.xml
- mvn install: Instala el paquete (por ejemplo, JAR, WAR) en el repositorio local de Maven (~/.m2/repository). Esto es útil para proyectos que están siendo utilizados como dependencias en otros proyectos
- mvn deploy: Envía el artefacto (como JAR, WAR) al repositorio remoto configurado en el pom.xml. Este paso es comúnmente utilizado cuando se está listando un artefacto para ser utilizado por otros equipos o proyectos
- mvn validate Verifica que la configuración del proyecto sea correcta antes de ejecutar los pasos de construcción. Es útil para asegurarse de que todos los elementos del pom.xml están configurados correctamente.
- mvn sit: Genera el sitio de documentación del proyecto. El sitio incluye información como las dependencias, los informes de cobertura, el historial de cambios y otros detalles configurables.
- mvn clean install: Combina los comandos clean e install. Primero limpia cualquier archivo anterior y luego construye e instala el artefacto en el repositorio local.
- mvn clean package: Limpia los artefactos de construcción anteriores y luego empaqueta el proyecto en un archivo JAR o WAR.
- mvn clean deploy: Limpia los artefactos anteriores y luego envía el paquete construido al repositorio remoto.
- mvn exec:java: Ejecuta una clase Java directamente desde Maven sin necesidad de compilar primero. Es útil para ejecutar aplicaciones Java desde un proyecto Maven sin crear un paquete.
- mvn dependency:tree: Muestra la jerarquía de dependencias del proyecto, es decir, todas las bibliotecas y sus dependencias transitivas.
- mvn dependency:copy-dependencies: Copia todas las dependencias de un proyecto en un directorio específico.
- mvn versions:display-dependency-updates: Muestra las actualizaciones disponibles para las dependencias del proyecto.
- mvn versions:use-latest-versions: Actualiza todas las dependencias del proyecto a sus versiones más recientes.
- mvn help:effective-pom: Muestra la configuración efectiva del pom.xml, incluyendo todos los valores heredados de los POMs superiores y las dependencias transitivas.
- mvn clean verify: Limpia el proyecto y luego realiza la compilación, las pruebas y la verificación de que el proyecto está en buen estado. Utiliza el ciclo de vida de validación para comprobar que el proyecto cumple con todos los requisitos de calidad.
- mvn archetype:generate: Crea un nuevo proyecto Maven a partir de una plantilla ("arquetipo"). Esto es útil cuando quieres empezar un proyecto con una estructura básica predefinida.
- mvn release:prepare: Prepara un proyecto para ser liberado. Este comando realiza varias tareas, como incrementar la versión del proyecto y etiquetar el repositorio.
- mvn release:perform: Realiza el proceso de liberar el proyecto, como subir el artefacto al repositorio de liberación después de preparar la versión.
- mvn deploy:deploy-file: Utiliza Maven para desplegar un archivo específico (no generado en el ciclo de vida de Maven) en un repositorio remoto. Es útil cuando tienes artefactos fuera del ciclo habitual de construcción.
- mvn clean test: Limpia el proyecto y luego ejecuta las pruebas. Es útil para asegurarse de que las pruebas se ejecutan sobre un código limpio.
- mvn compile exec:java: Compila el proyecto y luego ejecuta la clase principal definida en el pom.xml.
- mvn clean verify site Función: Limpia el proyecto, ejecuta las pruebas, verifica que todo esté en orden y luego genera el sitio de documentación del proyecto.
