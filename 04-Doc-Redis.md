<div align="center">
  <img src="https://raw.githubusercontent.com/jorgenavarroenamoradotokio/docs/main/logos/Redis-logo.svg">
</div>

## Índice
- [Introducción](#introducción)
  - [Arquitectura](#arquitectura)
  - [Modelo de base de datos en memoria (In-memory) y persistencia](#modelo-de-base-de-datos-en-memoria-in-memory-y-persistencia)
- [Instalación](#instalación)
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
- [Configuración](#configuración)
  - [Configuración de Memoria](#configuración-de-memoria)
  - [Configuración de Persistencia](#configuración-de-persistencia)
  - [Configuración de seguridad](#configuración-de-seguridad)
    - [Autenticación y Roles](#autenticación-y-roles)
    - [Cifrado con TLS](#cifrado-con-tls)
    - [Aislamiento en red](#aislamiento-en-red)
- [Patrón de arquitectura](#patrón-de-arquitectura)
  - [Caching](#caching)
  - [Session](#session)
  - [Pub/Sub](#pubsub)
  - [Task Queses](#task-queses)
  - [Rate Limiting](#rate-limiting)
  - [Distributed Locks](#distributed-locks)
  - [Geospatial Data](#geospatial-data)
- [Escalabilidad y alta disponibilidad](#escalabilidad-y-alta-disponibilidad)
  - [Sharding](#sharding)
  - [Replica Sets](#replica-sets)
  - [Failover Automático](#failover-automático)
  - [Monitoreo y Ajuste de Rendimiento](#monitoreo-y-ajuste-de-rendimiento)
- [Optimización](#optimización)
  - [Diseño Eficiente de Claves](#diseño-eficiente-de-claves)
  - [Uso Correcto de EXPIRE y TTL](#uso-correcto-de-expire-y-ttl)
  - [Minimización de Operaciones de Escritura](#minimización-de-operaciones-de-escritura)
  - [Compresión de Datos Almacenados](#compresión-de-datos-almacenados)
  - [Políticas de Desalojo](#políticas-de-desalojo)
  - [Evitar Almacenamiento de Datos Enormes en una Sola Clave](#evitar-almacenamiento-de-datos-enormes-en-una-sola-clave)
  - [No Usar Redis como Base de Datos Relacional](#no-usar-redis-como-base-de-datos-relacional)
- [Mantenimiento y resolución](#mantenimiento-y-resolución)
  - [Resolución de Problemas Comunes](#resolución-de-problemas-comunes)
  - [Recuperación de Datos en Casos de Falla](#recuperación-de-datos-en-casos-de-falla)
- [Pruebas](#pruebas)
  - [Pruebas de Carga y Estrés](#pruebas-de-carga-y-estrés)
  - [Simulación de Tráfico Real](#simulación-de-tráfico-real)
  - [Validación de Consistencia en Entornos Distribuidos](#validación-de-consistencia-en-entornos-distribuidos)
  - [Pruebas de Rendimiento en Escenarios de Caché](#pruebas-de-rendimiento-en-escenarios-de-caché)
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

# Instalación
## Sistemas Linux (Ubuntu/Debian)
En sistemas basados en Linux, como Ubuntu o Debian, la instalación de Redis es bastante sencilla gracias a los paquetes precompilados disponibles en los repositorios oficiales.
```bash
sudo apt update # actualizamos el indice de paquetes
sudo apt install redis-server redis-tools # instalamos redis
sudo systemctl status redis # verificamos que redis está corriendo
sudo systemctl enable redis # habilitamos redis para que se inicie automaticamente
redis-cli # Entramos en la consola de redis
```

## Sistemas Linux (CentOS)
Para sistemas como CentOS, el proceso de instalación es similar al de Ubuntu/Debian pero utilizando el gestor de paquetes yum o dnf (dependiendo de la versión).

```bash
sudo yum install epel-release # actualizamos el índice de paquetes
sudo yum install redis # instalamos redis
sudo systemctl start redis # verificamos que redis está corriendo

sudo systemctl enable redis # habilitamos redis para que se inicie automáticamente
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
Las claves deben ser claras y auto explicativas para poder identificar rápidamente lo que representan sin tener que analizar el contenido o el valor asociado.
- cart:{userId}:items (Lista de artículos en el carrito de compra del usuario).
- order:{orderId}:status (Estado de un pedido identificado por su ID).

### Considerar la Expiración de Claves
Cuando utilices claves que tienen una duración temporal, como sesiones de usuario o caché, es recomendable incluir un sufijo que indique su naturaleza temporal. Esto facilita la identificación y el mantenimiento de las claves que puedan expirar.
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
- Colas (Queues): Las listas de Redis son ideales para implementar sistemas de colas, como en el procesamiento de trabajos o tareas en segundo plano. Puedes usar las operaciones LPUSH y RPOP para agregar elementos al frente de la lista y consumirlos desde el final, creando una cola FIFO (First In, First Out).
- Pipelines: Puedes usar listas para organizar operaciones en batch o pipelines, procesando múltiples tareas en paralelo. Redis permite insertar y recuperar varios elementos de una lista en una sola operación.
- Mensajes en tiempo real: Almacenar mensajes para ser consumidos por otros sistemas.
- Registros históricos: Mantener un historial ordenado de eventos.
- Procesamiento Batch: Las listas son útiles cuando necesitas almacenar grandes volúmenes de datos y procesarlos en bloque. Puedes agregar elementos a la lista y luego recuperar un lote de elementos para su procesamiento.

### Sets y Sorted Sets
Un set es una colección no ordenada de elementos únicos. Redis asegura que no haya duplicados en un set. No importa el orden de los elementos, y las operaciones en sets son rápidas y eficientes.
- Eliminar duplicados: Utilizar sets para almacenar datos de forma única sin preocuparse por los duplicados.
- Sistemas de recomendación: Guardar elementos que se deben recomendar, como productos o servicios que un usuario ha interactuado.
- Seguimiento de usuarios activos: Almacenar identificadores de usuarios activos de forma eficiente.

Un sorted set es similar a un set, pero con la diferencia de que cada elemento en el conjunto tiene un puntaje (score) asociado. Los elementos se ordenan en función de este puntaje, lo que hace que los sorted sets sean ideales para casos en los que se necesita mantener un orden basado en algún criterio, como un ranking.
- Ranking de usuarios: Mantener una clasificación de usuarios según un puntaje (por ejemplo, puntuación en un juego o en una competencia).
- Sistemas de recomendación: Ordenar artículos, productos o contenidos en función de la relevancia.
- Liderazgo en tiempo real: Mostrar un ranking actualizado de la posición de los jugadores o usuarios en una aplicación.

### Bitmaps
Los bitmaps permiten trabajar con grandes volúmenes de datos binarios (bits), donde cada bit puede ser 0 o 1. Redis proporciona operaciones eficientes para manipular y contar bits.
- Flags: Puedes usar bitmaps para representar flags (banderas) o estados, como el seguimiento de la actividad de un usuario en una aplicación. Cada bit puede representar si un usuario ha realizado una acción o no.
- Contadores de usuarios activos: Un caso común es usar bitmaps para realizar un seguimiento de usuarios activos en un rango de tiempo o en un día determinado. Puedes usar BITCOUNT para contar cuántos bits están activados (representando usuarios activos).

### HyperLogLog
HyperLogLog es una estructura de datos probabilística utilizada para estimar el número de elementos únicos en un conjunto. Aunque no es exacta, es muy eficiente en cuanto a uso de memoria y es útil para grandes volúmenes de datos.
- Contar elementos únicos: Estimar el número de visitas únicas a una página web o la cantidad de usuarios que han interactuado con una aplicación.
- Rastreo de eventos únicos: Como el número de clics únicos, usuarios activos, o cualquier otro evento único.

### Streams
Los streams en Redis son una estructura de datos que permite almacenar y gestionar flujos de mensajes ordenados. Son útiles para crear sistemas de mensajería, logs o procesos de eventos en tiempo real.
- Sistemas de mensajería: Implementar aplicaciones de mensajería en tiempo real donde los mensajes se almacenan en orden y se consumen de manera secuencial.
- Logs y auditorías: Almacenar logs de eventos en tiempo real y procesarlos en orden cronológico.
- Procesamiento de eventos: Gestionar flujos de eventos, como notificaciones en tiempo real, de manera eficiente.

### Geolocalización
Redis permite almacenar y consultar datos geoespaciales mediante una serie de comandos optimizados para trabajar con ubicaciones geográficas.
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
Por defecto Redis es capaz de sobrescribir n veces la el valor de una clave para evitar esto debemos de agregar al comando de escritura la opción NX o NN. 
- Opción NX
Esta opcion solo lo registras cuando la clave/valor no existe y en caso de existir retornar (nil) y no modifica el valor
```bash
set name "pepito" NX
```
- Opción XX
Esta opción solo lo registras cuando la clave/valor existe y queremos que modifique el valor. en caso de no existir retornar (nil) y no registrar el valor
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

# Configuración
## Configuración de Memoria
Redis funciona en memoria, lo que lo hace extremadamente rápido pero también lo sujeta a limitaciones físicas.
- Configuración de maxmemory
Define el límite máximo de memoria que Redis puede utilizar. Si se alcanza el límite, Redis aplicará una política de desalojo para liberar espacio. (4gb)
- Políticas de Desalojo
Redis soporta varias políticas de desalojo para decidir qué datos eliminar cuando se alcanza el límite de memoria:
  - noeviction: Rechaza las escrituras cuando no hay suficiente memoria.
  - allkeys-lru: Elimina las claves menos usadas recientemente (LRU) en todo el espacio de claves.
  - volatile-lru: Elimina las claves menos usadas recientemente, pero solo de las claves con un tiempo de expiración.
  - allkeys-lfu: Elimina las claves menos usadas frecuentemente (LFU).
  - volatile-lfu: Similar a volatile-lru, pero basado en uso frecuente.
- Monitoreo y Ajustes
  - Comando: INFO memory para monitorear el uso de memoria.
  - Comando: MEMORY USAGE <key> para inspeccionar el tamaño de una clave específica.

## Configuración de Persistencia
Redis permite configurar persistencia para garantizar que los datos sobrevivan a reinicios o fallos.
- Persistencia con RDB (Redis Database Backup)
  - Realiza copias de seguridad periódicas del estado completo de la base de datos.
  - Ideal para escenarios en los que no se necesita una recuperación estricta en tiempo real.
- Persistencia con AOF (Append-Only File)
  - Registra todas las operaciones de escritura en un archivo de registro.
  - Permite una recuperación más precisa en comparación con RDB.
- Persistencia Híbrida
  - Combina las ventajas de RDB y AOF.
  - Se utiliza desde Redis 6.0 para mejorar el rendimiento y reducir el tiempo de recuperación.
- Compresión de Datos y Snapshots
  - Redis permite ajustar el tamaño y la frecuencia de los snapshots (RDB) para optimizar el almacenamiento.
  - Los datos se comprimen utilizando el algoritmo LZF para reducir el uso de disco.

## Configuración de seguridad
Redis no está diseñado para estar directamente expuesto a internet. La configuración de seguridad adecuada es esencial.

### Autenticación y Roles
Desde Redis 6.0, se introdujo un sistema avanzado de Access Control Lists (ACL) que permite gestionar usuarios y permisos.

- Configuración Básica
Configurar una contraseña global:
```bash
requirepass "TuContraseñaSegura"
```
- Configuración de ACL
Crear usuarios con permisos específicos:
```bash
acl setuser admin on >TuContraseñaSegura allkeys +@all
acl setuser read_only on >OtraContraseña ~readonly:* +@read
```

- Ver usuarios configurados:
```bash
ACL LIST
```

### Cifrado con TLS
Redis soporta TLS para asegurar la comunicación entre cliente y servidor.

Requisitos:
- Certificado SSL.
- Configuración de los archivos de certificado y clave en redis.conf.

```bash
tls-cert-file /ruta/a/certificado.pem
tls-key-file /ruta/a/clave.pem
tls-ca-cert-file /ruta/a/ca-cert.pem
tls-auth-clients yes
```

### Aislamiento en red
Asegurar que Redis solo escuche en interfaces internas:
- Implementar firewalls para restringir el acceso al puerto 6379.
- Usar subnets privadas en entornos cloud para proteger Redis de accesos externos.

# Patrón de arquitectura
Redis, con su modelo de datos versátil y alta velocidad, permite implementar patrones arquitectónicos efectivos para diversas aplicaciones modernas

## Caching
Redis es ampliamente utilizado como una capa de caché para acelerar el acceso a datos. Hay tres estrategias principales para la implementación de caché.
- Cache-aside (Lazy Loading): En este patrón, la aplicación consulta primero a Redis. Si la clave no está presente (cache miss), la aplicación obtiene los datos de la fuente original (por ejemplo, una base de datos), los devuelve al cliente y los almacena en Redis para futuras consultas.
  - Flujo del patrón:
    - Consulta a Redis.
    - Si no existe la clave:
      - Recupera los datos del sistema de origen.
      - Almacena los datos en Redis con una clave y un TTL (Time-to-Live).
- Write-through: La aplicación escribe simultáneamente en la fuente de datos original y en Redis. Este patrón garantiza que los datos en Redis siempre estén sincronizados con el sistema de origen.
  - Ventajas: Simplicidad en la consistencia de los datos.
  - Desventajas: Penalización de rendimiento debido a operaciones de escritura adicionales.
- Write-back: 
  - La aplicación actualiza primero los datos en Redis y luego sincroniza el sistema de origen en segundo plano.
  - Este patrón mejora el rendimiento de escritura, pero requiere un mecanismo para garantizar la persistencia.

## Session
Redis es ideal para gestionar sesiones debido a su velocidad y soporte para la expiración automática de claves.
- Implementación
  - Las sesiones se almacenan como claves en Redis.
  - La clave puede ser un identificador único de sesión (como un token JWT).
  - El valor contiene información de la sesión, generalmente en formato JSON.
- Mejores Prácticas
  - Usar claves con prefijos para distinguir las sesiones: session:session_id.
  - Configurar un TTL adecuado para evitar la acumulación de sesiones inactivas.
  - Encriptar o anonimizar datos sensibles antes de almacenarlos.

## Pub/Sub
El sistema de publicación/suscripción de Redis es utilizado para enviar mensajes entre servicios o notificar eventos en tiempo real.
- Comunicación entre Microservicios
Redis Pub/Sub permite que los servicios publiquen eventos a un canal, mientras que otros servicios suscritos a ese canal reciben notificaciones.
- Escenarios Comunes
  - Actualización de datos en tiempo real (como feeds).
  - Comunicación entre microservicios.
  - Notificaciones y alertas.

## Task Queses
Redis puede ser utilizado para gestionar colas de tareas mediante estructuras como listas o streams.
- Colas con Listas: Las listas de Redis (LPUSH y RPOP) son útiles para implementar colas FIFO.
- Procesamiento en Batch: Usar LRANGE para obtener varias tareas simultáneamente.
- Streams para Tareas Avanzadas: Los streams permiten la entrega garantizada de mensajes y el manejo de consumidores múltiples.

## Rate Limiting
Redis es efectivo para implementar restricciones de uso, como limitar solicitudes por usuario o IP.
- Token Bucket
  - Almacenar un contador en Redis que representa tokens disponibles.
  - El cliente consume un token por cada solicitud, y los tokens se recargan a intervalos regulares.
- Sliding Window Utiliza una lista o un conjunto ordenado para registrar las marcas de tiempo de las solicitudes y calcular el número de solicitudes permitidas en una ventana.

## Distributed Locks
Redis proporciona mecanismos para gestionar bloqueos distribuidos, lo cual es esencial en entornos multiusuario o distribuidos.
- Uso de SETNX
  - SETNX (Set if Not Exists) es utilizado para adquirir un bloqueo.
  - Una clave con un TTL asegura que el bloqueo se libere automáticamente si el proceso falla.
- Redlock: Un algoritmo distribuido para garantizar bloqueos seguros en múltiples nodos Redis.
- Uso de INCR y DECR: se usa para incrementar o decrementar en 1 un contador

## Geospatial Data
Redis soporta operaciones geoespaciales, útiles para aplicaciones que requieren búsquedas basadas en ubicación.
- Añadir Datos Geográficos: Almacenar ubicaciones con coordenadas.
- Búsquedas Basadas en Distancia: Encontrar ubicaciones dentro de un radio
- Cálculo de Distancias: Calcular la distancia entre dos puntos

# Escalabilidad y alta disponibilidad
Redis ofrece varios mecanismos para manejar cargas de trabajo crecientes y garantizar la alta disponibilidad.

## Sharding
El sharding es una técnica de distribución horizontal que permite dividir los datos entre múltiples nodos. Redis soporta sharding nativo mediante Redis Cluster.
- Redis Cluster
Redis Cluster distribuye automáticamente los datos y la carga entre múltiples nodos, proporcionando alta escalabilidad y tolerancia a fallos.
- Arquitectura
Los datos se dividen en 16384 slots de hash.
Cada nodo en el clúster maneja un subconjunto de estos slots.
Redis Cluster soporta replicas: cada nodo principal puede tener uno o más nodos secundarios.
- Slots y Claves Hash
Redis Cluster asigna cada clave a un slot mediante una función de hash: CRC16(key) % 16384.
Las claves que deben permanecer juntas (e.g., en operaciones como MGET) pueden utilizarse con etiquetas hash: key{tag}.
- Replicación en el Clúster
Cada nodo principal tiene uno o más nodos secundarios para garantizar alta disponibilidad.
Si un nodo principal falla, el clúster promueve automáticamente una réplica como nuevo nodo principal.

## Replica Sets
Las réplicas en Redis se utilizan para mejorar la disponibilidad y distribuir la carga de lectura.

## Failover Automático
Redis ofrece mecanismos como Sentinel para monitorear las instancias y realizar failover automático en caso de fallos.
- Configuración con Sentinel
Redis Sentinel monitorea las instancias de Redis, detecta fallos y promueve réplicas automáticamente.
- Integración con Herramientas Externas
Redis Sentinel puede integrarse con herramientas como:
  - Consul: Para registro de servicios.
  - Zookeeper: Para coordinación distribuida y detección de servicios.

## Monitoreo y Ajuste de Rendimiento
El monitoreo de Redis es esencial para garantizar un alto rendimiento y detectar cuellos de botella.
- Herramientas Nativas: 
  - Redis CLI
  - Redis Benchmark: Evaluar el rendimiento de Redis bajo carga
- Integración con Herramientas de Monitoreo
  - Prometheus y Grafana
  - Elastic Stack

# Optimización
Redis es una herramienta de alto rendimiento, pero para aprovecharla al máximo, es crucial implementar prácticas óptimas de diseño y administración.

## Diseño Eficiente de Claves
Un diseño eficiente de claves facilita la organización de datos y reduce el tiempo necesario para localizar información.
- Buenas Prácticas:
  - Claves descriptivas pero compactas: Las claves deben ser lo suficientemente descriptivas para identificar su propósito, pero evitar ser excesivamente largas, ya que Redis almacena claves en memoria.
  - Uso de prefijos: Implementar prefijos para categorizar claves y evitar colisiones en aplicaciones con múltiples subsistemas.
  - Evitar caracteres especiales: Aunque Redis permite casi cualquier carácter en las claves, es preferible usar solo caracteres seguros para facilitar debugging y operaciones automatizadas.

## Uso Correcto de EXPIRE y TTL
Establecer un tiempo de expiración para las claves garantiza que los datos innecesarios no ocupen memoria indefinidamente.
- Establecer expiración al crear claves
- Actualizar TTL según sea necesario
- Usar TTL para consultar el tiempo restante

## Minimización de Operaciones de Escritura
Las operaciones de escritura son costosas en términos de rendimiento y uso de memoria.
- Usar comandos atómicos: Combinar múltiples operaciones en un solo comando cuando sea posible.
Ejemplo: INCRBY, HSET, etc., en lugar de múltiples SET o GET seguidos por una modificación.
- Evitar sobreescritura innecesaria: Antes de actualizar una clave, verificar si el valor ha cambiado

## Compresión de Datos Almacenados
Reducir el tamaño de los datos en Redis puede ahorrar memoria y mejorar el rendimiento.
Uso de serialización eficiente:
- Convertir datos a formatos compactos como MessagePack o Protobuf en lugar de JSON o strings sin procesar.
- Compresión de datos grandes: Comprimir datos antes de almacenarlos en Redis usando herramientas como gzip.

## Políticas de Desalojo
Redis aplica políticas de desalojo cuando la memoria asignada está llena y se necesita espacio para nuevas claves. Configurar políticas adecuadas asegura que Redis gestione eficientemente los datos.
Políticas Soportadas:
- volatile-lru: Desaloja claves con TTL, basándose en el algoritmo Least Recently Used.
- allkeys-lru: Aplica LRU a todas las claves.
- volatile-lfu: Desaloja claves con TTL, basándose en la menor frecuencia de uso (Least Frequently Used).
- allkeys-lfu: Similar a volatile-lfu, pero para todas las claves.
- noeviction: Redis devuelve errores cuando no hay espacio disponible.

## Evitar Almacenamiento de Datos Enormes en una Sola Clave
Redis no está optimizado para manejar datos extremadamente grandes en una sola clave. Esto puede causar:
- Bloqueos al acceder o modificar la clave.
- Ineficiencia en el uso de memoria.
Alternativa: Dividir datos grandes en fragmentos más pequeños

## No Usar Redis como Base de Datos Relacional
Redis es una base de datos NoSQL diseñada para velocidad, no para modelado relacional complejo. Usar Redis para relaciones como JOIN entre tablas puede llevar a ineficiencia y código difícil de mantener.
Alternativa: Utilizar estructuras de datos nativas de Redis para simplificar relaciones
- Hashes para almacenar entidades relacionadas.
- Sets o Sorted Sets para manejar relaciones como rankings o referencias cruzadas.

# Mantenimiento y resolución
El mantenimiento proactivo y la resolución de problemas son esenciales para garantizar que Redis siga siendo un componente confiable y eficiente en aplicaciones críticas. Este capítulo aborda los problemas comunes que pueden surgir, estrategias para mantener Redis en producción, y cómo realizar la recuperación de datos en caso de fallas.

## Resolución de Problemas Comunes
Redis, a pesar de su simplicidad y rendimiento, puede enfrentar problemas como uso excesivo de memoria, latencia elevada o bloqueos. A continuación, se presentan los pasos y herramientas para identificar y resolver estos problemas.

- Identificación de Claves Grandes
Las claves grandes o desbalanceadas pueden consumir una cantidad desproporcionada de memoria y afectar el rendimiento.
Uso de SCAN: SCAN permite iterar sobre las claves de Redis sin bloquear el servidor.
Uso de MEMORY USAGE: MEMORY USAGE mide el tamaño en bytes de una clave específica
Automatización para encontrar claves grandes:
Un script en Python para identificar claves que superen un umbral de tamaño
```python
import redis
r = redis.StrictRedis(host='localhost', port=6379)
for key in r.scan_iter():
    size = r.memory_usage(key)
    if size > 1024 * 1024:  # Claves mayores a 1 MB
        print(f"Key: {key}, Size: {size} bytes")
```

- Manejo de Latencia y Bloqueos
Comando INFO: Evalúa métricas generales del sistema
Comando LATENCY DOCTOR: Identifica las causas comunes de latencia

Causas Comunes y Soluciones:
Operaciones costosas: 
  - Evitar operaciones como KEYS, FLUSHALL, o DEL en claves grandes.
  - Usar comandos alternativos: SCAN en lugar de KEYS.
Bloqueos por persistencia:
  - Redis puede bloquear durante la generación de snapshots (RDB) o al escribir un log de operaciones (AOF). 
  - Solución: Configurar persistencia asíncrona y reducir la frecuencia de snapshots.
Redes congestionadas:
  - Verificar el tráfico entre clientes y Redis.
  - Usar herramientas como tcpdump o netstat.

## Recuperación de Datos en Casos de Falla
Redis ofrece mecanismos para realizar copias de seguridad y restaurar datos en caso de fallos.
- Backup (Respaldos)
  - Snapshots (RDB)
  - Logs de Operaciones (AOF)
- Restore 
  - Restauración desde RDB
  - Restauración desde AOF

# Pruebas
Probar y validar Redis es esencial para garantizar su rendimiento y confiabilidad en entornos productivos. Este capítulo explora las mejores prácticas para realizar pruebas de carga y estrés, validar la consistencia en entornos distribuidos, y evaluar el rendimiento en escenarios de caché caliente y frío.

## Pruebas de Carga y Estrés
Redis ofrece herramientas integradas como redis-benchmark para medir el rendimiento bajo distintas cargas. Adicionalmente, se pueden simular escenarios de tráfico real para probar la capacidad del sistema.
- Uso de redis-benchmark
Redis-benchmark es una herramienta nativa para evaluar el rendimiento de Redis en términos de latencia, throughput, y operaciones por segundo (OPS).
```bash
redis-benchmark -q
```
Este comando realiza pruebas con los comandos más comunes (SET, GET, INCR, LPUSH, etc.) y muestra los resultados en términos de OPS.

Análisis de Resultados
- Latencia promedio: Debe mantenerse baja, idealmente en milisegundos.
- OPS (Operaciones por segundo): Un valor alto indica que Redis está manejando eficientemente las solicitudes.

## Simulación de Tráfico Real
Para entender cómo Redis se comportará bajo cargas específicas, se recomienda usar simulaciones personalizadas que representen el tráfico de la aplicación.

Herramientas Comunes:
- Apache JMeter:
Simula solicitudes a Redis mediante plugins especializados.
Configura patrones de carga como picos repentinos o tráfico constante.
- Redis Pipelining:
Redis soporta pipelining, lo que permite enviar múltiples comandos en una sola conexión, reduciendo la sobrecarga de red.

```python
import redis
r = redis.StrictRedis(host='localhost', port=6379)

pipeline = r.pipeline()
for i in range(1000):
    pipeline.set(f"key:{i}", i)
pipeline.execute()
```

Pruebas de Escenarios:
- Carga constante: Simula un flujo continuo de operaciones para medir estabilidad.
- Explosión de tráfico: Simula picos repentinos para evaluar cómo Redis maneja aumentos de carga.

## Validación de Consistencia en Entornos Distribuidos
En sistemas distribuidos, como Redis Cluster, garantizar la consistencia de datos es crucial, especialmente durante fallos o con configuraciones de replicación.

- Validación de Operaciones Atómicas
Redis asegura operaciones atómicas a nivel de comando, incluso en entornos distribuidos. Pruebas típicas incluyen:
Confirmar que INCR o DECR no generan resultados incorrectos bajo alta concurrencia.
Validar transacciones usando WATCH y MULTI.

```python
import redis
r = redis.StrictRedis(host='localhost', port=6379)
def increment_counter():
    r.watch("counter")
    current = int(r.get("counter") or 0)
    pipeline = r.pipeline()
    pipeline.multi()
    pipeline.set("counter", current + 1)
    pipeline.execute()

increment_counter()
```

- Consistencia en Redis Cluster
En Redis Cluster:
Datos distribuidos: Verificar que las claves se distribuyen uniformemente entre los nodos mediante CLUSTER KEYSLOT.
Replicación: Asegurar que los datos se replican correctamente en los nodos secundarios y validar la sincronización post fallo.
- Pruebas de Failover
Simular fallos y validar:
Promoción de réplicas: Usando Redis Sentinel.
Consistencia eventual: Asegurar que los datos están disponibles en todos los nodos después de un fallo.

## Pruebas de Rendimiento en Escenarios de Caché
Redis como caché puede operar en dos estados principales:
- Caché caliente: La mayoría de los datos solicitados están ya en memoria.
- Caché frío: Los datos solicitados no están inicialmente disponibles en memoria

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
- HELP @all: nos da toda la información de todos los comandos

## Comandos de Claves

- SCAN: Obtenemos todas las claves que coincidan con un patrón de búsqueda, los resultados nos los da paginados
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
- UNSUBSCRIBE: Se de suscribe de uno o más canales.
- PSUBSCRIBE: Se suscribe a uno o más canales con un patrón.
- PUNSUBSCRIBE: Se de suscribe de uno o más canales con un patrón.

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
