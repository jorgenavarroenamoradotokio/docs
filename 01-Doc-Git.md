<div align="center">
  <img src="https://raw.githubusercontent.com/jorgenavarroenamoradotokio/docs/main/logo/Git-Logo.svg">
</div>

## Índice
- [Introducción](#introducción)
  - [Características](#características)
  - [Conceptos básicos](#conceptos-básicos)
- [Funcionamiento](#funcionamiento)
- [Ciclo de vida de los archivos en Git](#ciclo-de-vida-de-los-archivos-en-git)
- [Ramas y bifurcaciones de código](#ramas-y-bifurcaciones-de-código)
  - [GitFlow que es y sus comandos](#gitflow-que-es-y-sus-comandos)
- [Fichero .gitignore](#fichero-gitignore)
- [Configuración en Git](#configuración-en-git)
- [Comando de ayuda](#comando-de-ayuda)
- [Comandos básicos](#comandos-básicos)
  - [Git init](#git-init)
  - [Git add](#git-add)
  - [Git status](#git-status)
  - [Git commit](#git-commit)
  - [Git log](#git-log)
- [Comandos básicos para repositorios remotos](#comandos-básicos-para-repositorios-remotos)
  - [Git clone](#git-clone)
  - [Git remote](#git-remote)
  - [Git push](#git-push)
  - [Git pull](#git-pull)
  - [Git fetch](#git-fetch)
- [Comandos de utilidades](#comandos-de-utilidades)
  - [Git Clean](#git-clean)
  - [Git mv](#git-mv)
  - [Git blame](#git-blame)
  - [Git grep](#git-grep)
  - [Git alias](#git-alias)
  - [Git reset](#git-reset)
  - [Git revert](#git-revert)
  - [Git restore](#git-restore)
  - [Git amend](#git-amend)
  - [Git cherry-pick](#git-cherry-pick)
  - [Git rebase](#git-rebase)
  - [Git stash](#git-stash)
    - [Formas de guardar cambios en el stash](#formas-de-guardar-cambios-en-el-stash)
    - [Comandos útiles para gestionar el stash](#comandos-útiles-para-gestionar-el-stash)
  - [Git reflog](#git-reflog)
- [Comandos de Ramas y Merge](#comandos-de-ramas-y-merge)
  - [Git branch](#git-branch)
  - [Git switch](#git-switch)
  - [Git tag](#git-tag)
    - [Creación y gestión de etiquetas](#creación-y-gestión-de-etiquetas)
    - [Tipos de etiquetas](#tipos-de-etiquetas)
  - [Git merge](#git-merge)
    - [Fast-Forward Merge (fusión rápida)](#fast-forward-merge-fusión-rápida)
    - [Merge con Commit de Fusión (Merge Commit / Three-way merge)](#merge-con-commit-de-fusión-merge-commit--three-way-merge)
    - [Merge con Conflictos](#merge-con-conflictos)
    - [Squash Merge (Fusión en un solo commit)](#squash-merge-fusión-en-un-solo-commit)
- [Comandos de comparación](#comandos-de-comparación)
  - [Git show](#git-show)
  - [Git diff](#git-diff)
  - [Git shortlog](#git-shortlog)
  - [Git describe](#git-describe)

# Introducción

Git es un sistema de control de versiones distribuido, creado por Linus Torvalds en 2005. Su objetivo principal es ayudarte a gestionar los cambios en el código fuente de un proyecto, permitiendo trabajar de forma colaborativa y ordenada.

Con Git, varios desarrolladores pueden trabajar en paralelo sin pisarse el trabajo. Cada cambio queda registrado, lo que facilita llevar un historial claro, revertir errores si es necesario y evitar conflictos entre versiones del código.

## Características

* **Distribuido**: A diferencia de otros sistemas de control de versiones, en Git cada desarrollador cuenta con una copia completa del historial del proyecto en su máquina local. Esto permite trabajar sin conexión, compartir cambios sin depender de un servidor central y, al mismo tiempo, usar repositorios remotos para sincronizar el trabajo en equipo.
* **Rastreo de versiones**: Git no guarda simplemente los archivos modificados, sino que registra una instantánea del estado del proyecto en cada confirmación (commit). Esto facilita volver atrás en el tiempo, comparar cambios, y saber quién hizo qué y cuándo.
* **Ramas (branching)**: Git permite crear ramas para desarrollar nuevas funcionalidades, realizar pruebas o corregir errores de forma aislada. Así se evita alterar el código principal (usualmente en la rama main). Una vez completado el trabajo en una rama, esta puede integrarse nuevamente al flujo principal sin perder historial.
* **Integración y resolución de conflictos**: Git permite fusionar los cambios de distintas ramas o colaboradores. Cuando dos personas modifican la misma parte del código, Git detecta el conflicto y ofrece herramientas para resolverlo manualmente, asegurando que el resultado final sea coherente.

## Conceptos básicos

| Concepto      | Descripción                                                                 |
|---------------|-----------------------------------------------------------------------------|
| **Repositorio (repo)** | Contenedor del proyecto que incluye archivos y el historial de cambios.       |
| **Commit**     | Registro de cambios en un momento específico. Incluye mensaje, autor y fecha. |
| **Rama (branch)** | Línea de desarrollo independiente para trabajar sin afectar el código principal. |
| **Fusión (merge)** | Proceso de combinar los cambios de una rama con otra.                        |
| **Push**       | Enviar los commits locales al repositorio remoto.                            |
| **Pull**       | Obtener y fusionar los cambios más recientes del repositorio remoto.         |


# Funcionamiento

El funcionamiento de Git se basa en capturar "versiones" del proyecto cada vez que se realizan y guardan cambios. Esta estrategia permite llevar un seguimiento detallado de cada modificación, regresar a estados anteriores si es necesario y colaborar en equipo manteniendo un historial claro y estructurado del desarrollo.

Cuando haces un commit, Git crea una instantánea del estado actual del proyecto. Esta instantánea actúa como una "foto" del código en ese momento, almacenando la estructura de archivos, su contenido y cualquier modificación realizada. Para optimizar el espacio, Git no guarda copias completas de los archivos en cada versión, sino que registra solo los cambios con respecto a la versión anterior (deltas).

Estas instantáneas se organizan en un historial de cambios, donde cada entrada incluye:

* El autor del cambio
* La fecha y hora
* Un identificador único (hash)
* Un mensaje que describe qué se hizo

Este historial cronológico permite revisar todo el proceso de desarrollo, entender por qué se hicieron ciertos cambios y, si es necesario, volver a versiones anteriores con facilidad.

Modificas archivos → `git add` → `git commit` → Historial de cambios

Commit A ──▶ Commit B ──▶ Commit C ──▶ Commit D
(inicio)     (agregado     (corrección   (nueva
               de archivo)   de bug)       funcionalidad)

# Ciclo de vida de los archivos en Git

Git gestiona el proceso de guardar cambios en tres estados fundamentales, que facilitan el control y la preparación de las modificaciones antes de hacer un guardado definitivo, conocido como **commit**. Estos tres estados son:

* **Directorio de trabajo (Modified)**: Aquí es donde ocurren las ediciones. Los archivos han sido modificados, pero Git aún no ha registrado esos cambios para ser guardados. En otras palabras, has cambiado el contenido, pero esos cambios todavía no forman parte del historial del proyecto.
* **Preparado (Staged)**: Cuando un archivo está "preparado", significa que has seleccionado específicamente qué modificaciones quieres incluir en el próximo commit. En esta etapa, Git sabe exactamente qué cambios se guardarán, dándote un control preciso para decidir qué incluir y qué dejar para después.
* **Guardado (Committed)**: Finalmente, en el estado "guardado", los cambios están registrados de forma permanente en el historial del proyecto. Esto crea una nueva versión o "instantánea" del proyecto, que puedes consultar o recuperar en cualquier momento.

# Ramas y bifurcaciones de código

Las ramas, también conocidas como bifurcaciones, son divisiones del estado del código que permiten crear caminos independientes para trabajar en nuevas funcionalidades o cambios, sin afectar la estabilidad del repositorio principal. Esto facilita que cada desarrollador pueda avanzar de forma individual, evitando conflictos o errores en el código base.

Una vez que el trabajo en una rama está listo y probado, se puede fusionar (merge) con la rama principal —tradicionalmente llamada master o main— para integrar esos cambios al proyecto.

Para organizar el flujo de trabajo con ramas y fusiones, es recomendable seguir la metodología **GitFlow**, un estándar muy popular en la comunidad de desarrollo. GitFlow está pensado para facilitar el desarrollo ágil, aportando estructura y claridad en la creación y combinación de ramas.

## GitFlow que es y sus comandos

GitFlow es una metodología de trabajo pensada para gestionar de forma ordenada las ramas y el desarrollo del código en un proyecto. Define un flujo estructurado para mantener el código organizado y facilitar el trabajo en equipo. Las ramas principales que utiliza GitFlow son:

| Rama           | Descripción                                                                                       | Comandos básicos GitFlow                           |
|----------------|-------------------------------------------------------------------------------------------------|---------------------------------------------------|
| **master/main**| Código en producción, versión estable y lista para los usuarios finales.                        | -                                                 |
| **hotfix**     | Corrección rápida de errores encontrados en producción.                                         | `git flow hotfix start <nombre>`<br>`git flow hotfix finish <nombre>` |
| **release**    | Código con nuevas funcionalidades listas para pasar a producción tras pruebas de calidad.       | `git flow release start <versión>`<br>`git flow release finish <versión>` |
| **develop**    | Rama base para integrar nuevas funcionalidades; se crean las ramas feature y release desde aquí.| -                                                 |
| **feature**    | Desarrollo aislado de funcionalidades específicas, sin afectar la rama develop hasta finalizar. | `git flow feature start <nombre>`<br>`git flow feature finish <nombre>`  |


                 ┌────────────┐
                 │  master    │◄────────────┐
                 └────┬───────┘             │
                      │                     │
           ┌──────────▼──────────┐          │
           │     develop         │◄────┐    │
           └────────┬────────────┘     │    │
                    │                  │    │
         ┌──────────▼──────────┐       │    │
         │    feature/*        │       │    │
         └─────────────────────┘       │    │
                    │                  │    │
                    ▼                  │    │
          ┌───────────────┐            │    │
          │  release/*    │◄───────────┘    │
          └─────┬─────────┘                 │
                ▼                           ▼
         ┌────────────┐              ┌────────────┐
         │   develop  │              │   master    │
         └────────────┘              └────┬───────┬┘
                                          ▼       ▼
                                   ┌────────┐ ┌─────────┐
                                   │ hotfix │ │  tag vX │
                                   └────────┘ └─────────┘

# Fichero .gitignore

El fichero ```.gitignore``` es un archivo de texto donde se especifica qué archivos y carpetas debe ignorar Git al momento de realizar un commit. Esto es útil para evitar que archivos temporales, configuraciones locales o binarios innecesarios formen parte del historial del proyecto.

Por lo general, el archivo ```.gitignore``` se coloca en la raíz del repositorio, al mismo nivel que el archivo ```README.md```.

```
# Archivos de compilación de Java
*.class

# Directorios de salida
/bin/
/build/
/out/

# Archivos y carpetas de Eclipse
.project
.classpath
.settings/
.metadata/
bin/
tmp/

# Archivos de configuración de IntelliJ IDEA
.idea/
*.iml
*.iws

# Archivos de configuración de NetBeans
/nbproject/private/
/nbbuild/
/dist/
/nbdist/
/.nb-gradle/

# Archivos temporales y logs
*.log
*.tmp
*.swp
*~

# Archivos de sistema
.DS_Store
Thumbs.db

# Archivos de dependencias y empaquetados
*.jar
*.war
*.ear

# Archivos de entorno y configuración local
.env
```

# Configuración en Git

Configurar Git es uno de los primeros pasos para comenzar a trabajar. Usando el comando git config puedes definir tus preferencias, establecer tu identidad, crear alias y mucho más.

Existen tres niveles de configuración:
* Global (```--global```): Aplica las opciones a todos los repositorios del usuario en el sistema.
* Local: Configuraciones que afectan únicamente al repositorio actual en el que estás trabajando.
* Sistema (```--system```): Afecta a todos los usuarios del sistema, y requiere permisos de administrador para modificarse.

Una configuración fundamental es definir el usuario que utiliza Git, ya que cada commit registra el nombre y correo electrónico del autor. Esto permite a los colaboradores saber quién hizo cada cambio.

Para configurar tu identidad global (para todos tus proyectos), utiliza estos comandos
```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu.email@example.com"
```

Si quieres revisar todas las configuraciones actuales (globales, locales y de sistema), puedes usar
```bash 
git config --list
```

# Comando de ayuda

Git incluye documentación integrada para todos sus comandos, lo que facilita consultar cómo funcionan y qué opciones tienen. Para acceder a esta ayuda, puedes usar el comando:
```bash 
git help <comando>
```

# Comandos básicos

Git cuenta con una serie de comandos esenciales que te permiten gestionar el control de versiones de tus proyectos de desarrollo. Con estos comandos básicos podrás iniciar repositorios, registrar y revisar cambios, y colaborar de manera efectiva con otros desarrolladores.

## Git init

El comando ```git init``` crea un nuevo repositorio Git vacío en el directorio local donde se ejecuta. Esto te permite comenzar a registrar el historial de cambios desde ese punto.

Al ejecutarlo, Git crea automáticamente una carpeta oculta llamada ```.git```, que contiene toda la información necesaria para gestionar y almacenar el historial de versiones del proyecto. Gracias a esta estructura, Git puede rastrear, revertir y fusionar cambios a lo largo del tiempo.

Dentro de .git, encontrarás varios archivos y carpetas importantes:

* HEAD: Archivo que apunta a la rama actual en la que estás trabajando. HEAD indica a Git en qué parte del historial estás y qué rama actualizará cuando hagas commits..
* config: Archivo de configuración local del repositorio. Aquí se guardan opciones específicas del proyecto, como la URL de repositorios remotos y preferencias de usuario para ese repositorio.
* index: También llamado "staging area" o área de preparación. Este archivo contiene la lista de archivos preparados para la próxima confirmación (commit). Es donde Git guarda los cambios antes de confirmarlos en el historia.
* objects: Directorio que almacena todos los objetos de Git, como commits, árboles (estructura de carpetas y archivos) y blobs (contenido de archivos). Cada objeto tiene un identificador único (hash SHA-1), lo que garantiza la integridad y permite la compresión eficiente de datos.
* refs: Contiene referencias a ramas y etiquetas del repositorio. Por ejemplo, en refs/heads están las ramas y en refs/tags las etiquetas que marcan versiones importantes.
* logs: Guarda un historial de actualizaciones de cada referencia (como cambios en HEAD o en las ramas). Esto permite registrar y revertir movimientos dentro del historial.
* hooks:  Carpeta con scripts que Git ejecuta automáticamente en eventos específicos (como pre-commit, post-commit o pre-push). Estos scripts son útiles para automatizar tareas como validaciones, pruebas o notificaciones.
* info: Contiene información adicional del repositorio. Aquí está el archivo exclude, que permite definir patrones de archivos a ignorar sin necesidad de modificar el .gitignore.

## Git add

El comando ```git add``` agrega archivos al área de preparación (staging area). Esto significa que marcas los archivos o cambios que quieres incluir en el próximo commit. Puedes añadir un archivo específico o todos los archivos modificados en el directorio de trabajo.
```bash
git add nombre_del_archivo     # Para un archivo específico
git add .                      # Para todos los archivos modificados
```

## Git status

El comando ```git status``` te muestra el estado actual de los archivos en tu repositorio. Con él puedes ver qué archivos han sido modificados pero aún no están preparados (staged), cuáles están listos para ser incluidos en el próximo commit y cuáles no están siendo rastreados por Git (archivos no versionados).

Este comando es fundamental para entender en qué punto del ciclo de trabajo se encuentran tus archivos y qué acciones puedes tomar a continuación.

## Git commit

El comando ```git commit``` guarda una “instantánea” de los cambios que has preparado en el área de staging. Cada commit representa un punto en el historial del proyecto y debe incluir un mensaje descriptivo que explique qué cambios se realizaron.

Para hacer un commit rápido con un mensaje corto, puedes usar
```bash
git commit -m "Mensaje descriptivo del commit"
```

Este mensaje es importante porque ayuda a ti y a otros colaboradores a entender qué cambios se hicieron en ese punto del proyecto

## Git log

El comando ```git log``` muestra el historial de commits del repositorio, con detalles como el autor, la fecha y el mensaje que explica cada cambio. Es una herramienta clave para revisar la evolución del proyecto.

Además, puedes usar varias opciones para hacer la información más útil y legible:

* git log --oneline: Muestra cada commit en una sola línea, con su identificador corto y el mensaje, ideal para tener una vista rápida.
* git log --graph: Muestra un gráfico en texto que representa la estructura de ramas y fusiones, útil para visualizar el flujo de trabajo.
* git log --author="Nombre": Filtra los commits hechos por un autor específico.
* git log --since="2 weeks ago": Muestra solo los commits realizados desde hace dos semanas (puedes usar otras fechas o rangos).
* git log -p: Muestra las diferencias (diff) introducidas en cada commit
```bash
git log --oneline --graph --decorate --all
```

# Comandos básicos para repositorios remotos

## Git clone

El comando ```git clone <URL-del-repositorio>```  te permite copiar un repositorio remoto (por ejemplo, de GitHub o GitLab) a tu equipo local. Esto crea una copia completa del proyecto, incluyendo todo su historial de cambios.

Es la forma habitual de empezar a trabajar en un proyecto colaborativo, ya que te da acceso a todo el código y las ramas existentes para poder modificarlas y colaborar..

## Git remote

El comando ```git remote``` se utiliza para gestionar las conexiones con repositorios remotos en Git, es decir, esos repositorios alojados en servidores como GitHub, GitLab, etc.

Algunos comandos básicos para trabajar con remotos son:

* Agregar un repositorio remoto 
```bash 
git remote add nombre_remoto URL_del_repositorio
```
Esto crea una conexión con un repositorio remoto que podrás usar para enviar (push) o recibir (fetch) cambios
* Ver las URLs asignadas (tanto para fetch como para push).
```bash 
git remote -v
```
* Eliminar un repositorio remoto 
```bash 
git remote remove nombre_remoto
```
* Modificar la URL de un repositorio remoto existente
```bash 
git remote set-url nombre_remoto nueva_URL
```

Estos comandos te permiten administrar fácilmente los repositorios remotos vinculados a tu proyecto

## Git push

El comando ```git push``` se utiliza para enviar los commits que tienes en tu repositorio local hacia un repositorio remoto. Esto hace que tus cambios estén disponibles para otros colaboradores y se integren en el proyecto compartido.

Por ejemplo, para enviar los cambios a la rama principal (main) en el remoto llamado origin.
```bash 
git push origin main
```

Es importante recordar que, para poder hacer push, la rama local debe estar actualizada con la remota, para evitar conflictos.

## Git pull

El comando ```git pull``` se usa para traer y combinar los cambios del repositorio remoto en tu repositorio local. Esto te permite mantener tu copia actualizada con las últimas modificaciones que otros colaboradores han hecho en el proyecto.

En esencia, git pull realiza dos acciones consecutivas:
* Descarga los cambios del repositorio remoto (git fetch).
* Fusiona esos cambios con tu rama local activa (git merge).

Un ejemplo básico para actualizar la rama principal (main) desde el remoto origin es
```bash
git pull origin main
```

## Git fetch

El comando ```git fetch``` descarga los cambios más recientes desde un repositorio remoto hacia tu repositorio local, actualizando las referencias remotas. Sin embargo, no modifica tu rama actual ni tu área de trabajo. Esto significa que los cambios están disponibles localmente, pero aún no se integran en tu código activo.

Este comando es útil cuando quieres revisar o preparar la integración de los cambios remotos sin afectar tu trabajo actual.

Por ejemplo, para obtener los últimos cambios del remoto ```origin```.
```bash
git fetch origin
```

# Comandos de utilidades

## Git Clean

El comando ```git clean``` se utiliza para eliminar archivos y directorios no rastreados (untracked) en el repositorio, es decir, aquellos que no están bajo control de versiones.

Precaución: Este comando puede ser destructivo, ya que elimina archivos que podrían ser importantes y que aún no has agregado a Git. Por seguridad, Git requiere que uses la opción ```-f``` (force) para que la eliminación se ejecute realmente.
```bash
git clean -f
```

Antes de eliminar cualquier archivo, puedes listar qué archivos o directorios serían afectados usando la opción -n (dry run), que simula la acción sin borrar nada:
```bash
git clean -n
```

Así podrás revisar qué se eliminaría y evitar pérdidas accidentales.

## Git mv

El comando ```git mv <origen> <destino>``` se utiliza para mover o renombrar archivos dentro de un repositorio Git de manera controlada. Esto significa que, además de cambiar la ubicación o el nombre del archivo en el sistema de archivos, Git registra este cambio en el índice (staging area) y en el historial del repositorio.

Usar ```git mv``` facilita el seguimiento de estos movimientos o renombramientos, manteniendo un historial claro y evitando confusiones en el control de versiones.

## Git blame

El comando ```git blame <nb-archivo>``` muestra, línea por línea, quién fue el autor de cada cambio en un archivo específico. Esta herramienta es muy útil para rastrear la autoría de modificaciones concretas, facilitando entender quién hizo cada cambio y cuándo, junto con el mensaje del commit asociado.

Con ```git blame``` puedes analizar el historial detallado de un archivo, lo que ayuda a identificar responsabilidades, entender decisiones y resolver dudas sobre el código.

## Git grep

El comando ```git grep <patrón-de-búsqueda>``` permite buscar texto dentro de los archivos de un repositorio Git. Es una herramienta rápida y eficiente para encontrar patrones específicos en el código fuente o en cualquier archivo versionado del proyecto.

A diferencia de las búsquedas tradicionales, git grep opera dentro del contexto del repositorio, lo que facilita búsquedas precisas sobre versiones, ramas y commits.

* Buscar en una rama concreta.
```bash
git grep <patrón-de-búsqueda> <nombre-rama>
```
* Buscar en los archivos de un commit específico.
```bash
git grep <patrón-de-búsqueda> <commit-id>
```
* Buscar solo dentro de un directorio.
```bash
git grep <patrón-de-búsqueda> -- <directorio>
```
* Mostrar solo los nombres de los archivos que contienen el patrón.
```bash
git grep -l <patrón-de-búsqueda>
```
* Realizar una búsqueda insensible a mayúsculas y minúsculas.
```bash
git grep -i <patrón-de-búsqueda>
```
* Mostrar el número de línea donde se encuentra la coincidencia.
```bash
git grep -n <patrón-de-búsqueda>
```
* Incluir en la búsqueda archivos no rastreados (no versionados).
```bash
git grep <patrón-de-búsqueda> --no-index
```

## Git alias

Aunque git alias no es un comando oficial, Git permite crear alias personalizados para los comandos que usas con frecuencia. Un alias es como un “atajo”: un nombre corto que ejecuta un comando completo o una combinación de comandos, facilitando y agilizando tu trabajo diario.

Los alias se configuran en el archivo .gitconfig, ya sea a nivel global (para todos los repositorios en tu máquina) o local (solo para un repositorio específico). Puedes añadirlos manualmente en el archivo o usar el comando git config, que es la forma más sencilla.

La sintaxis básica para crear un alias global es:
```bash
git config --global alias.<alias> "<comando>"
```

* ```--global```: Hace que el alias esté disponible en todos los repositorios de tu usuario.
* ```<alias>```: El nombre corto que quieres usar para el comando.
* ```<comando>```: El comando o secuencia de comandos que se ejecutará cuando uses el alias.

## Git reset

El comando ```git reset``` es uno de los más potentes de Git, utilizado para deshacer cambios y modificar el historial de commits. Su función principal es mover el puntero de la rama actual a un commit anterior o a una referencia específica, afectando el área de trabajo y el índice según las opciones usadas.

Las formas más comunes de usarlo son:

* git reset --soft <commit>
Mueve el puntero de la rama al commit indicado, sin modificar el índice ni el directorio de trabajo. Los archivos modificados permanecen en el área de staging, listos para ser confirmados en un nuevo commit.
* git reset --mixed <commit> (opción por defecto)
Mueve el puntero de la rama al commit indicado, restablece el índice (área de staging) pero mantiene los cambios en el directorio de trabajo. Es útil para deshacer commits pero conservar el trabajo local sin confirmar.
* git reset --hard <commit>
Mueve el puntero de la rama al commit indicado y restablece tanto el índice como el directorio de trabajo, eliminando cualquier cambio local que no haya sido guardado. Usa esta opción con precaución, ya que los cambios no confirmados se pierden.

Historial inicial:
A --- B --- C --- D  (HEAD)

Aplicamos:
git reset --hard B

Resultado:
A --- B  (HEAD)   ← C y D se eliminan del historial local

Peligroso si ya hiciste push

## Git revert

El comando ```git revert <commit-id>``` permite deshacer los cambios introducidos por un commit anterior, creando un nuevo commit que revierte esos cambios sin modificar el historial existente. Es una forma segura de "dar marcha atrás" sin perder el historial.

Opciones comunes:

* git revert <commit-id>
Revertir el commit especificado, generando un nuevo commit que invierte sus cambios.
* git revert --no-edit
Realiza el revert sin abrir el editor para modificar el mensaje del nuevo commit. Usa el mensaje por defecto.
* git revert --edit (por defecto)
Abre el editor para que puedas modificar el mensaje del commit de reversión.
* git revert -n o git revert --no-commit
No crea el commit automáticamente; solo aplica los cambios al área de trabajo y al índice, permitiendo revisar o modificar antes de confirmar.
* git revert --continue
Se usa cuando durante el proceso de revert se detectan conflictos y los has resuelto manualmente; continúa con la operación.
* git revert --abort
Cancela el proceso de revert en caso de conflictos complejos o si decides no continuar.

Historial inicial:
A --- B --- C --- D  (HEAD)

Aplicamos:
git revert C
git revert D

Resultado:
A --- B --- C --- D --- E' --- F'  (HEAD)
(E' y F' son commits que deshacen los efectos de C y D)

## Git restore

El comando ```git restore``` fue introducido en Git 2.23 para simplificar y separar algunas funciones que antes realizaba git checkout. Su principal objetivo es restaurar el contenido de archivos a partir del último commit o de cualquier commit específico, facilitando la reversión de cambios sin afectar otras áreas.

Algunas operaciones comunes con git restore son:
* Restaurar un archivo a su estado en el último commit:
* Restaurar todos los archivos modificados en el directorio de trabajo:
* Quitar archivos del área de preparación (hacer un “unstage”):
* Restaurar un archivo desde una rama específica:
* Restaurar un archivo desde un commit específico, forzando la acción sin pedir confirmación:

## Git amend

El comando ```git commit --amend``` (comúnmente llamado git amend) se utiliza para modificar el último commit realizado en tu rama. Esto es útil cuando quieres corregir el mensaje del commit, agregar archivos que olvidaste incluir, o ajustar cambios ya confirmados.

Algunos usos comunes:
* git commit --amend
Abre el editor de texto configurado en Git (como Vim o Nano) para modificar el mensaje del último commit.
* git add <archivos> seguido de git commit --amend
Permite añadir archivos nuevos al último commit. Tras agregar los archivos al área de preparación, este comando actualizará el commit, y podrás editar el mensaje si lo deseas. Si no modificas el mensaje, se mantendrá el original.
* git commit --amend --no-edit
Añade los archivos preparados al último commit sin abrir el editor para cambiar el mensaje; el mensaje original se conserva.
* git commit --amend --reset-author
Cambia el autor del último commit al usuario configurado actualmente en Git, útil si quieres actualizar la identidad del commit.

## Git cherry-pick

El comando ```Git cherry-pick <commit-id>``` permite aplicar uno o varios commits específicos de otra rama en tu rama actual. Esto es especialmente útil cuando solo quieres incorporar ciertos cambios puntuales sin hacer un merge completo.

Funcionamiento básico:

* Si no hay conflictos, el commit se integra directamente en tu rama actual.
* Si aparecen conflictos, deberás resolverlos manualmente, añadir los archivos corregidos con git add y luego continuar con
```bash
git cherry-pick --continue
```
* Si decides cancelar la operación debido a conflictos o cualquier otro motivo, puedes abortar el proceso con:
```bash
git cherry-pick --abort
```

## Git rebase

El comando ```git rebase <nb-rama>``` se utiliza para integrar cambios de una rama a otra de manera diferente a como lo hace git merge. En lugar de crear un nuevo "commit de fusión" como lo hace git merge, mueve o reaplica los commits de una rama sobre otra, lo que puede resultar en un historial de commits más limpio y lineal.

* ```git rebase -i``` El rebase interactivo te permite modificar el historial de commits antes de realizar el rebase. Puedes reordenar, combinar (squash), modificar, eliminar o dividir commits. Es útil para limpiar el historial de commits antes de integrarlo a una rama principal.
Esto abrirá una interfaz de texto que te permitirá editar los últimos 3 commits. Desde ahí puedes elegir acciones como:
  * pick: Mantener el commit tal cual.
  * reword: Cambiar el mensaje del commit.
  * edit: Modificar el commit.
  * squash: Combinar commits.
  * drop: Eliminar un commit.
* ```git rebase --onto <nueva-base> <id-commit-antiguo> <rama>``` te permite mover un conjunto de commits de una rama a otra, especificando un rango de commits más complejo.

## Git stash

El comando ```git stash``` es una herramienta muy práctica que te permite guardar temporalmente cambios no confirmados en tu área de trabajo, ya sea en el área de preparación (staging) o en el directorio de trabajo. Esto es útil cuando necesitas cambiar de rama o trabajar en otra cosa sin perder los cambios que aún no quieres confirmar.

### Formas de guardar cambios en el stash

* ```git stash```
Guarda todos los cambios tanto del directorio de trabajo como del área de preparación.
* ```git stash -k o git stash --keep-index```
Guarda solo los cambios en el directorio de trabajo, dejando intactos los que ya están en el área de preparación.
* ```git stash save "mensaje descriptivo"```
Guarda los cambios con un mensaje personalizado para poder identificarlos fácilmente más tarde. Actualmente esta obsoleto y es recomendable usar ```git stash push```

### Comandos útiles para gestionar el stash

* ```git stash list```
Muestra la lista de todos los stashes almacenados.
* ```git stash show -p stash@{n}```
Muestra los detalles y diferencias del stash seleccionado.
* ```git stash apply stash@{n}```
Aplica los cambios guardados en un stash sin eliminarlo de la lista.
* ```git stash pop```
Aplica el stash más reciente y lo elimina de la lista, es decir, “saca” los cambios y limpia el stash.
* ```git stash drop stash@{n}```
Elimina un stash específico de la lista.
* ```git stash clear```
Borra todos los stashes almacenados.
* ```git stash -u o git stash --include-untracked```
Crea un stash que incluye no solo los archivos modificados sino también los archivos no versionados (untracked).
* ```git stash branch <nombre-de-rama>```
Crea una nueva rama a partir del commit actual y aplica el stash en esa nueva rama para continuar el trabajo sin interferir en la rama actual.

## Git reflog

El comando ```git reflog``` muestra un registro detallado de todos los movimientos recientes del puntero HEAD y otras referencias dentro de tu repositorio.

Esto te permite:
* Ver cómo y cuándo ha cambiado el puntero HEAD.
* Recuperar commits perdidos, por ejemplo, tras un git reset --hard u otras acciones que puedan eliminar referencias.
* Rastrear cambios en las ramas: merges, rebases o cambios de rama (checkout).
* Identificar cuándo y cómo se movieron referencias de ramas.

Puedes limitar el número de entradas que muestra:
```bash
git reflog -n 5
```
O mostrar fechas relativas para facilitar la lectura:
```bash
git reflog --date=relative
```

Ejemplo de salida
```bash
$ git reflog
e19c7a1 HEAD@{0}: commit: Agregar funcionalidad de autenticación
b7d8f32 HEAD@{1}: commit: Corregir bug en el procesamiento de datos
7c2e9b3 HEAD@{2}: commit: Refactorizar lógica de la API
f32b111 HEAD@{3}: checkout: moving from feature-branch to master
c1d2e44 HEAD@{4}: commit: Mejorar validación de entradas
a34d5f2 HEAD@{5}: commit: Agregar prueba unitaria para validación
2b5a1c6 HEAD@{6}: reset: moving to HEAD^
8a22d7f HEAD@{7}: commit: Implementar nueva función de cálculo
5c8b40d HEAD@{8}: rebase -i (finish): rebase a7b6d88..8a22d7f
5c8b40d HEAD@{9}: rebase -i (start): rebase de master
3e4d9a1 HEAD@{10}: checkout: moving from master to feature-branch
b7d8f32 HEAD@{11}: commit: Corregir bug en el procesamiento de datos
d82e4a9 HEAD@{12}: commit: Agregar funcionalidad de autenticación
```

# Comandos de Ramas y Merge

## Git branch

El comando ```git branch``` se utiliza para gestionar las ramas dentro de un repositorio Git.

* ```git branch```
Lista todas las ramas locales del repositorio. La rama actual estará marcada con un asterisco (*).
* ```git branch <nombre-rama>```
Crea una nueva rama con el nombre especificado, pero no cambia a esa rama automáticamente.
* ```git branch -d <nombre-rama>```
Elimina una rama local de forma segura (Git evitará eliminarla si contiene cambios no fusionados).
* ```git branch -m <nuevo-nombre-rama>```
Cambia el nombre de la rama actual por el nuevo nombre indicado.
* ```git branch -r```
Lista las ramas remotas del repositorio.
* ```git branch -a```
Lista todas las ramas, tanto locales como remotas.

## Git switch

El comando ```git switch <nombre-de-la-rama>``` es un comando moderno introducido en Git para facilitar el cambio entre ramas del repositorio.

* ```git switch <nombre-de-la-rama>```
Cambia a la rama especificada.
* ```git switch -c <nombre-de-la-rama>```
Crea una nueva rama con el nombre indicado y cambia automáticamente a ella.

## Git tag

El comando ```git tag <nombre-del-tag>``` se utiliza para crear etiquetas (tags) en puntos específicos del historial del repositorio. Las etiquetas permiten marcar versiones importantes del proyecto, como lanzamientos (releases), hitos o momentos relevantes para facilitar el seguimiento.

### Creación y gestión de etiquetas

* ```git tag -a <version> -m "<mensaje>"```
Crea una etiqueta anotada con un mensaje descriptivo.
* ```git tag -d <nombre-del-tag>```
Elimina una etiqueta local.
* ```git push origin <nombre-del-tag>```
Envía una etiqueta específica al repositorio remoto.
* ```git push --tags```
Envía todas las etiquetas locales al repositorio remoto.
* ```git push --delete origin <nombre-del-tag>```
Elimina una etiqueta del repositorio remoto.

### Tipos de etiquetas

* Etiquetas ligeras (lightweight tags):
Son simplemente un puntero a un commit específico, sin metadatos adicionales.
Ejemplo: v1.0
* Etiquetas anotadas (annotated tags):
Contienen metadatos completos, incluyendo autor, fecha y un mensaje. Se almacenan como objetos en Git y son recomendadas para marcar versiones oficiales o hitos importantes.

## Git merge

El comando ```git merge <nombre-de-la-rama-a-fusionar>``` se utiliza para combinar los cambios de una rama en otra. Normalmente, este comando se ejecuta desde la rama de destino, fusionando los cambios de la rama especificada.

### Fast-Forward Merge (fusión rápida)

Este tipo de merge ocurre cuando la rama de destino no tiene ningún cambio desde el punto en el que se separó de la rama que se está fusionando. En otras palabras, si la rama principal (por ejemplo, main) no tiene cambios nuevos desde que se creó la rama que quieres fusionar, Git simplemente mueve el puntero de la rama hacia adelante al punto de la otra rama. No se crea un commit de merge porque no hay conflicto.
Resultado: No se crea un commit de merge, solo un avance en la referencia de la rama.

### Merge con Commit de Fusión (Merge Commit / Three-way merge)

Este tipo de merge se realiza cuando ambas ramas (la rama de destino y la rama que se va a fusionar) tienen cambios que no están presentes en la otra. Git no puede avanzar simplemente el puntero de la rama de destino, por lo que crea un commit de fusión. Este commit refleja la fusión de los cambios de ambas ramas.
Resultado: Git crea un commit especial llamado commit de fusión, que tiene dos padres: uno de la rama de destino (por ejemplo, main) y otro de la rama fusionada (por ejemplo, feature).

### Merge con Conflictos

Los conflictos ocurren cuando los cambios realizados en ambas ramas afectan la misma parte del código de manera incompatible. En este caso, Git no puede resolver automáticamente los conflictos y te pedirá que los resuelvas manualmente. Después de resolver los conflictos, deberás agregar los archivos modificados a la zona de preparación (staging area) y luego hacer un commit para completar el merge.

### Squash Merge (Fusión en un solo commit)

Aunque el comando git merge por sí mismo no realiza una "fusión squash", Git permite una fusión squash mediante la opción --squash ```git merge --squash <nombre-de-la-rama>```. Esta opción toma todos los commits de una rama y los combina en un solo commit cuando se fusiona con la rama de destino. Esto es útil cuando se desea tener un historial de commits más limpio.

# Comandos de comparación

## Git show

El comando ```git show <commit-id>``` permite visualizar información detallada sobre un objeto en Git. Aunque el uso más común es mostrar los detalles de un commit, también se puede utilizar con etiquetas (tag), árboles (tree) o blobs (archivos específicos).

Cuando se utiliza con un commit-id, la salida incluye:
* El hash completo del commit.
* El autor del commit.
* La fecha y hora del commit.
* El mensaje del commit.
* El diff (diferencia) introducido por ese commit.

```bash
git show <commit-id>
git show --stat 5e2f1a9
git show v1.0.0
```

## Git diff

El comando ```git diff``` es una herramienta fundamental de Git que permite ver las diferencias entre dos estados del repositorio. Estas diferencias pueden referirse a:

* Cambios en archivos aún no preparados para commit (working directory vs staging area).
* Cambios preparados (staging area vs último commit).
* Cambios entre dos commits, ramas o archivos.

* ```git diff``` Muestra las diferencias entre el directorio de trabajo (los cambios realizados en los archivos) y el staging area (el área de preparación para el próximo commit).
* ```git diff --staged``` Mostrar los cambios que se han añadido al área de staging.
* ```git diff <commit-id> <commit-id>``` Puedes ver las diferencias entre dos commits específicos.
* ```git diff <nb-branch> <nb-branch>``` para comparar los cambios entre dos ramas.
* ```git diff <archivo>``` ver las diferencias de un archivo específico.

## Git shortlog

El comando ```git shortlog``` proporciona un resumen condensado de los commits en un repositorio, agrupados por autor. A diferencia de git log, que muestra un historial detallado, git shortlog es ideal para visualizar rápidamente las contribuciones individuales al proyecto.

* ```git shortlog``` Muestra un resumen de los commits por autor, con una lista de mensajes de commit.
* ```git shortlog -n``` ordena los resultados de acuerdo al número de commits realizados para cada autor (de mayor a menor).
* ```git shortlog --since="fecha(yyyy-MM-dd)" --until="fecha(yyyy-MM-dd)"``` filtrar los commits en un rango de fechas específico.
* ```git shortlog --summary --numbered``` obtiene el total de commits agrupados por usuario.
* ```git shortlog -s``` ver solo el número de commits de cada autor, sin los detalles de los mensajes.
* ```git shortlog -e``` agrupa los commits por correo electrónico.
* ```git shortlog -c``` para agruparlo por fecha en lugar de por autor.
* ```git shortlog -w``` omite aquellos cambios en los espacios en blanco (útil para ver un resumen de las contribuciones sin distracciones por cambios de formato).

## Git describe

El comando ```git describe``` es utilizado para obtener una etiqueta descriptiva (o "nombre de referencia") asociada al commit actual o a un commit específico. Este comando es útil cuando quieres una forma más amigable y legible de identificar un commit que no solo involucra un hash largo, sino una referencia más comprensible basada en las etiquetas del repositorio.
