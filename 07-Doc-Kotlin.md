## Índice
- [Introducción](#introducción)
- [Características principales](#características-principales)
- [Variables](#variables)
  - [Ámbito de variables y duración de variables](#ámbito-de-variables-y-duración-de-variables)
  - [Inicialización por defecto](#inicialización-por-defecto)
  - [Variables primitivas y Variables de objeto](#variables-primitivas-y-variables-de-objeto)
  - [Inicialización diferida (`lateinit` y `lazy`)](#inicializacióndiferida-lateinitylazy)
- [Tipos de datos](#tipos-de-datos)
  - [Básicos](#básicos)
  - [Conversiones](#conversiones)
    - [Numéricas](#numéricas)
    - [Conversiones: SmartCast, UnSafeCast y SafeCast](#conversiones-smartcast-unsafecast-y-safecast)
- [String](#string)
  - [String templates](#string-templates)
  - [Raw Strings (""" ... """)](#raw-strings---)
- [Arrays y Colecciones](#arrays-y-colecciones)
  - [Arrays](#arrays)
  - [List](#list)
  - [Sets](#sets)
  - [Maps](#maps)
- [Operadores](#operadores)
  - [Aritméticos](#aritméticos)
  - [Asignación compuesta](#asignación-compuesta)
  - [Comparación](#comparación)
  - [Lógicos](#lógicos)
- [Null Safety](#null-safety)
- [Estructuras de control](#estructuras-de-control)
  - [Condicional `if`](#condicional-if)
  - [Expresión `when`](#expresión-when)
  - [Bucles](#bucles)
  - [Break y continue](#break-y-continue)
- [Funciones](#funciones)
- [Funciones de ámbito (`let`, `also`, `run`, `apply`, `with`)](#funciones-de-ámbito-let-also-run-apply-with)
- [Lambdas](#lambdas)
- [Excepciones](#excepciones)
- [Corrutinas](#corrutinas)
  - [Conceptos clave](#conceptosclave)
- [Programacion orientada a objetos (POO)](#programacion-orientada-a-objetos-poo)
  - [Modificadores de acceso](#modificadores-de-acceso)
  - [Constructores](#constructores)
  - [Inicialización `init`](#inicialización-init)
  - [Encapsulación (get/set)](#encapsulación-getset)
  - [Herencia](#herencia)
  - [Abstracciones](#abstracciones)
  - [Interfaces](#interfaces)
  - [Polimorfismo](#polimorfismo)
  - [Clases](#clases)
    - [Clases data](#clases-data)
    - [Clases Object (singleton)](#clases-object-singleton)
    - [Clases anidadas y clases internas](#clases-anidadas-y-clases-internas)
    - [Clases selladas (`sealed`)](#clases-selladas-sealed)
    - [Sobrecarga y sobreescritura](#sobrecarga-y-sobreescritura)
- [Anotaciones comunes](#anotacionescomunes)

# Introducción

Kotlin es un lenguaje de programación moderno, seguro, expresivo y totalmente interoperable con Java. Fue desarrollado por JetBrains y se convirtió en lenguaje oficial para Android en 2017.

**Ventajas:**
* Sintaxis concisa
* Seguridad ante `null`
* Interoperabilidad con Java
* Compatible con múltiples plataformas (JVM, JavaScript, iOS)

# Características principales

| Característica    | Descripción                                                            |
| ----------------- | ---------------------------------------------------------------------- |
| Conciso           | Menos líneas de código que Java                                        |
| Seguro            | Sistema de tipos que evita errores comunes como `NullPointerException` |
| Interoperable     | Reutiliza código Java sin problemas                                    |
| Multiplataforma   | Puede usarse en Android, backend, navegador (Kotlin/JS) y iOS          |
| Soporte funcional | Soporta funciones lambda y de orden superior                           |

# Variables

```kotlin
val nombre = "Kotlin"   // Inmutable
var edad = 10           // Mutable
```

En Kotlin hay dos formas de declarar variables:
- `val`: para variables de solo lectura (inmutables).
- `var`: para variables mutables.

**Inferencia de tipos:** Kotlin detecta el tipo de la variable al asignar un valor, aunque también puedes declararlo explícitamente:

```kotlin
val activo: Boolean = true
```

## Ámbito de variables y duración de variables

* **Locales**: dentro de funciones o bloques
* **De instancia**: declaradas en clases
* **Estáticas (companion object)**: compartidas por toda la clase
* **Parámetros**: en funciones

## Inicialización por defecto

* Enteros: `0`
* Flotantes: `0.0`
* Booleanos: `false`
* Char: `\u0000`
* Objetos: `null` (si son declarados como opcionales)

## Variables primitivas y Variables de objeto

* **Primitivas**: en Kotlin todos los tipos son objetos, pero el compilador los optimiza como 
tipos primitivos donde es posible.
* **Variables de objeto**: referencian instancias de clases. Al asignar una variable a otra,
ambas apuntan al mismo objeto en memoria.

## Inicialización diferida (`lateinit` y `lazy`)

Es una característica muy útil cuando no puedes o no quieres inicializar una variable en el
momento de su declaración.

* **`lateinit var`**: pospone la asignación de una propiedad **mutable** no nula hasta antes de su primer uso; se comprueba en _runtime_.

```kotlin
lateinit var nombre: String

class Usuario {
    lateinit var nombre: String

    fun inicializar() {
        nombre = "Carlos"
    }

    fun mostrar() {
        println("Nombre: $nombre")
    }
}

fun main() {
    val u = Usuario()
    u.inicializar()
    u.mostrar()  // Nombre: Carlos
}
```

* **`val by lazy { … }`** evalúa la expresión **una sola vez** la primera vez que se accede; es _thread‑safe_ por defecto.

```kotlin
val mensaje: String by lazy {
    println("Inicializando...")
    "Hola Kotlin"
}

fun main() {
    println("Antes del acceso")
    println(mensaje)     // Se inicializa aquí
    println(mensaje)     // Ya no se vuelve a calcular
}
```

# Tipos de datos

## Básicos

| Tipo    | Descripción             | Ejemplo  |
| ------- | ----------------------- | -------- |
| Boolean | true / false            | `true`   |
| Int     | Entero 32 bits          | `42`     |
| Long    | Entero largo            | `42L`    |
| Float   | Decimal simple          | `3.14f`  |
| Double  | Decimal doble precisión | `2.718`  |
| Char    | Carácter Unicode        | `'A'`    |
| String  | Cadena de caracteres    | `"Hola"` |

Versiones sin signo

| Tipo    | Descripción        |
| ------- | ------------------ |
| UByte   | Entero de 8 bits   | 
| UShort  | Entero de 16 bits  |
| UInt    | Entero de 32 bits  |
| ULong   | Entero de 64 bits  |


## Conversiones

### Numéricas
Las conversiones son **explícitas** para prevenir pérdida de precisión:

```kotlin
val x: Int = 10
val y: Long = x.toLong() // Correcto
```

Funciones de conversión comunes:
* `toByte()`, `toShort()`, `toInt()`, `toLong()`
* `toFloat()`, `toDouble()`
* `toChar()`

```kotlin
fun main() {
    val valor: Int = 42
    val largo: Long = valor.toLong()
    val decimal: Double = valor.toDouble()
    val floatVal: Float = 3.14f
    val intFromFloat: Int = floatVal.toInt() // Float → Int (pierde decimales)
    println("Long: $largo, Double: $decimal")
    println("Int desde Float: $intFromFloat")
}
```

### Conversiones: SmartCast, UnSafeCast y SafeCast

Hacer cast (o type casting) significa decirle al compilador que trate un valor de un tipo como si fuera de otro.
En Kotlin hay tres grandes formas de lograrlo

* **Smart-Cast** (`is`) permite al compilador inferir el tipo tras una comprobación
  
```kotlin
fun procesar(x: Any) {
    if (x is String) {        // comprueba el tipo
        println(x.length)     // aquí x es tratado como String automáticamente
    }
}
```

* **Un-Safe-Cast** Obliga al compilador a tratar el valor como otro tipo

```kotlin
val animal: Any = "Gato"
val texto: String = animal as String
val numero: Int   = animal as Int
```

* **Safe-Cast** Devuelve el objeto casteado o null si no se puede.
Evita excepciones y funciona bien con el sistema null–safety.

```kotlin
val dato: Any = 42
val texto: String? = dato as? String   // resultado → null
println(texto?.length ?: "No era String")
```

# String 

Un String es una secuencia inmutable de caracteres. Kotlin utiliza la clase String de la JVM, 
lo que significa que puedes acceder a todos los métodos que Java ofrece.

**Declaración y operaciones básicas**

```kotlin
val mensaje = "Hola, Kotlin"
println(mensaje.length)         // Tamaño: 12
println(mensaje[0])             // 'H'
println(mensaje.substring(0, 4)) // "Hola"
println(mensaje.contains("Kot")) // true
```

**Comparaciones**

```kotlin
val nombre = "Ana"
println(nombre == "Ana")                     // true
println(nombre.equals("ana", ignoreCase=true)) // true
```

## String templates

Kotlin permite interpolación de variables en cadenas con $ y expresiones con ${}:

```kotlin
val edad = 30
val saludo = "Tienes $edad años"
val futuro = "En 5 años tendrás ${edad + 5} años"
```

## Raw Strings (""" ... """)
Cadenas multilínea, sin necesidad de escapar caracteres especiales
Preserva saltos de línea, No necesita escapar caracteres especiales como \n o \",
Ideal para escribir texto multilínea, JSON, SQL, etc.

```kotlin
val texto = """
    Línea 1
    Línea 2
    Línea 3
""".trimIndent() // elimina los espacios comunes al inicio de cada línea
println(texto)
```

# Arrays y Colecciones

Las colecciones estándar tienen variantes **inmutables** y **mutables**.

## Arrays 

```kotlin
val elementos = Array<Int>(3){100}
val numeros = arrayOf(1, 2, 3, 4, 5)
val edades = intArrayOf(10, 20, 30)
val notas = doubleArrayOf(8.5, 7.0, 9.2)
val vacio = arrayOfNulls<String>(3) // null, null, null
val cuadrados = Array(5) { i -> i * i }  // [0, 1, 4, 9, 16]

val matriz = arrayOf(
    arrayOf(1, 2, 3),
    arrayOf(4, 5, 6),
    arrayOf(7, 8, 9)
)
```

## List

Es una agrupación de objetos ordenada que permite elementos duplicados.

```kotlin
val lista = listOf("Lunes", "Martes")
val mutable = mutableListOf("A")
mutable.add("B")
```

**Tipos**

- `listOf`  inmutable
- `mutableListOf` mutable

```kotlin
val lista = listOf("Lunes", "Martes")
val mutable = mutableListOf("A")
mutable.add("B")

// Elimina y ordenar de manera descendente
val listNum = mutableListOf(1, 2, 3)
listNum.removeAt(0)
listNum.sortDescending()
```

**Principales métodos para listas**

- Add
- Remove
- sort
- contains
- indexOf

**Recorrer una lista**

- Un bucle estándar for
- Un bucle forEach

## Sets

No permite elementos duplicados, puede o no estar ordenada, dependiendo de su implementación.

**Tipos**

- `setOf`  inmutable
- `mutableSetOf` mutable

```kotlin
val conjunto = setOf(1, 2, 2)  // [1, 2]
```

**Principales métodos para listas**

- Add
- Remove
- contains

**Recorrer un Set**

- Un bucle estándar for
- Un bucle forEach

## Maps

Es una colección de pares: clave → valor. Cada clave debe ser única.

**Tipos**

- `mapOf`  inmutable
- `mutableMapOf` mutable

**Principales métodos para listas**

- put
- Remove
- keys
- values
- entries

**Recorrer un Map**

- Un bucle estándar for
- Un bucle forEach

```kotlin 
val mapa = mapOf("nombre" to "Ana", "edad" to 30)

val mapaMutable = mutableMapOf<String, Int>()
mapaMutable.put("uno", 1)
mapaMutable.put("dos", 2)

for ((clave, valor) in mapa) {
    println("$clave → $valor")
}
```

# Operadores

## Aritméticos

- Operador de suma (`+`)
- Operador de resta (`-`)
- Operador de multiplicación (`*`)
- Operador división (`/`)
- Operador módulo de la división (`%`)
- Operador de incremento (`++`): se utiliza para aumentar el valor de una variable en uno.
- Operador de decremento (`--`): se utiliza para restar el valor de una variable en uno.
  * Delante de la variable: se realiza primero la operación y luego se lo asigna a la variable el resultado.
  * Detrás de la variable: primero se asigna el valor a la variable y luego se opera.

## Asignación compuesta

- Operador de asignación de suma (`+=`). 
- Operador de asignación de resta (`-=`). 
- Operador de asignación de multiplicación (`*=`). 
- Operador de asignación de división (`/=`). 
- Operador de asignación de modulo (`%=`).

```kotlin
var contador = 5
contador += 3  // contador = 8
```

## Comparación

- Operador menor (`<`). 
- Operador mayor (`>`). 
- Operador menor o igual (`<=`). 
- Operador mayor o igual (`>=`). 
- Operador igual (`==`). 
- Operador distinto de igual (`!=`).

## Lógicos

- and `&&`
- or `||`
- distinto `!`

# Null Safety

Evita errores por referencias nulas:
* `?.`: llamada segura
* `?:`: operador Elvis
* `!!`: asume que no es null (no recomendado)
* `let`: Ejecuta un bloque de código solo si la variable no es null (cuando se combina con `?.`)

```kotlin
val nombre: String? = null
val longitud = nombre?.length ?: 0
println("$longitud")

val saludo = nombre ?: "Desconocido"
println("Hola, $saludo")

val nombre: String? = null
nombre?.let {
    println("El nombre tiene ${it.length} letras")
}  // No imprime nada si es null

```

# Estructuras de control

Las instrucciones de control son sentencias que permiten controlar el flujo de ejecución de un programa. Estas instrucciones se dividen en tres categorías:
- Instrucciones de selección o condicionales
- Instrucciones de iteración o de bucle.
- Instrucciones de acceso o salto.

## Condicional `if`

```kotlin
val max = if (a > b) a else b
```

## Expresión `when`

Es el reemplazo moderno del switch de Java, pero mucho más flexible, limpio y expresivo. 
Puedes usarla tanto como expresión (retorna un valor) como estructura de control.

```kotlin
when (x) {
    x < 0 -> println("Negativo")
    1 -> println("Uno")
    in 2..5 -> println("Rango")
    else -> println("Otro")
}

val vocal = 'a'
when (vocal) {
    'a', 'e', 'i', 'o', 'u' -> println("Es una vocal")
    else -> println("No es una vocal")
}

when (valor) {
    is Int -> println("Es un entero")
    is String -> println("Es un texto")
    is Boolean -> println("Es un booleano")
    else -> println("Tipo desconocido")
}
```

## Bucles

```kotlin
for (i in 1..5) println(i)

// Saltando posiciones
for (i in 1..10 step 2) {
    println(i) // 1, 3, 5, 7, 9
}

//  Inverso
for (i in 5 downTo 1) {
    println(i) // 5, 4, 3, 2, 1
}

// Omitir ultimo valor
for (i in 0 until 5) {
    println(i) // 0, 1, 2, 3, 4
}

// Recorrer una lista
val frutas = listOf("Manzana", "Banana", "Naranja")
for (fruta in frutas) {
    println(fruta)
}

while (x < 10) x++

do {
    println(x)
} while (x < 10)
```

## Break y continue

- `Break` fuerza la salida del bucle
- `Continue` fuerza a pasar la siguiente iteración
- Puedes etiquetar un bucle y luego usar break o continue para controlar bucles anidados

En caso de usar estas sentencias en la ejecución de bucles anidados debemos de tener en 
cuenta que si no indicamos nada la sentencia break/continue afecta al bucle mas interno pero 
si queremos cambiar este comportamiento deberemos de indicar un alias/etiqueta para que 
afecte al bucle que queramos.

```kotlin
// Cuando i es 5, el bucle se rompe y se sale del for.
for (i in 1..10) {
    if (i == 5) break
    println(i)
}

// Cuando i es 3, se salta la impresión y continúa con el siguiente número.
for (i in 1..5) {
    if (i == 3) continue
    println(i)
}

// Uso de etiquetas
outer@ for (i in 1..3) {
    for (j in 1..3) {
        if (i == 2) break@outer
    }
}
```

# Funciones 

```kotlin
fun saludar(nombre: String): String  = return "Hola, $nombre"
```

**Valores por defecto**:

```kotlin
fun saludar(nombre: String = "Invitado")
```

* **Sobrecarga de funciones**: 
 
```kotlin
mostrar("Programador", "Kotlin")
mostrar("Programador")
mostrar(language = "Kotlin")

fun mostrar(job: String) = println(job)
fun mostrar(job: String = "Administrador", language: String) = println("Trabajo $job - Lenguaje $language")
```

* **Funciones infix**:

Las funciones infix permiten un estilo más natural de lectura, como 5 por 3 en lugar de 5.por
(3).

```kotlin
infix fun Int.por(x: Int) = this * x
println(5 por 3) // 15
```

* **Parámetros variables (`vararg`)**:

```kotlin
fun imprimir(vararg mensajes: String)
```

* **Extensiones**:

```kotlin
fun String.mayusculas(): String = this.uppercase()

val msg: String = "hola"
println(msg.mayusculas())
```

* **Orden superior**:

```kotlin
fun operar(a: Int, b: Int, f: (Int, Int) -> Int): Int = f(a, b)
val suma = operar(2, 3) { x, y -> x + y }
```

# Funciones de ámbito (`let`, `also`, `run`, `apply`, `with`)

Las scope functions ejecutan un bloque dentro del contexto de un objeto y devuelven, según el caso, el resultado del bloque o el propio objeto.

| Función | Receptor (this/it) | Devuelve        | Uso típico |
|---------|-------------------|-----------------|------------|
| `let`   | `it`              | Resultado bloque| Ejecutar lógica si no es null; transformar |
| `also`  | `it`              | Objeto          | Side‑effects (logging, debug)              |
| `run`   | `this`            | Resultado bloque| Calcular y devolver valor                  |
| `apply` | `this`            | Objeto          | Configurar/ inicializar objeto             |
| `with`  | `this`            | Resultado bloque| Agrupar operaciones sobre un objeto        |


```kotlin
// let
val nombre: String? = "Kotlin"
nombre?.let {
    println("La longitud es ${it.length}")
}

// also
val lista = mutableListOf("A", "B")
lista
    .also { println("Antes: $it") }
    .add("C")

// run
val texto: String? = "Texto"
val longitud = texto?.run { length } // solo si texto no es null

// apply
data class Person(var nombre: String = "", var edad: Int = 0)
val usuario = Person().apply {
    nombre = "Carlos"
    edad = 25
}
println(usuario) // Person(nombre=Carlos, edad=25)

// with
val builder = StringBuilder()
val resultado = with(builder) {
    append("Hola, ")
    append("mundo!")
    toString()
}
println(resultado) // Hola, mundo!
```

# Lambdas

Una lambda es una función anónima (sin nombre) que puedes
* Guardar en una variable
* Pasar como argumento a otra función
* Devolver como resultado desde otra función
* No puedes usar `return` para salir directamente de una función externa dentro de una lambda.
En ese caso se puede usar `return@nombreEtiqueta` o una función anónima

```kotlin
val nombreLambda: Tipo = { parámetros -> cuerpo }

// Anonima
val saludar = { println("Hola Kotlin") }
saludar() // Imprime: Hola Kotlin

// Con parametros
val cuadrado: (Int) -> Int = { x -> x * x }
println(cuadrado(4))  // 16

// Con multiples parametros
val suma: (Int, Int) -> Int = { a, b -> a + b }
println(suma(2, 3))  // 5

// inferencia automatica de tipos
val resta = { a: Int, b: Int -> a - b }


// Uso en función de orden superior
fun procesarLista(lista: List<Int>, operacion: (Int) -> Int): List<Int> {
    return lista.map(operacion)
}
```

**Parametro it**: Cuando hay solo un parámetro, Kotlin permite usar la palabra clave it
automáticamente

```kotlin
val triple = { it: Int -> it * 3 }
val resultado = triple(4)  // 12

val triple: (Int) -> Int = { it * 3 }
```

**Lambdas como argumentos a funciones**

```kotlin
fun operar(a: Int, b: Int, operacion: (Int, Int) -> Int): Int {
    return operacion(a, b)
}

val resultado = operar(5, 3) { x, y -> x * y }
println(resultado)  // 15
```

**Lambdas en colecciones**

```kotlin
// Filter
val lista = listOf(1, 2, 3, 4, 5)
val pares = lista.filter { it % 2 == 0 }  // [2, 4]

// map
val dobles = lista.map { it * 2 }  // [2, 4, 6, 8, 10]

// forEach
lista.forEach { println(it) }
```

**Lambdas como retorno de funciones**

```kotlin
fun generadorDeMultiplicador(factor: Int): (Int) -> Int {
    return { numero -> numero * factor }
}

val porTres = generadorDeMultiplicador(3)
println(porTres(4))  // 12
```

# Excepciones

```kotlin
try {
    val resultado = 10 / 0
} catch (e: ArithmeticException) {
    println("Error: ${e.message}")
} finally {
    println("Finalizando")
}

val edad = 2
if (edad < 18) {
    throw IllegalArgumentException("Debe ser mayor de edad")
} else {
    println("Edad válida")
}
```

# Corrutinas

Las corrutinas son la solución de Kotlin para la **concurrencia asíncrona y no bloqueante**.

## Conceptos clave

| Término | Qué hace | Ejemplo |
|---------|----------|---------|
| `suspend` | Marca una función que puede **suspenderse** sin bloquear el hilo. | `suspend fun fetch(): String` |
| `CoroutineScope` | Alcance donde viven las corrutinas; gestiona su cancelación. | `scope.launch { … }` |
| `launch` | Inicia una corrutina que no devuelve resultado. | `scope.launch { actualizarUI() }` |
| `async/await` | Devuelve un `Deferred<T>` para obtener un valor futuro. | `val datos = async { api.get() }.await()` |
| `Dispatcher` | Decide en qué hilo/hilos se ejecuta. | `withContext(Dispatchers.IO) { … }` |

```kotlin
fun main() = runBlocking {
    val tiempo = measureTimeMillis {
        val uno = async { tareaPesada(1) }
        val dos = async { tareaPesada(2) }
        println("Resultado = ${uno.await() + dos.await()}")
    }
    println("Completado en $tiempo ms")
}
```

> **Tip**: Usa **`SupervisorJob`** para que el fallo de una corrutina hija no cancele sus hermanas.

# Programacion orientada a objetos (POO)

Clases, herencia, abstracciones e interfaces funcionan como en Java, pero con _syntactic sugar_:
- `data class` genera automáticamente métodos de utilidad.  
- Clases son `final` por defecto → usa `open` para heredar.  
- `sealed class` restringe jerarquías y permite exhaustividad en `when`.

## Modificadores de acceso

| Modificador | Significado                                   |
| ----------- | --------------------------------------------- |
| `public`    | Accesible desde cualquier lugar (por defecto) |
| `private`   | Accesible solo dentro de la clase             |
| `protected` | Solo accesible en la clase y sus subclases    |
| `internal`  | Accesible dentro del mismo módulo             |

```kotlin
class Persona {
    private var secreto = "1234"
    public var nombre = "Juan"
}
```

## Constructores

* **Definición básica**

```kotlin
class Persona {
    var nombre: String = ""
    var edad: Int = 0
}

val persona = Persona()
persona.nombre = "Ana"
persona.edad = 30
```

* **Primario**

```kotlin
class Persona(val nombre: String, var edad: Int)

val p = Persona("Luis", 25)
println(p.nombre)  // Luis
```

* **Secundario**

```kotlin
class Alumno {
    var nombre: String
    var edad: Int

    constructor(nombre: String, edad: Int) {
        this.nombre = nombre
        this.edad = edad
    }
}
```

## Inicialización `init`

El bloque init se ejecuta justo después del constructor primario

```kotlin
class Estudiante(val nombre: String) {
    init {
        println("Creando estudiante con nombre: $nombre")
    }
}
```

## Encapsulación (get/set)

```kotlin
class Usuario {
    var edad: Int = 0
        set(value) {
            field = if (value < 0) 0 else value // field hace referencia al campo edad
        }
        get() field
}
```

## Herencia

En Kotlin, las clases son final por defecto, así que deben marcarse con open para permitir herencia.

```kotlin
open class Animal(val nombre: String) {
    open fun hablar() {
        println("$nombre hace un sonido")
    }
}

class Perro(nombre: String) : Animal(nombre) {
    override fun hablar() {
        println("$nombre dice: Guau")
    }
}

val perro = Perro("Max")
perro.hablar()  // Max dice: Guau
```

## Abstracciones

```kotlin
abstract class Figura {
    abstract fun area(): Double
}

class Circulo(val radio: Double) : Figura() {
    override fun area(): Double = Math.PI * radio * radio
}
```

## Interfaces

Kotlin permite herencia múltiple de interfaces

```kotlin
interface Vehiculo {
    fun encender()
}

class Auto : Vehiculo {
    override fun encender() {
        println("Auto encendido")
    }
}
```

## Polimorfismo

Permite tratar objetos diferentes a través de un mismo tipo base

```kotlin
val lista: List<Figura> = listOf(Circulo(3.0), Circulo(5.0))

for (f in lista) {
    println(f.area())
}

```

## Clases
### Clases data

Se usan para almacenar datos, y automáticamente generan: equals, hashCode, toString, copy, etc

```kotlin
data class Producto(val nombre: String, val precio: Double)

val prod1 = Producto("Pan", 1.0)
val prod2 = prod1.copy(precio = 1.2)
```

### Clases Object (singleton)

```kotlin
object Config {
    val version = "1.0.0"
    fun imprimir() = println("Versión: $version")
}
```

### Clases anidadas y clases internas

```kotlin
class Externa {
    private val mensaje = "Hola"

    class Anidada {
        fun saludar() = "Desde clase anidada"
    }

    inner class Interna {
        fun saludar() = mensaje
    }
}
```

### Clases selladas (`sealed`)

Usadas para modelar tipos restringidos (como enums, pero con más poder):

```kotlin
sealed class Resultado
class Exito(val datos: String) : Resultado()
class Error(val mensaje: String) : Resultado()

fun manejar(r: Resultado) {
    when (r) {
        is Exito -> println("OK: ${r.datos}")
        is Error -> println("Error: ${r.mensaje}")
    }
}
```

### Sobrecarga y sobreescritura

* **Sobrecarga**: varios métodos con el mismo nombre pero diferentes parámetros
* **Sobreescritura**: redefinir comportamiento heredado (`override`)

```kotlin
class Calculadora {
    fun sumar(a: Int, b: Int): Int = a + b
    fun sumar(a: Double, b: Double): Double = a + b
}
```

# Anotaciones comunes

| Anotación | Propósito |
|-----------|-----------|
| `@JvmStatic` | Expone método/propiedad como `static` para Java. |
| `@JvmOverloads` | Crea sobrecargas para parámetros con valor por defecto. |
| `@JvmField` | Expone propiedad como campo público. |
| `@Serializable` (kotlinx.serialization) | Genera _serializers_ en tiempo de compilación. |
| `@Parcelize` | Implementa automáticamente `Parcelable` en Android. |
| `@Inject` / `@HiltAndroidApp` | DI con Dagger/Hilt. |
| `@OptIn` | Habilita APIs experimentales. |
