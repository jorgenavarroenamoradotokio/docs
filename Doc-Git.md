<div align="center">
  <img src="https://raw.githubusercontent.com/jorgenavarroenamoradotokio/docs/feature/git/logos/Git-Logo.svg">
</div>

## Índice
- [Intoduccion](#intoduccion)
  - [Caracteristicas](#caracteristicas)
  - [Conceptos basicos](#conceptos-basicos)
- [Fucnionamiento](#fucnionamiento)
- [Proceso de confirmacion de cambios](#proceso-de-confirmacion-de-cambios)

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

# Proceso de confirmacion de cambios

Git organiza el proceso de guardado de cambios en tres estados clave, que ayudan a controlar y preparar las modificaciones antes de hacer un guardado definitivo (llamado commit). Estos tres estados son:

- Directorio de trabajo (Modified)
En este estado, los archivos del proyecto han sido editados, pero Git aún no ha preparado estos cambios para ser guardados. Es decir, has realizado cambios en el contenido, pero aún no están listos para formar parte del historial del proyecto.

- Preparado (Staged)
Cuando los archivos están en el estado "Preparado", significa que has marcado ciertos cambios como listos para ser guardados en el próximo commit. En esta etapa, Git ya sabe exactamente qué cambios específicos se incluirán en el próximo guardado, permitiendo un control sobre qué modificaciones se guardarán y cuáles no.

- Guardado (Committed)
En el estado "Guardado", los cambios ya están registrados permanentemente en el historial del proyecto. Esto crea una versión nueva del proyecto, permitiendo a Git almacenar esa "instantánea" del proyecto, que se puede revisar o restaurar en el futuro.

