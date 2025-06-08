<div align="center">
  <img src="https://raw.githubusercontent.com/jorgenavarroenamoradotokio/docs/main/logo/Git-Logo.svg">
</div>

## Índice
- [Introducción](#introducción)
  - [Características](#características)
  - [Conceptos básicos](#conceptos-básicos)
- [Fucnionamiento](#fucnionamiento)
- [Ciclo de vida de los archivos en git](#ciclo-de-vida-de-los-archivos-en-git)
- [Las ramas y/o bifurcaciones de código](#las-ramas-yo-bifurcaciones-de-código)
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
  - [Git reflog](#git-reflog)
- [Comandos de Ramas y Merge](#comandos-de-ramas-y-merge)
  - [Git branch](#git-branch)
  - [Git switch](#git-switch)
  - [Git tag](#git-tag)
  - [Git merge](#git-merge)
    - [Fast-Forward Merge (fusión rápida)](#fast-forward-merge-fusión-rápida)
    - [Merge con Commit de Fusión (Merge Commit)](#merge-con-commit-de-fusión-merge-commit)
    - [Merge con Conflictos](#merge-con-conflictos)
    - [Squash Merge (Fusión en un solo commit)](#squash-merge-fusión-en-un-solo-commit)
- [Comandos de comparación](#comandos-de-comparación)
  - [Git show](#git-show)
  - [Git diff](#git-diff)
  - [Git shortlog](#git-shortlog)
  - [Git describe](#git-describe)

# Introducción

Git es un sistema de control de versiones distribuidas, diseñado para gestionar el desarrollo de proyectos de software de forma colaborativa y eficiente. Fue creado por Linus Torvalds en 2005, y su propósito principal es permitir que los desarrolladores realicen un seguimiento de los cambios en el código fuente de un proyecto, facilitando la colaboración, la organización y la prevención de errores o conflictos entre versiones.

## Características

- Distribuido: A diferencia de otros sistemas de control de versiones, en Git cada desarrollador tiene una copia completa del historial de cambios del proyecto en su máquina local. Esto permite trabajar offline y compartir cambios sin un servidor central, aunque también es compatible con repositorios centralizados.
- Rastreo de versiones: Git guarda una "instantánea" de cada cambio realizado en los archivos de un proyecto. Esto permite revertir cambios, comparar versiones anteriores y saber quién hizo cada cambio y cuándo.
- Branching (ramas): Git permite trabajar en diferentes "ramas" o versiones paralelas del proyecto. Esto facilita que los equipos desarrollen nuevas funcionalidades o correcciones de errores sin afectar el código principal (por lo general, en la rama mano master). Una vez que se finaliza una funcionalidad, esta puede estar integrada de nuevo en la rama principal.
- Integración y resolución de conflictos: Git permite combinar el trabajo de diferentes personas, y proporciona herramientas para resolver conflictos cuando dos personas modifican el mismo código.

## Conceptos básicos

- Repositorio (repo): Es el lugar donde se almacena el proyecto, junto con su historial de cambios.
- Commit: Es una "captura" de los cambios realizados en el proyecto en un momento específico.
- Branch (rama): Una línea de desarrollo que permite trabajar en paralelo en el proyecto.
- Fusionar: Combinar cambios de una rama en otra.
- Push/Pull: Envío (push) o recepción (pull) de cambios entre el repositorio local y uno remoto.

# Fucnionamiento

El principal funcionamiento de git esta basado en capturar "versiones" de documentos cada vez que el usuario realiza cambios y los guarda. Esto facilita el seguimiento de cada modificación, permite regresar a versiones anteriores y colaborar en proyectos de equipo al mantener un historial claro de todo lo que se ha realizado sobre uno o varios documentos.

Cada vez que se guardan cambios en Git, este crea una "instantánea" de los archivos en su estado actual. Esta instantánea funciona como una foto del proyecto en ese momento, almacenando detalles específicos sobre cómo están organizados los archivos, su contenido y cualquier modificación realizada. Con esta estructura, Git guarda solo las diferencias entre cada versión para no ocupar espacio innecesario, mientras sigue permitiendo reconstruir cada estado pasado del proyecto.

Git organiza estas "instantáneas" en un historial de cambios que registra cada versión del proyecto en el orden en que se hicieron. Cada entrada en el historial contiene información como quién realizó el cambio, cuándo ocurrió y un pequeño mensaje que describe el cambio realizado. Esto crea un registro cronológico completo del desarrollo del proyecto, haciendo posible revisar el proceso de cambios desde el inicio y entender la evolución del proyecto.

# Ciclo de vida de los archivos en git

Git organiza el proceso de guardado de cambios en tres estados clave, que ayudan a controlar y preparar las modificaciones antes de hacer un guardado definitivo (llamado commit). Estos tres estados son:

- Directorio de trabajo (Modified): En este estado, los archivos del proyecto han sido editados, pero Git aún no ha preparado estos cambios para ser guardados. Es decir, has realizado cambios en el contenido, pero aún no están listos para formar parte del historial del proyecto.

- Preparado (Staged): Cuando los archivos están en el estado "Preparado", significa que has marcado ciertos cambios como listos para ser guardados en el próximo commit. En esta etapa, Git ya sabe exactamente qué cambios específicos se incluirán en el próximo guardado, permitiendo un control sobre qué modificaciones se guardarán y cuáles no.

- Guardado (Committed): En el estado "Guardado", los cambios ya están registrados permanentemente en el historial del proyecto. Esto crea una versión nueva del proyecto, permitiendo a Git almacenar esa "instantánea" del proyecto, que se puede revisar o restaurar en el futuro.

# Las ramas y/o bifurcaciones de código

Las ramas o bifurcaciones de código son una división del estado del código que nos permite crear nuevos caminos a favor de la evolución del código para trabajar de manera individual sobre una funcionalidad son perjudicar y comprometer la estabilidad de los repositorios. Para posteriormente fusionarlo con la rama principal (master/main).
Es recomendable usar la metodología de GitFlow a la hora de crear ramas y fusionar su contenido, ya que es un estándar global usando por la comunidad de desarrollo enfocado principalmente al desarrollo ágil.

## GitFlow que es y sus comandos

GitFlow es una metodología de trabajo enfocada en la gestión de ramas y del código. Para ello se definen las siguientes estructuras.
- Rama principal(master/main) Almacena el código que está en produccion.
- Rama hotfix: Alamcena las correciones de los bugs y fallos localizados en producción.
- Rama release: Almacena el código de las nuevas funcionalidades que pasaran a producción cuando pase los estándares de calidad.
- Rama develop: Copia de la rama principal de la cual se crean las ramas feature y realease.
- Rama feature: Almacena el código de una funcionalidad.

# Fichero .gitignore

El documento ```.gitignore``` es un archivo de texto en el que se indica a git que archivos y carpetas de un proyecto debe de ignorar a la hora de realizar commit. Este documento normalmente se coloca en la raíz del repositorio a la misma altura que el documento ```README.mk```

# Configuración en Git

Configurar Git es uno de los primeros pasos para empezar a trabajar. A través de comando git config podemos definir nuestras preferencias, establecer tu identidad, crear alias, etc

Existen tres niveles de configuración:
- Global (```--global```): Configura opciones que se aplican a todos los repositorios del usuario.
- Local: Las configuraciones locales afectan solo al repositorio en el que estas trabajando.
- Sistema (```--system```): Aplica configuraciones a todos los usuarios en el sistema, requiere permisos de administrador.

Configurar el usuario que lo utiliza: Esto es esencial, ya que Git registra el nombre y el correo electrónico del autor en cada confirmación. Así, otros colaboradores sabrán quién realizó cada cambio. Usa los siguientes comandos para definir tu identidad global (afecta a todos los repositorios en tu sistema) o específico para un proyecto
```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu.email@example.com"
```
- ```git config --list``` lista la configuración que tenemos.

# Comando de ayuda

Git tiene integrada toda la documentación del funcionamiento de los múltiples comandos que lo componen, para poder consultar la wiki usaremos el comando ```git help```.

# Comandos básicos

Git ofrece una serie de comandos esenciales para gestionar el control de versiones en proyectos de desarrollo. Estos comandos básicos te permiten iniciar y gestionar repositorios, registrar cambios en el código, ver el historial y colaborar con otros.

## Git init

El comando ```git init``` inia un nuevo repositorio en git en el directorio local. Crea un repositorio vacío donde puedes empezar a registrar el historial de cambios. 

Al ejecutar este comando automáticamente crea una carpeta oculta con nombre ```.git```. Esta carpeta contiene toda la información que Git necesita para gestionar y almacenar el historial de versiones del proyecto, de manera que se puedan rastrear, revertir y fusionar cambios a lo largo del tiempo.

- HEAD: Es un archivo que apunta a la rama actual en la que se está trabajando. HEAD permite a Git saber en qué parte del historial se encuentra el trabajo actual y qué rama debe actualizar al hacer commits.

- config: Archivo de configuración específico para el repositorio. Aquí se almacenan configuraciones locales del proyecto, como las remotas (URL de repositorios), opciones específicas y preferencias de usuario para el repositorio en cuestión.

- index: También conocido como el "staging area" o área de preparación, este archivo contiene una lista de archivos preparados para la próxima confirmación. Aquí es donde Git guarda la información de los cambios antes de confirmarlos en el historial.

- objects: Este directorio almacena todos los objetos de Git, como commits, árboles (estructura de carpetas y archivos) y blobs (contenido de los archivos). Cada objeto se almacena usando un identificador único (SHA-1 hash), lo que garantiza la integridad y permite la compresión de datos.

- refs: Este directorio contiene referencias a las ramas y etiquetas del repositorio. Dentro de refs/headsestán las referencias a cada rama, y en refs/tagsse guardan las etiquetas de las versiones marcadas del proyecto.

- logs: Almacena un historial de las actualizaciones de cada referencia (por ejemplo, cambios en HEAD y en las ramas). Esto permite registrar y deshacer cambios en las ramas.

- hooks: Contiene scripts que Git ejecuta automáticamente en ciertos eventos (como pre-commit, post-commit, pre-push, etc.). Estos scripts son útiles para automatizar tareas como validaciones de código, pruebas automáticas, o notificaciones antes o después de realizar ciertas acciones.

- info: Almacena archivos de información adicional sobre el repositorio. Aquí se encuentra el archivo exclude, que permite especificar patrones de archivos para ignorar sin añadirlos al archivo .gitignore.

## Git add

El comando ```git clone <URL-del-repositorio>``` agrega archivos al área de preparación (staging area), es decir, marca los archivos que quieres incluir en el próximo commit. Se puede agregar un solo archivo o todos los archivos modificados.

```bash
git add nombre_del_archivo     # Para un archivo específico
git add .                      # Para todos los archivos modificados
```

## Git status

El comando ```git status``` muestra el estado de los archivos en el repositorio. Este comando te dice si hay cambios que no están preparados, qué archivos están listos para el commit y cuáles no están versionados.

## Git commit

El comando ```git commit``` guarda una “instantánea” de los cambios en el repositorio. Un commit es un paso en el historial del proyecto y debe ir acompañado de un mensaje que describa los cambios.
- ```git commit -m "<msg del commit>"``` realizar el commit de una manera más sencilla solo indicando el título del commit

## Git log

El comando ```git log``` permite ver el historial de commits del repositorio, mostrando detalles de cada commit como el autor, la fecha y el mensaje asociado.

# Comandos básicos para repositorios remotos

## Git clone

El comando ```git clone <URL-del-repositorio>``` permite copiar un repositorio existente, como uno que esté en GitHub o GitLab, a tu equipo local. Esto es especialmente útil para trabajar en proyectos colaborativos.

## Git remote

El comando ```git remote``` permite gestionar las conexiones a los repositorios remotos en Git.
- Para añadir un nuevo repositorio remoto usaremos ```git remote add nombre_remoto URL_del_repositorio```.
- Para consultar las urls que tenemos asignadas (fetch y push) al repositorio usaremos ```git remote -v``` .
- Para agregar eliminar una usaremos ```git remote remove nombre_remoto```.
- Para modificar una usamremos ```git remote set-url nombre_remoto nueva_URL```.

## Git push

El comando ```git push``` nos permite enviar los commits locales al repositorio remoto, haciendo que los cambios sean accesibles para otros colaboradores.

## Git pull

El comando ```git pull``` permite traernos los cambios del repositorio remoto al repositorio local, permitiendo actualizar el código local con los últimos cambios del proyecto.

## Git fetch

El comando ```git fetch``` se utiliza para actualizar tu repositorio local con los cambios más recientes de un repositorio remoto, sin modificar tu rama actual o tu área de trabajo. En otras palabras, descarga los datos más recientes desde un servidor remoto, pero no aplica esos cambios automáticamente en tu entorno de trabajo.

# Comandos de utilidades

## Git Clean

El comando ```git clean``` permite eliminar archivos no rastreados (untracked) y directorios del repositorio. Debemos de tener en cuenta que este comando es potencialmente destructivo porque puede eliminar archivos importantes que no se han añadido al control de versiones. Por esta razón, Git requiere que utilice se utilice la opciones -f(force) para eliminar solo ficheros.
No solo podemos eliminar los documentos que no estén rastreados sino podemos obtener el listado de documentos que son afectados si ejecutamos el comando ```git clean -f``` para ellos usaremos ```git clean -n```.

## Git mv

El comando ```git mv <origen> <destino>``` se utiliza para mover o renombrar archivos dentro de un repositorio de manera controlada, es decir, realizando un seguimiento de los cambios en el índice (staging area) y en el historial del repositorio. Este comando no solo mueve o renombra los archivos en el sistema de archivos, sino que también informa a Git sobre los cambios, lo que facilita el control de versiones y la gestión de estos movimientos.

## Git blame

El comando ```git blame <nb-archivo>``` se utiliza para mostrar quien es el responsable de cada línea de un archivo en el historial de proyectos. Es una herramienta útil para rastrear la autoría de cambios específicos en el código y entender quién hizo qué y por qué, en una línea de tiempo detallada.

## Git grep

El comando ```git grep <patrón-de-búsqueda>``` se utiliza para buscar texto dentro de los archivos de un repositorio. Es una herramienta poderosa que permite realizar búsquedas rápidas y eficientes de patrones específicos dentro del código fuente o en cualquier archivo del proyecto. A diferencia de herramientas de búsqueda tradicionales, git grep se ejecuta dentro del contexto de un repositorio Git, lo que lo hace especialmente útil para proyectos versionados.
- ```git grep <patrón-de-búsqueda> <nb-rama>``` se realiza la búsqueda sobre una rama en concreto.
- ```git grep <patrón-de-búsqueda> <commit-id>``` se realiza la búsqueda sobre los archivos asociados a ese commit.
- ```git grep <patrón-de-búsqueda> -- <directorio>``` se realiza la búsqueda sobre un directorio.
- ```git grep -l <patrón-de-búsqueda>``` muestra el número de líneas que cumplen el patrón en cada fichero.
- ```git grep -i <patrón-de-búsqueda>``` realiza una búsqueda insensible a mayusculas.
- ```git grep -n <patrón-de-búsqueda> ``` muestra la línea donde se cumple la coincidencia.
- ```git grep <patrón-de-búsqueda> --no-index``` para realizar una búsqueda incluyendo los ficheros no versionados.

## Git alias

El comando git alias no es un comando oficial de Git en sí mismo, pero Git permite crear alias personalizados para los comandos más utilizados, lo que hace más fácil y rápido ejecutar tareas repetitivas. Un alias en Git es simplemente un nombre corto para un comando o una combinación de comandos, de modo que puedas escribir menos y realizar la misma operación.
Git tiene un sistema para crear alias usando la configuración global o local del repositorio. Los alias se definen en el archivo de configuración de Git (.gitconfig), y puedes agregarlos de manera manual o mediante el comando git config. La forma más común de crear alias es mediante el comando git config. Aquí se muestra la sintaxis básica para crear un alias: ```git config --global alias.<alias> "<comando>"```
- --global: Indica que el alias será global (es decir, estará disponible en todos los repositorios en tu máquina). Si quieres que sea solo para un repositorio específico, omite esta opción.
- <alias>: Es el nombre corto que deseas darle al alias.
- <comando>: Es el comando real que se ejecutará cuando uses el alias.

## Git reset

El comando ```git reset``` es uno de los comandos más poderosos de git, ya que se utiliza para deshacer cambios en tu repositorio y modificar el historial de commits. Dependiendo de cómo se utilice, puede afectar a tu ara de trabajo, índice etc. La principal función es mover el puntero de la rama actual a un commit anterior o a una referencia dependiendo de las opciones que utilices.
- ```git reset --soft``` mueve el puntero de la rama actual al commit especificado, pero no cambia el índice (área de staging) ni el directorio de trabajo. Los archivos modificados siguen en el área de staging listos para ser commitados.
- ```git reset --mixed``` (predeterminado) mueve el puntero de la rama actual al commit especificado y deshace los cambios en el índice (staging area), pero mantiene los archivos en el directorio de trabajo.
- ```git reset --hard``` mueve el puntero de la rama al commit especificado y deshace tanto el índice como los cambios en el directorio de trabajo.

## Git revert

El comando ```git revert <commit-id>``` permite crear un nuevo commit que deshace los cambios de un commit anterior
- ```git revert <commit-id>``` commit que deseas revertir.
- ```git revert --no-edit``` realiza la acción de revertir el commit pero sin mostrar la consola para modificar el mensaje del commit.
- ```git revert --continue``` se aplica cuando se detecta que existen conflictos a la hora de revertir los cambios (estos se deben de resolver de manera manual).
- ```git revert --abort``` se aplica cuando los conflictos detectados son demasiados y quieres cancelar el proceso.
- ```git revert --edit``` comportamiento por defecto, abre el editor para modificar el mensaje del commit.
- ```git revert -n``` o ```git revert --no-commit``` no crea le comit automáticamente, solo prepara el área de trabajo para que puedas revisar los cambios antes de hacer el commit.

## Git restore

El comando ```git restore``` fue introduccio en Git 2.2.3 para simplificar y externalizar algunas funciones que realizaba el comando ```git checkout```, el principal objetivo es retaurta el contenido de un archivo a partir de su último commit. ```git restore``` no solo puede restaurar el contenido de un documento con el valor del último commit sino que puede realizar las siguientes operativas tambien
- Restaurar el contenido de un documento de un commit especifico.
- ```git restore .``` restaurar el contenido de todos los documentos modificados.
- ```git resotre --staged <archivo>``` o ```git restore --staged .``` restaurar archivos del area de preparación (unstage).
- ```git resotre --source=<nombre-de-rama> <archivo>``` restaurar un archivo desde un branch especifico.
- ```git restore --source=<commit-id> --force``` restaurar un archivo sin necesidad de confirmacion. 

## Git amend

El comando ```git commit --amend``` (comúnmente referido como ```git amend```) se utiliza para modificar el ultimo commit en tu rama. Permite realizar cambios, ya sea para modificar el mensaje, agregar archivos que olvidaste añadir o incluso corregir cambios que podrían no haber sido correctos. 
- ```git commit --amend``` nos permite modificar el mensaje del último commit. Esto directamente abrira el editor de texto configurado en tu Git (Vim o nano)
- ```git commit --amend``` tras agregar documentos (```git add```) agregar estos documentos al último commit registrado y te permitirá editar el mensaje, en caso de no actualizarlo se quedará el que estaba
- ```git commit --amend --no-edit``` agregará documentos y omitirá el paso de modificar el mensaje del commit
- ```git commit --amend --reset-author``` permite modificar el autor del último commit utilizando el usuario que tienes configurado en tu git

## Git cherry-pick

El comando ```Git cherry-pick <commit-id>``` nos permite aplicar commits de otras ramas en nuestra rama de trabajo, esto es útil si solo necesitamos ciertos cambios de una rama y no queremos hacer un merge completo.
Al ejecutar el comando no se encuentran conflictos, se realiza una integración simple y exitosa.
En caso de encontrase conflictos, se deben de resolver manualmente, agregarlos (```git add```) y posteriormente ejecutar ```git cherry-pick --continue```, pero en caso de querer abortar este proceso usaremos
```git cherry-pick --abort```

## Git rebase

El comando ```git rebase <nb-rama>``` se utiliza para integrar cambios de una rama a otra de manera diferente a como lo hace git merge. En lugar de crear un nuevo "commit de fusión" como lo hace git merge, mueve o reaplica los commits de una rama sobre otra, lo que puede resultar en un historial de commits más limpio y lineal.
- ```git rebase -i``` El rebase interactivo te permite modificar el historial de commits antes de realizar el rebase. Puedes reordenar, combinar (squash), modificar, eliminar o dividir commits. Es útil para limpiar el historial de commits antes de integrarlo a una rama principal.
Esto abrirá una interfaz de texto que te permitirá editar los últimos 3 commits. Desde ahí puedes elegir acciones como:
  - pick: Mantener el commit tal cual.
  - reword: Cambiar el mensaje del commit.
  - edit: Modificar el commit.
  - squash: Combinar commits.
  - drop: Eliminar un commit.
- ```git rebase --onto <nueva-base> <id-commit-antiguo> <rama>``` te permite mover un conjunto de commits de una rama a otra, especificando un rango de commits más complejo.

## Git stash

El comando ```git stash``` es una herramienta muy útil en Git que no spermite guardar temporalmente cambios no confirmados en tu área de trabajo (tanto en el area de preparación como en el directorio de trabajo)
Existen dos formas de guardar la información en el stash
- ```git stash``` sin parámetros almacena la información en el directorio de trabajo y en el area de preparacion.
- ```git stash -k``` o ```git stash --keep-index``` se almacena la información solamente en el directorio de trabajo.
- ```git stash save "mensaje descriptivo"``` permite agregar mensajes para poder localizarlos más fácilmente.
- ```git stash list``` para listar todos los stash almacenados.
- ```git stash show -p sthas@{n}``` para obtener la información detallada de un stash.
- ```git stash apply stash@{n}``` para recuperar los cambios de un stash.
- ```git stash pop``` para confirmar que se van a implementar esos cambios guardados y eliminarlo posteriormente de los stash almacenados.
- ```git stash drop stash@{0}``` para eliminar un stash.
- ```git stash clear``` para eliminar todos los stash almacenados.
- ```git stash -u o git stash --include-untracked``` crea un stash con todos los documentos modificados y todos los documentos/directorios no versionados (untracked).
- ```git stash branch <nombre-de-rama>``` crea una nueva rama a partir del commit actual y aplica el stash allí.

## Git reflog

El comando ```git reflog``` muestra un registro de los cambios más recientes en tu referencia HEAD (y otras referencias). 
En este registro podemos obtener:
-  Información de los cambios en el puntero HEAD.
-  Recuperación de commits perdidos, si se ha realizado algun git reset --hard o cualquier acción que borre referencias a commits.
-  Cambios en las ramas, se han realizado operaciones de merge, rebase, o checkout de ramas.
-  Rastrear referencias de ramas, si una referencia de rama se ha movido se podrá ver donde cuando y como ocurrió.

Podemos personalizar la salida que nos muestra este comando, por ejemplo limitando el número de registros mostrados por pantalla o buscando las acciones realizadas sobre una fecha
```git reflog -n 5``` o ```git reflog --date=relative```

Ejecucion del comando
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

El comando ```git branch``` se utiliza para la gestión de ramas dentro de un repositorio.
- ```git branch``` lista todas las ramas locales del repositorio (aquellas en la que aparezca el * indica que es la rama en la que estas posicionado actualmente).
- ```git branch <nb-rama>``` permite crear una rama (pero no cambia a ella).
- ```git branch -d <nb-rama>``` elimina una rama local (la opción -d sirve para eliminar de forma segura).
- ```git branch -m <new-nb-rama>``` modifica el nombre de la rama en la que estas.
- ```git branch -r``` lista las ramas del repositorio remoto.
- ```git branch -a``` lista todas las ramas disponibles tanto locales como remotas.

## Git switch

El comando ```git switch <nb-de-la-rama>``` es un nuevo comando insertado en Git que nos permite cambiar entre las múltiples ramas disponibles en nuestro repositorio.
- ```git switch -c <nb-de-la-rama>``` nos permite crear una nueva rama y cambiar a ella de manera automática.

## Git tag

El comando ```git tag <nb-del-tag>``` se utiliza para crear etiquetas (tags) en puntos específicos de la historia de un repositorio. Las etiquetas permiten marcar versiones importantes del proyecto, como lanzamientos de software (releases), hitos del proyecto, o cualquier otro momento relevante que quieras identificar.
Por defecto, las etiquetas no se envían al repositorio remoto al hacer un git push.
- ```git tag -a <version> -m <msg del tag>``` creamos un tag
- ```git tag -d <nb-del-tag>``` elimina el tag.
- ```git push --delete origin <nb-del-tag>``` eliminamos el tag del repositorio remoto.
- ```git push origin <nb-del-tag>``` enviamos al repositorio remoto un tag.
- ```git push --tags``` enviamos todos los tags al repositorio remoto.

Existen do tipos principales de etiquetas:
- Etiquetas Ligeras: Son simplemente un marcador (un puntero) a un commit específico. No contienen más información que la referencia al commit al que apuntan. (v1.0)
- Etiquetas anotadas: Son más completas y contienen más información, como el nombre del autor, la fecha y un mensaje de etiqueta. Estas etiquetas se almacenan como objetos completos en la base de datos de Git, lo que las hace más útiles para el seguimiento de versiones, ya que puedes añadir detalles sobre el propósito de la etiqueta.

## Git merge

El comando ```git merge <nombre-de-la-rama-a-fusionar>``` se utiliza para combinar cambios de diferentes ramas dentro de un repositorio Git.
Existen varios tipos de fusión que pueden ocurrir al usar este comando, dependiendo de las circunstancias de las ramas y cambios realizados en ellas.

### Fast-Forward Merge (fusión rápida)

Este tipo de merge ocurre cuando la rama de destino no tiene ningún cambio desde el punto en el que se separó de la rama que se está fusionando. En otras palabras, si la rama principal (por ejemplo, main) no tiene cambios nuevos desde que se creó la rama que quieres fusionar, Git simplemente mueve el puntero de la rama hacia adelante al punto de la otra rama. No se crea un commit de merge porque no hay conflicto.
Resultado: No se crea un commit de merge, solo un avance en la referencia de la rama.

### Merge con Commit de Fusión (Merge Commit)

Este tipo de merge se realiza cuando ambas ramas (la rama de destino y la rama que se va a fusionar) tienen cambios que no están presentes en la otra. Git no puede avanzar simplemente el puntero de la rama de destino, por lo que crea un commit de fusión. Este commit refleja la fusión de los cambios de ambas ramas.
Resultado: Git crea un commit especial llamado commit de fusión, que tiene dos padres: uno de la rama de destino (por ejemplo, main) y otro de la rama fusionada (por ejemplo, feature).

### Merge con Conflictos

Los conflictos ocurren cuando los cambios realizados en ambas ramas afectan la misma parte del código de manera incompatible. En este caso, Git no puede resolver automáticamente los conflictos y te pedirá que los resuelvas manualmente. Después de resolver los conflictos, deberás agregar los archivos modificados a la zona de preparación (staging area) y luego hacer un commit para completar el merge.

### Squash Merge (Fusión en un solo commit)

Aunque el comando git merge por sí mismo no realiza una "fusión squash", Git permite una fusión squash mediante la opción --squash ```git merge --squash <nombre-de-la-rama>```. Esta opción toma todos los commits de una rama y los combina en un solo commit cuando se fusiona con la rama de destino. Esto es útil cuando se desea tener un historial de commits más limpio.

# Comandos de comparación

## Git show

El comando ```git show <commit-id>``` se utiliza para mostrar información detallada sobre un objeto específico del repositorio, como un commit, una etiqueta (tag) o un archivo. Generalmente, se usa para ver detalles de un commit reciente o de cualquier otro objeto que tenga un identificador, como su hash.

## Git diff

El comando ```git diff``` es una herramienta fundamental de Git que muestra las diferencias entre dos estados del repositorio. Estas diferencias pueden referirse a los cambios realizados en los archivos, entre ramas, entre commits, entre el área de staging y el directorio de trabajo, etc.
- ```git diff``` Muestra las diferencias entre el directorio de trabajo (los cambios realizados en los archivos) y el staging area (el área de preparación para el próximo commit).
- ```git diff --staged``` Mostrar los cambios que se han añadido al área de staging.
- ```git diff <commit-id> <commit-id>``` Puedes ver las diferencias entre dos commits específicos.
- ```git diff <nb-branch> <nb-branch>``` para comparar los cambios entre dos ramas.
- ```git diff <archivo>``` ver las diferencias de un archivo específico.

## Git shortlog

El comando ```git shortlog``` es útil para ver un resumen de los commits realizados en un repositorio, agrupados por autor. A diferencia de ```git log```, que muestra un historial detallado de todos los commits, ```git shortlog``` proporciona un resumen más condensado y fácil de leer, especialmente útil para ver contribuciones por cada autor.
- ```git shortlog -n``` ordena los resultados de acuerdo al número de commits realizados para cada autor (de mayor a menor).
- ```git shortlog --since="fecha(yyyy-MM-dd)" --until="fecha(yyyy-MM-dd)"``` filtrar los commits en un rango de fechas específico.
- ```git shortlog --summary --numbered``` obtiene el total de commits agrupados por usuario.
- ```git shortlog -s``` ver solo el número de commits de cada autor, sin los detalles de los mensajes.
- ```git shortlog -e``` agrupa los commits por correo electrónico.
- ```git shortlog -c``` para agruparlo por fecha en lugar de por autor.
- ```git shortlog -w``` omite aquellos cambios en los espacios en blanco (útil para ver un resumen de las contribuciones sin distracciones por cambios de formato).

## Git describe

El comando ```git describe``` es utilizado para obtener una etiqueta descriptiva (o "nombre de referencia") asociada al commit actual o a un commit específico. Este comando es útil cuando quieres una forma más amigable y legible de identificar un commit que no solo involucra un hash largo, sino una referencia más comprensible basada en las etiquetas del repositorio.
