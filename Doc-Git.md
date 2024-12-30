<div align="center">
  <img src="https://raw.githubusercontent.com/jorgenavarroenamoradotokio/docs/feature/git/logos/Git-Logo.svg">
</div>

## Índice
- [Intoduccion](#intoduccion)
  - [Caracteristicas](#caracteristicas)
  - [Conceptos basicos](#conceptos-basicos)
- [Fucnionamiento](#fucnionamiento)
- [Ciclo de vida de los archivos en git](#ciclo-de-vida-de-los-archivos-en-git)
- [Configuracion en Git](#configuracion-en-git)
- [Comando de ayuda](#comando-de-ayuda)
- [Comandos basicos](#comandos-basicos)
  - [Git init](#git-init)
  - [Git add](#git-add)
  - [Git status](#git-status)
  - [Git commit](#git-commit)
  - [Git log](#git-log)
- [Comandos basicos para repositorios remotos](#comandos-basicos-para-repositorios-remotos)
  - [Git clone](#git-clone)
  - [Git remote](#git-remote)
  - [Git push](#git-push)
  - [Git pull](#git-pull)
- [Comandos de reparación](#comandos-de-reparación)
  - [Git Clean](#git-clean)
  - [Git Checkout](#git-checkout)
  - [Git restore](#git-restore)
  - [Git cherry-pick](#git-cherry-pick)
  - [Git stash](#git-stash)
  - [Git reflog](#git-reflog)
- [Comandos de Ramas y Merge](#comandos-de-ramas-y-merge)
- [Comandos de comparación](#comandos-de-comparación)

# Intoduccion

Git es un sistema de control de versiones distribuidas, diseñado para gestionar el desarrollo de proyectos de software de forma colaborativa y eficiente. Fue creado por Linus Torvalds en 2005, y su propósito principal es permitir que los desarrolladores realicen un seguimiento de los cambios en el código fuente de un proyecto, facilitando la colaboración, la organización y la prevención de errores o conflictos entre versiones.

## Caracteristicas

- Distribuido : A diferencia de otros sistemas de control de versiones, en Git cada desarrollador tiene una copia completa del historial de cambios del proyecto en su máquina local. Esto permite trabajar offline y compartir cambios sin un servidor central, aunque también es compatible con repositorios centralizados.
- Rastreo de versiones : Git guarda una "instantánea" de cada cambio realizado en los archivos de un proyecto. Esto permite revertir cambios, comparar versiones anteriores y saber quién hizo cada cambio y cuándo.
- Branching (ramas) : Git permite trabajar en diferentes "ramas" o versiones paralelas del proyecto. Esto facilita que los equipos desarrollen nuevas funcionalidades o correcciones de errores sin afectar el código principal (por lo general, en la rama maino master). Una vez que se finaliza una funcionalidad, esta puede estar integrada de nuevo en la rama principal.
- Integración y resolución de conflictos : Git permite combinar el trabajo de diferentes personas, y proporciona herramientas para resolver conflictos cuando dos personas modifican el mismo código.

## Conceptos basicos

- Repositorio (repo) : Es el lugar donde se almacena el proyecto, junto con su historial de cambios.
- Commit : Es una "captura" de los cambios realizados en el proyecto en un momento específico.
- Branch (rama) : Una línea de desarrollo que permite trabajar en paralelo en el proyecto.
- Fusionar : Combinar cambios de una rama en otra.
- Push/Pull : Envío (push) o recepción (pull) de cambios entre el repositorio local y uno remoto.

# Fucnionamiento

El principal funcionamiento de git esta badado en capturar "versiones" de documentos cada vez que el susario realiza cambios y los guarda. Esto facilita el seguimiento de cada modificacion, permite regresar a versiones anteriores y colaborar en proyectos de equipo al manterner un historial clao de todo lo que se ha realizado sobre uno o varios documentos.

Cada vez que se guardan cambios en Git, este crea una "instantánea" de los archivos en su estado actual. Esta instantánea funciona como una foto del proyecto en ese momento, almacenando detalles específicos sobre cómo están organizados los archivos, su contenido y cualquier modificación realizada. Con esta estructura, Git guarda solo las diferencias entre cada versión para no ocupar espacio innecesario, mientras sigue permitiendo reconstruir cada estado pasado del proyecto.

Git organiza estas "instantáneas" en un historial de cambios que registra cada versión del proyecto en el orden en que se hicieron. Cada entrada en el historial contiene información como quién realizó el cambio, cuándo ocurrió y un pequeño mensaje que describe el cambio realizado. Esto crea un registro cronológico completo del desarrollo del proyecto, haciendo posible revisar el proceso de cambios desde el inicio y entender la evolución del proyecto.

# Ciclo de vida de los archivos en git

Git organiza el proceso de guardado de cambios en tres estados clave, que ayudan a controlar y preparar las modificaciones antes de hacer un guardado definitivo (llamado commit). Estos tres estados son:

- Directorio de trabajo (Modified)
En este estado, los archivos del proyecto han sido editados, pero Git aún no ha preparado estos cambios para ser guardados. Es decir, has realizado cambios en el contenido, pero aún no están listos para formar parte del historial del proyecto.

- Preparado (Staged)
Cuando los archivos están en el estado "Preparado", significa que has marcado ciertos cambios como listos para ser guardados en el próximo commit. En esta etapa, Git ya sabe exactamente qué cambios específicos se incluirán en el próximo guardado, permitiendo un control sobre qué modificaciones se guardarán y cuáles no.

- Guardado (Committed)
En el estado "Guardado", los cambios ya están registrados permanentemente en el historial del proyecto. Esto crea una versión nueva del proyecto, permitiendo a Git almacenar esa "instantánea" del proyecto, que se puede revisar o restaurar en el futuro.

# Configuracion en Git

Configurar Git es uno de los primeros pasos para empezar a trabajar. A traves de comando git config podemos deefinir nuestras peferencias, establecer tu identidad, crear alias, etc

Existen tres niveles de configuracion:
- Global (```--global```): Configura opciones que se aplican a todos los repositorios del usuario
- Local: Las configiuraciones locales afectan solo al repositorio en el que estas trabajando
- Sistema (```--system```): Aplica configuiraciones a todos los usuarios en el sistema, requiere permisos de administrador

Confiugurar el usuario que lo utiliza: Esto es esencial, ya que Git registra el nombre y el correo electrónico del autor en cada confirmación. Así, otros colaboradores sabrán quién realizó cada cambio. Usa los siguientes comandos para definir tu identidad global (afecta a todos los repositorios en tu sistema) o específico para un proyecto
```cmd 
git config --global user.name "Tu Nombre"
git config --global user.email "tu.email@example.com"
```
Para consultar toda la configuracion que tenemos usaremos el comando ```git config --list```

# Comando de ayuda

Git tiene integrada toda la documentacion del funcionamiento de los multiples comandos que lo componen, para poder consultar la wiki usaremos el comando ```git help```

# Comandos basicos

Git ofrece una serie de comandos esenciales para gestionar el control de versiones en proyectos de desarrollo. Estos comandos basicos te permiten iniciar y gestionar repositorios, registrar cambiso en el codigo, ver el hiotorial y colaborar con otros.

## Git init

El comando ```git init``` inia un nuevo repositorio en girt en el directorio local. Crea un repositorio vacio donde puedes empezar a registrar el historial de cambios. 

Al ejecutar este comando automaticamente crea una carpeta oculta con nombre ```.git```. Esta carpeta contiene toda la información que Git necesita para gestionar y almacenar el historial de versiones del proyecto, de manera que se puedan rastrear, revertir y fusionar cambios a lo largo del tiempo.

-  HEAD
Es un archivo que apunta a la rama actual en la que se está trabajando. HEADpermite a Git saber en qué parte del historial se encuentra el trabajo actual y qué rama debe actualizar al hacer commits.

-  config
Archivo de configuración específico para el repositorio. Aquí se almacenan configuraciones locales del proyecto, como las remotas (URL de repositorios), opciones específicas y preferencias de usuario para el repositorio en cuestión.

-  index
También conocido como el "staging area" o área de preparación, este archivo contiene una lista de archivos preparados para la próxima confirmación. Aquí es donde Git guarda la información de los cambios antes de confirmarlos en el historial.

-  objects
Este directorio almacena todos los objetos de Git, como commits, árboles (estructura de carpetas y archivos) y blobs (contenido de los archivos). Cada objeto se almacena usando un identificador único (SHA-1 hash), lo que garantiza la integridad y permite la compresión de datos.

-  refs
Este directorio contiene referencias a las ramas y etiquetas del repositorio. Dentro de refs/headsestán las referencias a cada rama, y ​​en refs/tagsse guardan las etiquetas de las versiones marcadas del proyecto.

-  logs
Almacena un historial de las actualizaciones de cada referencia (por ejemplo, cambios en HEADy en las ramas). Esto permite registrar y deshacer cambios en las ramas.

-  hooks
Contiene scripts que Git ejecuta automáticamente en ciertos eventos (como pre-commit, post-commit, pre-push, etc.). Estos scripts son útiles para automatizar tareas como validaciones de código, pruebas automáticas, o notificaciones antes o después de realizar ciertas acciones.

-  info
Almacena archivos de información adicional sobre el repositorio. Aquí se encuentra el archivo exclude, que permite especificar patrones de archivos para ignorar sin añadirlos al archivo .gitignore.

## Git add

El comando ```git clone <URL-del-repositorio>``` agrega archivos al área de preparación (staging area), es decir, marca los archivos que quieres incluir en el próximo commit. Se puede agregar un solo archivo o todos los archivos modificados.

```
git add nombre_del_archivo    # Para un archivo específico
git add .                      # Para todos los archivos modificados
```

## Git status

El comando ```git status``` muestra el estado de los archivos en el repositorio. Este comando te dice si hay cambios que no están preparados, qué archivos están listos para el commit y cuáles no están versionados.

```
git status
```

## Git commit

El comando ```git commit``` guarda una “instantánea” de los cambios en el repositorio. Un commit es un paso en el historial del proyecto y debe ir acompañado de un mensaje que describa los cambios.

Para realizar el commit de una manera mas sencilla solo indicando el titulo del commit usaremos la opcion -m

```
git commit -m "Mensaje que describe los cambios"
```

## Git log

El comando ```git log``` permite ver el historial de commits del repositorio, mostrando detalles de cada commit como el autor, la fecha y el mensaje asociado.

```
git log
```

# Comandos basicos para repositorios remotos

## Git clone

El comando ```git clone <URL-del-repositorio>``` permite copiar un repositorio existente, como uno que esté en GitHub o GitLab, a tu equipo local. Esto es especialmente útil para trabajar en proyectos colaborativos.

## Git remote

El comando ```git remote``` permite gestionar las conexiones a los repositorios remotos en Git.
- Para añadir un nuevo repositorio remoto usaremos ```git remote add nombre_remoto URL_del_repositorio```
- Para consultar las urls que tenemos asignadas (fetch y push) al repositorio usaremos ```git remote -v``` 
- Para agregar eliminar una usaremos ```git remote remove nombre_remoto```
- Para modificar una usamremos ```git remote set-url nombre_remoto nueva_URL```

## Git push

El comando ```git push``` nos permite enviar los commits locales al repositorio remoto, haciendo que los cambios sean accesibles para otros colaboradores.

## Git pull

El comando ```git pull``` permite traernos los cambios del repositorio remoto al repositorio local, permitiendo actualizar el código local con los últimos cambios del proyecto.

# Comandos de reparación

## Git Clean

El comando ```git clean``` permite eliminar archivos no rastreados (untracked) y directorios del repositorio. Debemos de tener en cuenta que este comando es potencialmente destructivo porque puede eliminar archivos importantes que no se han añadido al control de versiones. Por esta razón, Git requiere que utilice se utilice la opciones -f(force) para eliminar solo ficheros.
No solo podemos eliminar los documentos que no este rastreados sino podemos obtener el listado de documentos que son afectados si ejecutamos el comando ```git clean -f``` para ellos usaremos ```git clean -n```

## Git Checkout

El comando ```git checkout <commit-id> -- <archivo-o-directorio>``` permite restaurar el contenido de un archivo o directorios desde la ultima confirmación (commit) o desde un commit anterior.
Acutalmente este comando esta en desuso y se remplazo por ```git restore```

## Git restore

El comando ```git restore``` fue introduccio en Git 2.2.3 para simplificar y externalizar algunas funciones que realizaba el comando ```git checkout```, el principal objetivo es retaurta el contenido de un archivo a partir de su ultimo commit. ```git restore``` no solo puede restaurar el contenido de un documento con el valor del ultimo commit sino que puede realizar las siguientes operativas tambien
- Restaurar el contenido de un documento de un commit especifico
- Restaurar el contenido de todos los documentos modificados ```git restore .```
- Restaurar archivos del area de preparación (unstage) ```git resotre --staged <archivo>``` o ```git restore --staged .```
- Restaurar un archivo desde un branch especifico ````git resotre --source=<nombre-de-rama> <archivo>```
- Restaurar un archivo sin necesidad de confirmacion ```git restore --source=<commit-id> --force```

## Git amend

## Git cherry-pick

El comando ```Git cherry-pick <commit-id>``` nos permite aplicar commits de otras ramas en nuestra rama de trabajo, esto es util si solo necesitamos ciertos cambios de una rama y no queremos hacer un merge completo.
Al ejecutar el comando no se encuentran conflictos, se realiza una integracion simple y exitosa.
En caso de encontrase conflictos, se deben de resolver manualmente, agregarlos (```git add```) y posteriormente ejecutar ```git cherry-pick --continue```, pero en caso de querer abortar este proceso usaremos
```git cherry-pick --abort```


## Git stash

El comando ````git stash``` es una herramienta muy útil en Git que no spermite guardar temporalmente cambios no confirmados en tu área de trabajo (tanto en el area de preparación  como en el directorio de trabajo)
Existen dos formas de guardar la informacion en el stash
- ```git stash``` sin parametros almacena la informacion en el directorio de trabajo y en el area de preparacion
- ```git stash -k``` o ```git stash --keep-index``` se almacena la informacion solamente en el directorio de trabajo
```git stash save "mensaje descriptivo"``` permite  agregar mensajes para poder localizarlos mas facilmente
```git stash list``` para listar todos los stash almacenados
```git stash show -p sthas@{n}``` para obtener la informacion detallada de un stash
```git stash apply stash@{n}``` para recuperar los cambios de un stash
```git stash pop``` para confirmar que se van a implementar esos cambios guardados y eliminarlo postermiormente de los stash almacenados
```git stash drop stash@{0}``` para eliminar un stash
```git stash clear``` para eliminar todos los stash almacenados
```git stash -u o git stash --include-untracked``` crea un stash con todos los documentos modificados y todos los documentos/directorios no versionados (untracked)
```git stash branch <nombre-de-rama>``` crea una nueva rama a partir del commit actual y aplica el stash allí.

## Git reflog

El comando ```git reflog``` muestra un registro de los cambios mas recientes en tu referencia HEAD (y otrras referencias). 
En este registro podemos obtener:
-  informacion de los cambios en el puntero HEAD
-  recuperacion de commits perdidos, si se ha realizado algun git reset --hard o cualquier accion que borre referencias a commits
-  cambios en las ramas, se se han realizado operaciones de merge, rebase, o checkout de ramas
-  rastrear referencias de ramas, si una referencia de rama se ha movido se podra ver donde cuando y como ocurrió.

Podemos personalizar la salida que nos muestra este comando, por ejemplo limitando el numero de registros mostrados por pantalla o buscando las acciones realizadas sobre una fecha
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

# Comandos de comparación
