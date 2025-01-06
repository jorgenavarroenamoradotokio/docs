<div align="center">
  <img src="https://raw.githubusercontent.com/jorgenavarroenamoradotokio/docs/feature/git/logos/Git-Logo.svg">
</div>

## Índice
- [Introducción](#introducción)
  - [Arquitectura](#arquitectura)
  - [Modelo de base de datos en memoria (In-memory) y persistencia](#modelo-de-base-de-datos-en-memoria-in-memory-y-persistencia)
- [Instalacción](#instalacción)
  - [Sistemas Linux (Ubuntu/Debian)](#sistemas-linux-ubuntudebian)
  - [Sistemas Linux (CentOS)](#sistemas-linux-centos)
  - [MacOs](#macos)
  - [Windows](#windows)
  - [Docker](#docker)
- [Modelado de datos en Redis](#modelado-de-datos-en-redis)
  - [Claves](#claves)
    - [Namespaces](#namespaces)
    - [Uso de Separadores Consistentes](#uso-de-separadores-consistentes)
    - [Evitar el Uso de Claves Demasiado Largas](#evitar-el-uso-de-claves-demasiado-largas)
    - [Usar Claves Específicas y Descriptivas](#usar-claves-específicas-y-descriptivas)
    - [Considerar la Expiración de Claves](#considerar-la-expiración-de-claves)
    - [Incluir Versiones o Prefijos de Aplicación si es Necesario](#incluir-versiones-o-prefijos-de-aplicación-si-es-necesario)
    - [Evitar el Uso de Caracteres Especiales Innecesarios](#evitar-el-uso-de-caracteres-especiales-innecesarios)
    - [Evitar el Uso de Claves Estáticas con Valores Constantes](#evitar-el-uso-de-claves-estáticas-con-valores-constantes)
    - [Uso de Claves para Indicar Estado de Procesos](#uso-de-claves-para-indicar-estado-de-procesos)
    - [Claves para Eventos Temporales](#claves-para-eventos-temporales)
  - [Valores](#valores)
    - [String](#string)
    - [Hashes](#hashes)
    - [List](#list)
    - [Sets y Sorted Sets](#sets-y-sorted-sets)
    - [Bitmaps](#bitmaps)
    - [HyperLogLog](#hyperloglog)
    - [Streams](#streams)
    - [Geolocalización](#geolocalización)
- [Sistema de lectura y escritura](#sistema-de-lectura-y-escritura)
  - [Escritura](#escritura)
    - [Sobrescritura](#sobrescritura)
    - [Lectura](#lectura)
- [Configuracion](#configuracion)
  - [Configuracion avanzada](#configuracion-avanzada)
  - [Configuracion de seguridad](#configuracion-de-seguridad)
- [Despliegue  en entornos cloud y on-premises](#despliegue--en-entornos-cloud-y-on-premises)
- [Patros de arquitectura](#patros-de-arquitectura)
  - [Caching](#caching)
  - [Session](#session)
  - [Pub/Sub](#pubsub)
  - [Task Queses](#task-queses)
  - [Rate Limiting](#rate-limiting)
  - [Distributed Locks](#distributed-locks)
  - [Geospatial Data](#geospatial-data)
- [Escalabilidad y alta disponibilidad](#escalabilidad-y-alta-disponibilidad)
- [Optimización](#optimización)
- [Mantenimiento y resolucion](#mantenimiento-y-resolucion)
- [Pruebas](#pruebas)
- [Comandos](#comandos)
  - [Comandos Generales](#comandos-generales)
  - [Comandos de Claves](#comandos-de-claves)
  - [Comandos de Strings](#comandos-de-strings)
  - [Comandos de Hashes](#comandos-de-hashes)
  - [Comandos de Listas](#comandos-de-listas)
  - [Comandos de Conjuntos (Sets)](#comandos-de-conjuntos-sets)
  - [Comandos de Conjuntos Ordenados (Sorted Sets)](#comandos-de-conjuntos-ordenados-sorted-sets)
  - [Comandos de Bitmaps](#comandos-de-bitmaps)
  - [Comandos de Streams](#comandos-de-streams)
  - [Comandos de Pub/Sub](#comandos-de-pubsub)
  - [Comandos de Transacciones](#comandos-de-transacciones)
  - [Comandos de Cluster](#comandos-de-cluster)

# Introducción
Redis es una base de datos en memoria de código abierto, altamente eficiente, que se utiliza principalmente para almacenamiento y recuperación rápida de datos. Aunque se le conoce principalmente por su uso como sistema de cache, Redis ofrece una gama de funcionalidades avanzadas que lo convierten en una herramienta crucial en el desarrollo de aplicaciones modernas.

Redis no solo es una excelente opción para caching, sino que también se utiliza en una variedad de escenarios avanzados en aplicaciones modernas, gracias a su arquitectura eficiente y su capacidad para manejar grandes volúmenes de datos en tiempo real.
- Caching: Redis se utiliza ampliamente como sistema de cache para mejorar el rendimiento de las aplicaciones. Dado que Redis almacena datos en memoria, se puede acceder a ellos mucho más rápido que si se obtuvieran de una base de datos tradicional o de servicios externos. Redis es ideal para almacenar resultados de consultas complejas, datos de sesión de usuarios, y cualquier otra información que se pueda generar dinámicamente. Se puede emplear un enfoque de cacheado de datos por tiempo (TTL - Time to Live), donde los datos almacenados en cache se eliminan automáticamente después de un tiempo predefinido.
- Pub/Sub (Publicación/Suscripción): Redis también soporta el modelo de comunicación pub/sub, que permite a las aplicaciones intercambiar mensajes en tiempo real. En este patrón, los publicadores envían mensajes a canales, y los suscriptores reciben estos mensajes en tiempo real. Este modelo es útil en aplicaciones como chat en tiempo real, notificaciones push, sistemas de eventos, y monitoreo en vivo.
- Gestión de sesiones: Redis es comúnmente usado para almacenar y gestionar las sesiones de usuarios en aplicaciones web y móviles. Dado que es extremadamente rápido, puede manejar grandes volúmenes de sesiones simultáneas. Además, la persistencia opcional asegura que los datos de las sesiones se mantengan entre reinicios del servidor.
- Colas y tareas asíncronas: Redis ofrece estructuras de datos como listas, conjuntos ordenados y pilas que pueden usarse para implementar sistemas de cola. Las tareas y trabajos asíncronos, como el procesamiento de imágenes, el envío de correos electrónicos o el cálculo en segundo plano, se pueden gestionar eficientemente mediante estas estructuras. Redis puede actuar como un sistema de colas distribuido, permitiendo que diferentes instancias de aplicación procesen trabajos en paralelo.
- Contadores y métricas en tiempo real: Redis es muy eficiente en la gestión de contadores de alta velocidad, como aquellos utilizados para rastrear visitas a una página, "likes" en una publicación, o cualquier otro tipo de métrica en tiempo real. Utilizando estructuras de datos como contadores, bitmaps, o hyperloglogs, Redis es capaz de manejar una gran cantidad de operaciones de lectura y escritura de manera eficiente y con baja latencia.
- Geolocalización: Redis ofrece soporte para operaciones geoespaciales, lo que permite almacenar y consultar datos de ubicación (latitud y longitud). Esto es útil para aplicaciones que necesitan realizar búsquedas o filtrados geoespaciales, como encontrar los puntos de interés más cercanos a una ubicación específica.

## Arquitectura 
Redis es su modelo de arquitectura de un solo hilo (single-threaded). Esto significa que, aunque Redis puede manejar múltiples conexiones concurrentes, todas las operaciones (como la lectura, escritura y manipulación de datos) se procesan en un único hilo, utilizando un bucle de eventos (event loop).

El uso de un único hilo tiene varias implicaciones:
- Simplicidad en la concurrencia: Al ser single-threaded, Redis evita los problemas complejos asociados con la sincronización de hilos y los bloqueos. En lugar de crear múltiples hilos para manejar solicitudes concurrentes, Redis gestiona todas las operaciones mediante un solo hilo que ejecuta las operaciones en un ciclo continuo.
- Desempeño optimizado: Redis hace uso de un bucle de eventos, lo que le permite procesar operaciones de manera no bloqueante. Cuando Redis recibe una solicitud, la maneja de inmediato y, si la operación involucra tiempos de espera (por ejemplo, en una operación de red), Redis no se bloquea esperando una respuesta, sino que puede atender otras solicitudes mientras espera. Esto contribuye a una baja latencia y alto rendimiento, incluso con millones de solicitudes por segundo.
- Escalabilidad vertical: A pesar de ser single-threaded, Redis puede manejar una gran carga gracias a su eficiencia y diseño optimizado. Sin embargo, para escalar horizontalmente y aprovechar múltiples núcleos de CPU, Redis puede ser replicado y configurado en un entorno distribuido, como en un clúster de Redis.

## Modelo de base de datos en memoria (In-memory) y persistencia
Redis es una base de datos en memoria, lo que significa que los datos se almacenan y acceden directamente desde la RAM en lugar de un disco. Esta característica permite a Redis ofrecer una velocidad de acceso a datos extremadamente rápida, ya que las operaciones de lectura y escritura en memoria son mucho más rápidas que las que involucran acceso a disco. Sin embargo, Redis también ofrece opciones de persistencia para garantizar que los datos no se pierdan en caso de un fallo del sistema o reinicio

Existen diversos mecanismos principales de persistencia:
- RDB (Redis Database Snapshotting): Redis puede crear instantáneas periódicas de los datos almacenados en memoria y guardarlas en un archivo en disco. Esto ocurre en intervalos de tiempo configurables y permite una recuperación rápida de los datos después de un reinicio. RDB es adecuado cuando la consistencia de los datos no es crítica y se puede tolerar una pequeña pérdida de datos entre las instantáneas.
- AOF (Append Only File): En este modo, Redis guarda todas las operaciones que modifican la base de datos en un archivo de registro en disco. Cada vez que se realiza una operación, se agrega al final del archivo AOF. Este enfoque ofrece una mayor durabilidad, ya que permite una recuperación precisa de los datos en el caso de una caída del sistema. Sin embargo, las operaciones de escritura pueden ser más lentas en comparación con RDB debido a la escritura continua en disco.
- Persistencia combinada: Redis también puede configurarse para usar ambos mecanismos, RDB y AOF, proporcionando un equilibrio entre rendimiento y durabilidad. En este caso, RDB se usa para realizar instantáneas periódicas, mientras que AOF asegura que las operaciones se registren de manera continua.

# Instalacción
## Sistemas Linux (Ubuntu/Debian)
En sistemas basados en Linux, como Ubuntu o Debian, la instalación de Redis es bastante sencilla gracias a los paquetes precompilados disponibles en los repositorios oficiales.
```bash
sudo apt update # actualizamos el indice de paquetes
sudo apt install redis-server redis-tools # instalamos redis
sudo systemctl status redis # verificamos que redis esta corriendo
sudo systemctl enable redis # habilitamos redis para que se inice automaticamente
redis-cli # Entramos en la consola de redis
```

## Sistemas Linux (CentOS)
Para sistemas como CentOS, el proceso de instalación es similar al de Ubuntu/Debian pero utilizando el gestor de paquetes yum o dnf (dependiendo de la versión).

```bash
sudo yum install epel-release # actualizamos el indice de paquetes
sudo yum install redis # instalamos redis
sudo systemctl start redis # verificamos que redis esta corriendo

sudo systemctl enable redis # habilitamos redis para que se inice automaticamente
sudo systemctl status redis 
redis-cli # Entramos en la consola de redis
```

## MacOs
se puede instalar de manera fácil usando Homebrew, que es un gestor de paquetes popular en este sistema operativo.
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)" # Instalamos Homebre en caso de no tenerlo instalado
brew install redis # instalamos redis
redis-server # iniciamos redis
redis-cli # entramos en la consola de redis
```

## Windows 
No tiene soporte nativo en Windows, pero puedes instalarlo en una máquina con Windows, se debe de tener instalado en el equipo Windows Subsystem for Linux (WSL)
La forma más recomendada de instalar Redis en Windows es utilizando WSL (Windows Subsystem for Linux). Esto te permite ejecutar una distribución de Linux dentro de Windows, y luego puedes seguir los pasos típicos de instalación de Redis para Linux.

## Docker
Docker es una forma sencilla y eficiente de instalar Redis sin necesidad de preocuparse por las dependencias del sistema operativo.

```bash
docker run --name redis -p 6379:6379 -d redis # instalamos redis
docker exec -it redis redis-cli # nos conectamos a la consola de redis
```

# Modelado de datos en Redis
Redis es una base de datos en memoria de alto rendimiento que ofrece un conjunto diverso de estructuras de datos avanzadas. A diferencia de las bases de datos relacionales, que utilizan tablas y filas, Redis utiliza un modelo de datos basado en claves y valores, donde cada valor puede estar asociado a diferentes tipos de estructuras de datos. Esta flexibilidad permite a los desarrolladores elegir la estructura de datos que mejor se adapta a sus necesidades.

## Claves 
El manejo adecuado de las claves en Redis es fundamental para garantizar un rendimiento eficiente, evitar conflictos de nombres y mantener la coherencia en las aplicaciones. Dado que Redis no impone restricciones de nombres de claves, es importante seguir ciertos convenios y buenas prácticas al definirlas, especialmente cuando se trabaja en proyectos más grandes o colaborativos.

### Namespaces
Un espacio de nombres es una técnica para organizar las claves de manera que se eviten colisiones de nombres y se mejore la legibilidad de las mismas. El espacio de nombres se puede implementar mediante un prefijo que separa las claves relacionadas.
- Para claves relacionadas con usuarios: "user:{userId}:profile", "user:{userId}:settings".
- Para claves relacionadas con productos: "product:{productId}:details", "product:{productId}:stock".
- Para claves relacionadas con una sesión de usuario: "session:{sessionId}".

### Uso de Separadores Consistentes
Un buen separador mejora la legibilidad y organiza la jerarquía de las claves. El separador más comúnmente utilizado es el dos puntos (:). Esta convención permite dividir las claves en segmentos lógicos y hacer que sean fáciles de entender a simple vista.
- user:123:profile (Accede al perfil del usuario con ID 123).
- product:456:stock (Accede al stock de producto con ID 456).

### Evitar el Uso de Claves Demasiado Largas
Si bien Redis permite claves de longitud arbitraria, es recomendable mantener las claves lo más cortas y descriptivas posibles para evitar problemas de rendimiento y mejorar la legibilidad.
- user:123:profile en lugar de users:profiles:123:all_info.
- session:xyz en lugar de user_session_data_for_xyz_user_in_the_system.

### Usar Claves Específicas y Descriptivas
Las claves deben ser claras y auto-explicativas para poder identificar rápidamente lo que representan sin tener que analizar el contenido o el valor asociado.
- cart:{userId}:items (Lista de artículos en el carrito de compra del usuario).
- order:{orderId}:status (Estado de un pedido identificado por su ID).

### Considerar la Expiración de Claves
Cuando utilices claves que tienen una duración temporal, como sesiones de usuario o caché, es recomendable incluir un sufijo que indique su naturaleza temporal. Esto facilita la identificación y el mantenimiento de las claves expirables.
- session:{sessionId}:expires (Indicar la fecha de expiración de una sesión).
- cache:{cacheKey}:ttl (Indicar el tiempo de vida de un cache).

### Incluir Versiones o Prefijos de Aplicación si es Necesario
Cuando desarrollas una aplicación que podría tener múltiples versiones o clientes, es útil incluir un prefijo que indique la versión o el contexto de la aplicación. Esto previene conflictos de claves al actualizar la versión de la aplicación o al tener múltiples servicios que interactúan con Redis.
- app_v1:user:{userId}:profile
- app_v2:user:{userId}:profile

### Evitar el Uso de Caracteres Especiales Innecesarios
Aunque Redis permite el uso de caracteres especiales en las claves, es recomendable evitar el uso excesivo de caracteres especiales que puedan causar confusión o problemas en algunas situaciones. Limita los caracteres especiales a los más necesarios, como los dos puntos (:) para los espacios de nombres.

Caracteres recomendados:
- : (para separar las partes de la clave).
- _ (como un separador adicional si es necesario).
Caracteres a evitar:
- #, %, *, @, etc., ya que podrían generar confusión o interferir con otras herramientas de Redis.

### Evitar el Uso de Claves Estáticas con Valores Constantes
Es recomendable evitar claves que puedan ser estáticas y que se repitan constantemente sin aportar valor adicional. Las claves deberían estar asociadas a datos dinámicos que cambian con el tiempo.
- Evitar claves como: status:active, status:inactive, que probablemente no cambien de forma dinámica.
- Prefiere user:{userId}:status, ya que cada usuario podría tener su propio estado.

### Uso de Claves para Indicar Estado de Procesos
Si necesitas almacenar el estado de un proceso, es recomendable incluir en la clave información sobre el proceso y su estado de una forma comprensible.
- job:{jobId}:status para almacenar el estado de un trabajo en ejecución.
- task:{taskId}:progress para almacenar el progreso de una tarea.

### Claves para Eventos Temporales
Cuando trabajas con eventos o logs, es útil incluyendo la fecha o un timestamp en las claves, especialmente cuando los datos están organizados por fechas.
- log:{timestamp}:event para almacenar eventos con marcas de tiempo.

## Valores
### String
Los strings en Redis son la estructura de datos más básica y también la más utilizada. Una string puede almacenar cualquier tipo de valor, como números, texto o incluso datos binarios.
Casos de uso:
- Contadores: Almacenar y actualizar contadores de manera eficiente (como el número de visitas, clics, etc.).
- Caché: Almacenar datos temporales, como el resultado de una consulta costosa.
- TTL (Time to Live): Configurar un tiempo de expiración para claves de datos.

### Hashes
Los hashes permiten almacenar objetos complejos que consisten en una colección de pares clave-valor. Cada campo dentro de un hash tiene un nombre (campo) y un valor asociado.
Casos de uso:
- Almacenar información de usuario: Un hash es ideal para almacenar atributos de un usuario, como su nombre, dirección, edad, etc.
- Almacenar configuraciones: Puedes usar hashes para guardar configuraciones de aplicación, donde cada campo es una configuración diferente.

### List
Las lists son secuencias de elementos ordenados en Redis. Se pueden insertar y eliminar elementos desde ambos extremos de la lista, lo que las hace ideales para implementar estructuras como colas o pilas.

Casos de uso:
- Colas (Queues): Las listas de Redis son ideales para implementar sistemas de colas, como en el procesamiento de trabajos o tareas en segundo plano. Puedes usar las operaciones LPUSH y RPOP para agregar elementos al frente de la lista y consumirlos desde el final, creando una cola FIFO (First In, First Out).
- Pipelines: Puedes usar listas para organizar operaciones en batch o pipelines, procesando múltiples tareas en paralelo. Redis permite insertar y recuperar varios elementos de una lista en una sola operación.
- Mensajes en tiempo real: Almacenar mensajes para ser consumidos por otros sistemas.
- Registros históricos: Mantener un historial ordenado de eventos.
- Procesamiento Batch: Las listas son útiles cuando necesitas almacenar grandes volúmenes de datos y procesarlos en bloque. Puedes agregar elementos a la lista y luego recuperar un lote de elementos para su procesamiento.

### Sets y Sorted Sets
Un set es una colección no ordenada de elementos únicos. Redis asegura que no haya duplicados en un set. No importa el orden de los elementos, y las operaciones en sets son rápidas y eficientes.

Casos de uso:
- Eliminar duplicados: Utilizar sets para almacenar datos de forma única sin preocuparse por los duplicados.
- Sistemas de recomendación: Guardar elementos que se deben recomendar, como productos o servicios que un usuario ha interactuado.
- Seguimiento de usuarios activos: Almacenar identificadores de usuarios activos de forma eficiente.

Un sorted set es similar a un set, pero con la diferencia de que cada elemento en el conjunto tiene un puntaje (score) asociado. Los elementos se ordenan en función de este puntaje, lo que hace que los sorted sets sean ideales para casos en los que se necesita mantener un orden basado en algún criterio, como un ranking.

Casos de uso:
- Ranking de usuarios: Mantener una clasificación de usuarios según un puntaje (por ejemplo, puntuación en un juego o en una competencia).
- Sistemas de recomendación: Ordenar artículos, productos o contenidos en función de la relevancia.
- Liderazgo en tiempo real: Mostrar un ranking actualizado de la posición de los jugadores o usuarios en una aplicación.

### Bitmaps
Los bitmaps permiten trabajar con grandes volúmenes de datos binarios (bits), donde cada bit puede ser 0 o 1. Redis proporciona operaciones eficientes para manipular y contar bits.

Casos de uso:
- Flags: Puedes usar bitmaps para representar flags (banderas) o estados, como el seguimiento de la actividad de un usuario en una aplicación. Cada bit puede representar si un usuario ha realizado una acción o no.
- Contadores de usuarios activos: Un caso común es usar bitmaps para realizar un seguimiento de usuarios activos en un rango de tiempo o en un día determinado. Puedes usar BITCOUNT para contar cuántos bits están activados (representando usuarios activos).

### HyperLogLog
HyperLogLog es una estructura de datos probabilística utilizada para estimar el número de elementos únicos en un conjunto. Aunque no es exacta, es muy eficiente en cuanto a uso de memoria y es útil para grandes volúmenes de datos.

Casos de uso:
- Contar elementos únicos: Estimar el número de visitas únicas a una página web o la cantidad de usuarios que han interactuado con una aplicación.
- Rastreo de eventos únicos: Como el número de clics únicos, usuarios activos, o cualquier otro evento único.

### Streams
Los streams en Redis son una estructura de datos que permite almacenar y gestionar flujos de mensajes ordenados. Son útiles para crear sistemas de mensajería, logs o procesos de eventos en tiempo real.

Casos de uso:
- Sistemas de mensajería: Implementar aplicaciones de mensajería en tiempo real donde los mensajes se almacenan en orden y se consumen de manera secuencial.
- Logs y auditorías: Almacenar logs de eventos en tiempo real y procesarlos en orden cronológico.
- Procesamiento de eventos: Gestionar flujos de eventos, como notificaciones en tiempo real, de manera eficiente.

### Geolocalización
Redis permite almacenar y consultar datos geoespaciales mediante una serie de comandos optimizados para trabajar con ubicaciones geográficas.

Casos de uso:
- Sistemas de geolocalización: Almacenar la ubicación de usuarios, tiendas, eventos, etc., y realizar consultas de proximidad (por ejemplo, "¿cuáles son los usuarios más cercanos a mi ubicación?").
- Aplicaciones de navegación: Utilizar Redis para optimizar la búsqueda y visualización de datos relacionados con ubicaciones geográficas.

# Sistema de lectura y escritura
## Escritura
Las operaciones de escritura en Redis se gestionan mediante comandos que modifican el estado de las claves y sus valores
Proceso de Escritura:
- Comando de escritura: Redis acepta comandos de escritura, como SET, HSET, LPUSH, ZADD, etc., los cuales modifican los valores asociados a las claves.
- Confirmación de escritura: Redis responde al cliente confirmando que la operación fue exitosa, generalmente con un mensaje como OK o el valor actualizado (dependiendo del tipo de comando).
- Persistencia (Opcional): Si se tiene configurada la persistencia (por ejemplo, mediante RDB o AOF), Redis puede guardar los datos modificados en disco en intervalos regulares o después de ciertos comandos de escritura.

```bash
SET hola "mundo"
```

### Sobrescritura
Por defecto Redis es capaz de sobrescribir n veces la el valor de una clave para evitar esto debemos de agregar al comando de escritura la opcion NX o NN. 
- Opcion NX
Esta opcion solo lo registras cuando la clave/valor no existe y en caso de existir retornar (nil) y no modifica el valor
```bash
set name "pepito" NX
```
- Opcion XX
Esta opcion solo lo registras cuando la clave/valor existe y queremos que modifique el valor. en caso de no existir retornar (nil) y no registrar el valor
```bash
set name "pepito" XX
```

### Lectura
El sistema de lectura en Redis es también extremadamente rápido. Cuando un cliente solicita un valor asociado a una clave, Redis realiza una búsqueda directa en la memoria RAM para recuperar la información solicitada.
Proceso de Lectura:
- Comando de lectura: El cliente envía un comando de lectura, como GET, HGET, LRANGE, ZREVRANGE, etc., solicitando un valor almacenado en Redis.
- Retorno de resultados: Si Redis encuentra la clave, devuelve el valor correspondiente al cliente. Si no encuentra la clave, Redis devuelve un error o un valor nulo, dependiendo del tipo de comando utilizado.
- Sincronización con la persistencia (si aplica): Si la clave no existe en la memoria, pero se está utilizando persistencia, Redis puede intentar cargar los datos desde el disco, si se utiliza AOF o RDB.

```bash 
GET hola
```

# Configuracion
## Configuracion avanzada
## Configuracion de seguridad
# Despliegue  en entornos cloud y on-premises
# Patros de arquitectura
## Caching
## Session
## Pub/Sub
## Task Queses
## Rate Limiting
## Distributed Locks
## Geospatial Data
# Escalabilidad y alta disponibilidad
# Optimización
# Mantenimiento y resolucion
# Pruebas
# Comandos
## Comandos Generales
- AUTH: Autenticación para conectarse a Redis (si se configura contraseña).
- ECHO: Devuelve el mismo mensaje que recibe.
- PING: Comprueba si Redis está disponible.
- QUIT: Cierra la conexión actual.
- SELECT: Selecciona la base de datos específica en Redis.
- FLUSHDB: Elimina todas las claves de la base de datos seleccionada.
- FLUSHALL: Elimina todas las claves de todas las bases de datos.
- INFO: Proporciona información sobre el estado del servidor Redis.
- TIME: Devuelve la hora del servidor Redis.
- HELP @all: nos da toda la informacion de todos los comandos

## Comandos de Claves

- SCAN: Obtenemos todas las claves que coincidan con un patron de busqueda, los resultados nos los da paginados
- KEYS: Devuelve todas las claves que coincidan con un patrón.
- DEL: Elimina una o más claves.
- DUMP: Serializa la clave para poder almacenarla en otro lugar.
- EXISTS: Comprueba si una clave existe.
- EXPIRE: Establece el tiempo de vida de una clave (en segundos).
- EXPIREAT: Establece el tiempo de expiración de una clave en una fecha específica (en timestamp).
- MIGRATE: Mueve una clave de una base de datos Redis a otra.
- MOVE: Mueve una clave a otra base de datos (si la clave no existe en la base de datos actual).
- PERSIST: Elimina la expiración de una clave.
- PEXPIRE: Establece el tiempo de vida de la clave en milisegundos.
- PEXPIREAT: Establece la fecha de expiración en milisegundos.
- PTTL: Devuelve el tiempo restante de vida de una clave en milisegundos.
- RANDOMKEY: Devuelve una clave aleatoria de la base de datos actual.
- RENAME: Renombra una clave.
- RENAMENX: Renombra una clave solo si la nueva clave no existe.
- TTL: Devuelve el tiempo restante de vida de una clave en segundos.

## Comandos de Strings

- SET: Establece el valor de una clave.
- GET: Obtiene el valor de una clave.
- GETSET: Establece el valor de una clave y devuelve el valor anterior.
- MSET: Establece múltiples claves con valores.
- MGET: Obtiene los valores de múltiples claves.
- SETEX: Establece el valor de una clave con un tiempo de expiración.
- SETNX: Establece el valor de una clave solo si no existe.
- INCR: Incrementa el valor de una clave numérica.
- INCRBY: Incrementa el valor de una clave numérica por un valor específico.
- DECR: Decrementa el valor de una clave numérica.
- DECRBY: Decrementa el valor de una clave numérica por un valor específico.
- APPEND: Añade un valor a una clave.
- STRLEN: Devuelve la longitud del valor de una clave.
  
## Comandos de Hashes

- HSET: Establece el valor de un campo en un hash.
- HGET: Obtiene el valor de un campo en un hash.
- HDEL: Elimina uno o más campos de un hash.
- HEXISTS: Comprueba si un campo existe en un hash.
- HGETALL: Obtiene todos los campos y valores de un hash.
- HKEYS: Obtiene todos los campos de un hash.
- HVALS: Obtiene todos los valores de los campos de un hash.
- HINCRBY: Incrementa el valor de un campo en un hash.
- HSETNX: Establece un campo en un hash solo si no existe.
- HMSET: Establece múltiples campos en un hash (desaprobado en Redis 4.0 y posterior, se recomienda HSET).
- HMGET: Obtiene múltiples campos de un hash.

## Comandos de Listas

- LPUSH: Añade un valor al inicio de una lista.
- RPUSH: Añade un valor al final de una lista.
- LPOP: Elimina y devuelve el primer elemento de una lista.
- RPOP: Elimina y devuelve el último elemento de una lista.
- LLEN: Devuelve el número de elementos en una lista.
- LRANGE: Devuelve una sección de una lista.
- LREM: Elimina elementos de una lista.
- LSET: Establece el valor de un índice en una lista.
- LINSERT: Inserta un valor antes o después de un elemento en una lista.
- BLPOP: Elimina y devuelve el primer elemento de una lista, bloqueando la operación hasta que haya un valor.
- BRPOP: Elimina y devuelve el último elemento de una lista, bloqueando la operación hasta que haya un valor.

## Comandos de Conjuntos (Sets)

- SADD: Añade uno o más elementos a un conjunto.
- SREM: Elimina uno o más elementos de un conjunto.
- SMEMBERS: Devuelve todos los elementos de un conjunto.
- SISMEMBER: Comprueba si un elemento es miembro de un conjunto.
- SCARD: Devuelve el número de elementos en un conjunto.
- SPOP: Elimina y devuelve un elemento aleatorio de un conjunto.
- SRANDMEMBER: Devuelve un elemento aleatorio de un conjunto sin eliminarlo.
- SDIFF: Devuelve la diferencia entre conjuntos.
- SDIFFSTORE: Almacena la diferencia entre conjuntos en una nueva clave.
- SINTER: Devuelve la intersección de conjuntos.
- SINTERSTORE: Almacena la intersección de conjuntos en una nueva clave.
- SUNION: Devuelve la unión de conjuntos.
- SUNIONSTORE: Almacena la unión de conjuntos en una nueva clave.

## Comandos de Conjuntos Ordenados (Sorted Sets)

- ZADD: Añade uno o más elementos a un conjunto ordenado.
- ZREM: Elimina uno o más elementos de un conjunto ordenado.
- ZINCRBY: Incrementa la puntuación de un elemento en un conjunto ordenado.
- ZRANGE: Devuelve los elementos de un conjunto ordenado dentro de un rango.
- ZRANGEBYSCORE: Devuelve los elementos de un conjunto ordenado dentro de un rango de puntuación.
- ZRANK: Devuelve la posición de un elemento en un conjunto ordenado.
- ZREVRANGE: Devuelve los elementos de un conjunto ordenado en orden inverso.
- ZREVRANGEBYSCORE: Devuelve los elementos de un conjunto ordenado dentro de un rango de puntuación en orden inverso.
- ZREVRANK: Devuelve la posición de un elemento en un conjunto ordenado en orden inverso.
- ZCARD: Devuelve el número de elementos en un conjunto ordenado.
- ZPOPMIN: Elimina y devuelve el elemento con la puntuación más baja de un conjunto ordenado.
- ZPOPMAX: Elimina y devuelve el elemento con la puntuación más alta de un conjunto ordenado.

## Comandos de Bitmaps

- SETBIT: Establece un bit en una posición específica.
- GETBIT: Obtiene el valor de un bit en una posición específica.
- BITCOUNT: Cuenta el número de bits establecidos en un rango de bits.
- BITOP: Realiza operaciones bit a bit entre varios conjuntos de bits.

## Comandos de Streams

- XADD: Añade un nuevo mensaje a un stream.
- XREAD: Lee mensajes de uno o más streams.
- XREADBLOCK: Lee mensajes de un stream con un tiempo de espera bloqueante.
- XGROUP: Crea, elimina o consulta un grupo de consumidores para un stream.
- XACK: Marca un mensaje como confirmado por un consumidor en un grupo.
- XDEL: Elimina mensajes de un stream.
- XRANGE: Devuelve un rango de mensajes de un stream.
- XREVRANGE: Devuelve un rango de mensajes de un stream en orden inverso.

## Comandos de Pub/Sub

- PUBLISH: Publica un mensaje en un canal.
- SUBSCRIBE: Se suscribe a uno o más canales.
- UNSUBSCRIBE: Se desuscribe de uno o más canales.
- PSUBSCRIBE: Se suscribe a uno o más canales con un patrón.
- PUNSUBSCRIBE: Se desuscribe de uno o más canales con un patrón.

## Comandos de Transacciones

- MULTI: Inicia una transacción.
- EXEC: Ejecuta todas las operaciones de la transacción.
- DISCARD: Descarta todas las operaciones de la transacción.
- WATCH: Observa claves para verificar si se modifican antes de ejecutar una transacción.

## Comandos de Cluster

- CLUSTER INFO: Muestra información sobre el estado del clúster.
- CLUSTER NODES: Devuelve información sobre los nodos del clúster.
- CLUSTER MEET: Añade un nuevo nodo a un clúster.
- CLUSTER FORGET: Elimina un nodo del clúster.