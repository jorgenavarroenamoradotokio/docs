<div align="center">
  <img src="https://raw.githubusercontent.com/jorgenavarroenamoradotokio/docs/feature/java/logos/Java-Logo.svg">
</div>

# Introducción

Java es un lenguaje de programación orientado a objetos que fue desarrollado por Sun Microsystems en la década de 1990 y gestionado actualmente por Oracle Corporation. Java es un lenguaje de programación de alto nivel y es conocido por su portabilidad, lo que significa que el código Java puede ser ejecutado en cualquier plataforma que tenga una máquina virtual Java (JVM) instalada.

## Términos principales de java

<table>
  <tr>
    <td>Simple</td>
    <td>Java dispone de un conjunto conciso y coherente de características que facilitan su aprendizaje y su uso.</td>
  </tr>
  <tr>
    <td>Seguro</td>
    <td>Java constituye un medio seguro para crear aplicaciones de Internet</td>
  </tr>
  <tr>
    <td>Portable</td>
    <td>Los programas de Java se pueden ejecutar en cualquier entorno para el que exista un sistema de tiempo de ejecución de Java (JVM)</td>
  </tr>
  <tr>
    <td>Orientado a Objetos</td>
    <td>Java aplica la filosofía moderna de programación orientada a Objetos</td>
  </tr>
  <tr>
    <td>Robusto</td>
    <td>Java aboga por una programación sin errores gracias a sus tipos estrictos y las comprobaciones en tiempo de ejecución</td>
  </tr>
  <tr>
    <td>Subprocesos múltiples</td>
    <td>Java ofrece compatibilidad con programación de subprocesamiento múltiple.</td>
  </tr>
  <tr>
    <td>Neutralidad arquitectónica</td>
    <td>Java no se limita a un equipo o sistema operativo en concreto.</td>
  </tr>
  <tr>
    <td>Interpretado</td>
    <td>Java admite código compatible entre plataformas gracias al uso de código de bytes</td>
  </tr>
  <tr>
    <td>Alto rendimiento</td>
    <td>El código de bytes de Java esta optimizado para acelerar la ejecución</td>
  </tr>
  <tr>
    <td>Distribuido</td>
    <td>El diseño de Java se orientas al entrono distribuido de Internet</td>
  </tr>
  <tr>
    <td>Dinámico</td>
    <td>Los programas de Java incluyen abundante información de tiempo de ejecución que se usa para verificar y resolver el acceso a objetos en tiempo de ejecución</td>
  </tr>
</table>

## La programación orientada a objetos (OOP)

La Programación Orientada a Objetos (POO) es un paradigma de programación que se enfoca en el concepto de "objetos", los cuales son instancias de una clase y que tienen propiedades (atributos) y acciones (métodos) asociados.
En POO, se modelan los problemas como una colección de objetos que interactúan entre sí para lograr un objetivo. Cada objeto es una entidad independiente que tiene su propio estado interno y puede realizar acciones específicas. Estos objetos pueden ser agrupados en clases, las cuales son modelos que describen las propiedades y acciones que los objetos de una determinada categoría deben tener. La POO se basa en cuatro principios fundamentales:
- Encapsulamiento: Es un mecanismo de programación que combinan el código con los datos que manipula, al tiempo que los protege de interferencias externas.
Los atributos y métodos de un objeto están encapsulados en su propia clase, lo que significa que no pueden ser accedidos directamente desde fuera de la clase.
-	Herencia: permite la creación de nuevas clases a partir de clases ya existentes, adquiriendo las propiedades y métodos de la clase padre.
-	Polimorfismo: la capacidad de un objeto para tomar diferentes formas o comportamientos dependiendo del contexto.
-	Abstracción: el proceso de identificar las características esenciales de un objeto o sistema y eliminar todo lo que no es relevante para el problema que se está resolviendo.

## Técnica de sangrado

Java es un lenguaje libre, lo que significa que no importa la posición de las instrucciones en una línea. No obstante, con el paso del tiempo, se ha desarrollado un estilo de sangrado común que permite crear programas más legibles.
El estilo más común de sangrado es después de cada llave, es decir, aplicamos un nivel de sangrado.
Tendremos que tener en cuenta que existen instrucciones especiales que requieren un sangrado adicional.

## Palabras reservadas de java

Una palabra reservada en Java es una palabra clave que tiene un significado especial y está reservada por el lenguaje Java para realizar una función específica. No se pueden utilizar como identificadores para nombres de variables, nombres de clases, nombres de métodos u otros identificadores definidos por el usuario en el código fuente de Java.

Las palabras reservadas de Java se utilizan para declarar variables, estructuras de control de flujo, métodos, clases y otras construcciones del lenguaje de programación Java. Debido a que estas palabras tienen un significado especial en el lenguaje, no se pueden usar para otros fines que no sean los definidos por el lenguaje Java.

Es importante conocer y entender las palabras reservadas de Java para poder escribir un código fuente válido en Java y evitar errores de sintaxis.

# Variables

Es un contenedor que se utiliza para almacenar datos que pueden cambiar a lo largo de la ejecución de un programa. Cada variable tiene un tipo de datos específico que define qué tipo de valor puede almacenar, como números enteros, caracteres, cadenas de texto, etc.

## Definir una variable

La estructura a la hora de definir una variable siempre es el mismo, el tipo de variable, el nombre de la variable y el valor de la variable, siendo este último optativo ya que, por defecto según el tipo y ámbito de la variable, aunque normalmente suele ser null. Ejemplos de definición de variables

- Declaración: int mivar;
- Declaración e inicialización:  int p =10;
- Declaración múltiple con inicialización: int p, s, a=5;
  
Los identificadores de las variables (nombres) se pueden utilizar cualquier tipo combinación de letras, número y los símbolos $ y _. Pero existen unas excepciones, estas excepciones son:
-	No se pueden usar palabras reservadas, ni la palabra goto.
-	No pueden comenzar por un carácter numérico. 

## Ámbito de variables y duración de variables

En Java, el ámbito y la duración de una variable dependen del tipo de variable que se esté utilizando. Hay cuatro tipos principales de variables en Java: variables locales, variables de instancia, variables de clase y variables de parámetros.

- Variables locales: Son variables que se declaran dentro de un método o bloque de código y su ámbito está limitado a ese bloque. Estas variables se crean cuando se ejecuta el bloque y se eliminan cuando el bloque se completa.
- Variables de instancia: Son variables que se declaran dentro de una clase, pero fuera de cualquier método. Estas variables se crean cuando se crea un objeto de la clase y se eliminan cuando el objeto es eliminado.
- Variables de clase: Son variables que se declaran dentro de una clase y fuera de cualquier método con la palabra clave static. Estas variables se crean cuando se carga la clase en la memoria y se eliminan cuando la clase es eliminada de la memoria.
  
- Variables de parámetros: Son variables que se utilizan para pasar valores a un método. Estas variables se crean cuando se llama al método y se eliminan cuando el método se completa.
Pero también existe el ámbito de visibilidad:
  *	A nivel de clase compartidas por todos los métodos (se les conoce como atributos o campos).
  *	A nivel de método solo visibles dentro de ese método (se les conoce como locales).
  *	A nivel de bloque solo visibles dentro de esa estructura (se les conoce como locales).

### Variables primitivas y Variables de objeto

- Variables primitivas
Las variables primitivas o tipo elementan, son variables de datos originales de un lenguaje, esto es, aquellas que nos proporciona el lenguaje con los que podemos en ocasiones construir tipos de datos abstractos y estructuras de datos.La ventaja de estas variables es que a hora de crearlas asigna directamente un espacio de memoria para almacenar el dato con el que se inicializo.
A la hora de asignar el valor de una variable a otra se realizará una copia del dato. 

- Variables Objeto
Las variables de tipo referencia a objetos (Variables objeto), son variables más complejas ya que hacen referencia al espacio de memoria destinado a almacenar la información de dicha variable. A la hora de crear este tipo de variable se necesita el operador new.
A la hora de asignar el valor de un objeto a otro objeto del mismo tipo no se realiza una copia de los datos, sino que ambas variables apuntan al mismo espacio de memoria. Esto quiere decir que si se modifica el dato en una en la otra también (no se tienen dos objetos).

# Tipos de datos

## Básicos
Los tipos de datos primitivos en Java son aquellos que se definen por el lenguaje y que se utilizan para representar valores simples. Hay ocho tipos de datos primitivos en Java:

<table>
  <tr>
    <th>Tipo</th>
    <th>Valores</th>
    <th>Intervalo</th>
    <th>Ejemplo</th>
  </tr>
  <tr>
    <td>boolean</td>
    <td>True/False</td>
    <td>-</td>
    <td>true</td>
  </tr>
  <tr>
    <td>byte</td>
    <td>Entero 8 bits</td>
    <td>-128 a 127</td>
    <td>39</td>
  </tr>
  <tr>
    <td>short</td>
    <td>Entero de 16 bits</td>
    <td>-32768 a 32768</td>
    <td>780</td>
  </tr>
  <tr>
    <td>int</td>
    <td>Entero de 32 bits</td>
    <td>-2147483648 a 2147483647</td>
    <td>59400</td>
  </tr>
  <tr>
    <td>long</td>
    <td>Entero de 64 bits</td>
    <td>-9223372036854775808 a 9223372036854775808</td>
    <td>20000000</td>
  </tr>
  <tr>
    <td>float</td>
    <td>Decimal de 32 bits</td>
    <td>-</td>
    <td>45.6f</td>
  </tr>
  <tr>
    <td>double</td>
    <td>Decimal de 64 bits</td>
    <td>-</td>
    <td>80.4</td>
  </tr>
  <tr>
    <td>char</td>
    <td>Código Unicode de 16 bits</td>
    <td>-</td>
    <td>´@´</td>
  </tr>
<table>

### Enteros

Es el tipo básico encargado de almacenar datos numéricos. El tipo básico más usado es el de tipo INT, ya que principalmente se usan para controlar bucles, indexar matrices o realizar operaciones matemáticas enteras generales. En caso de necesitar un intervalo mayor lo más recomendable de usar es el tipo long.

### Flotantes (Float)

Tipo básico encargado de almacenar y representar los números con componentes fraccionales, divididos en dos tipos float y double. El tipo más recomendado para usar es el tipo double ya que casi todas las funciones matemáticas devuelven valores double.

### Carácter

Java no almacena los caracteres en unidades de 8bits como hace otros lenguajes, java almacena dicha información usando el sistema Unicode, el cual define un conjunto de caracteres asociados al valor de una letra humana (código ASCII)

### Boolean 

El tipo básico boolean se encarga de almacenar los valores true/false mediante el uso de las palabras reservadas (true/false).

### Literales

Los literales son representaciones directas y concretas de valores en el código fuente. 
Los literales numéricos se puede representar de manera decimal, octal, hexadecimal y binario. 
Se puede usar el carácter _ a la hora de definir el valor numérico de una variable, pero tenemos que tener en cuenta las siguientes reglas.
- No se puede usar ni al principio, al final o junto al punto decimal
  *	Int n = _345;
  * double d =45._9;
  *	long in = 234_;
-	Los literales numéricos por defecto son int, para que lo sean debemos de indicarlo con la letra l, ej. 345l
-	Los literales decimales por defecto son double, si queremos que sean float debemos de indicarlo con una f

## Complejos (Objetos)

Son cualquier objeto de cualquier clase java, se maneja igual que los tipos básicos (mediante el uso de variables, cuyo tipo es la clase). Los valores que almacenan son la referencia del espacio de memoria que está asociado al objeto. Mediante el uso de variables se puede acceder a los métodos de los objetos. No se puede hacer conversión ni implícita ni explicita entre los tipos primitivos y los objetos.

### Creación de un objeto y ciclo de vida de los objetos

Para poder crear un objeto se debe de usar el operador new seguido del constructor de la clase. Al realizar esta operación obtenemos la referencia al objeto almacenado en nuestra variable de clase.

¿Qué es un constructor de una clase?

Un constructor es un método especial en una clase de Java que se utiliza para inicializar objetos de la clase recién creados. El constructor tiene el mismo nombre que la clase y no devuelve ningún valor, ni siquiera void. Se llama automáticamente cuando se crea una instancia de la clase utilizando la palabra clave "new".

En general, los constructores se utilizan para inicializar los campos de datos de la clase y para realizar cualquier otro tipo de inicialización que pueda ser necesaria antes de que el objeto esté listo para ser utilizado. Por ejemplo, un constructor puede inicializar valores predeterminados para los campos de la clase o puede tomar argumentos y utilizarlos para inicializar los campos de datos de la clase.

Es importante tener en cuenta que, si no se proporciona un constructor en una clase de Java, se creará un constructor predeterminado automáticamente. El constructor predeterminado no realiza ninguna acción específica y simplemente inicializa todos los campos de datos con sus valores predeterminados.

Puede darse el caso de que se den constructores sobrecargado es un constructor que tiene el mismo nombre que otro constructor en la misma clase, pero con diferentes parámetros. Es decir, se define un constructor sobrecargado cuando se quiere proporcionar varias maneras de inicializar un objeto de una clase.

Cuando se llama al constructor, el compilador de Java determina cuál constructor se debe utilizar basándose en el número y tipo de argumentos proporcionados en la llamada al constructor. Si se proporcionan argumentos que coinciden con la firma de un constructor sobrecargado, entonces ese constructor será el que se utilizará para crear el objeto.

Los constructores sobrecargados permiten que una clase tenga múltiples formas de crear un objeto, cada una con diferentes combinaciones de valores iniciales. Por ejemplo, una clase de "Coche" puede tener un constructor que tome el modelo, la marca y el año de fabricación como argumentos, y otro constructor que tome solo el modelo y la marca como argumentos. En este caso, el primer constructor se utilizaría si se conocen todos los detalles del coche, mientras que el segundo constructor podría utilizarse si solo se conocen el modelo y la marca

¿Cómo se destruye un objeto?

Para destruir un objeto en Java, es necesario que el objeto ya no sea referenciado por ninguna variable y no esté siendo utilizado en ningún lugar del programa.

Java tiene un mecanismo de recolección de basura automático que se encarga de eliminar los objetos que ya no son utilizados. Cuando un objeto queda sin referencias, es decir, no hay ninguna variable que apunte a él, el recolector de basura lo identifica como un objeto que puede ser eliminado y lo elimina de la memoria, es decir, se pone en marcha el recolector de basura (Garbage Collector).

Sin embargo, también se puede destruir un objeto manualmente usando el método finalize(). Este método es llamado por el recolector de basura justo antes de eliminar el objeto. Si un objeto tiene un método finalize() definido, éste puede ser utilizado para realizar tareas de limpieza o liberar recursos antes de que el objeto sea eliminado. Deberemos de tener en cuenta que este método puede ser llamado una o ninguna vez.
 
¿Qué es el recolector de basura?

El Garbage Collector (recolector de basura, en español) es un componente de la máquina virtual de Java (JVM) que se encarga de administrar la memoria en tiempo de ejecución y liberar la memoria utilizada por objetos que ya no están siendo referenciados por el programa.

En Java, los objetos se crean en el heap, una región de memoria dinámica que está separada del stack, que se utiliza para almacenar variables locales y otros datos de la pila. A medida que se crean objetos, se van asignando espacios de memoria en el heap, y a medida que el programa utiliza estos objetos, el heap va creciendo en tamaño. Sin embargo, cuando un objeto ya no es referenciado por el programa, es decir, ninguna variable apunta a ese objeto, ese espacio de memoria ya no se utiliza y se puede liberar para otros usos.

Es aquí donde entra en acción el Garbage Collector. El Garbage Collector es un proceso en segundo plano que se encarga de monitorear los objetos que están siendo utilizados por el programa. Cuando detecta un objeto que ya no está siendo referenciado por ninguna variable, marca ese objeto como elegible para ser eliminado. Luego, en algún momento posterior, el Garbage Collector se encargará de liberar la memoria utilizada por ese objeto y de recuperar el espacio en el heap.

## Conversión de tipos

El objetivo de las conversiones son la transformación de un tipo a otro tipo, existen dos tipos de conversión. Solo el tipo boolean no puede ser convertido de ninguna manera.

-	Conversión implícita: La conversión implícita se realiza automáticamente por el compilador de Java cuando un tipo de dato se asigna a otro tipo compatible.  En caso de no poder realizarse se lanzará una excepción.
Por ejemplo: 
```java
int x = 10; 
double y = x; // conversión implícita de int a double
```
- Conversión explícita: La conversión explícita se realiza mediante una operación de casting y se usa cuando se requiere convertir un tipo de dato en otro tipo no compatible. El casting se realiza colocando el tipo de destino entre paréntesis antes de la variable a convertir.

Por ejemplo:
```java
double x = 3.14;
int y = (int) x; // conversión explícita de double a int mediante casting
```

Es importante tener en cuenta que la conversión explícita puede provocar la pérdida de información o la truncación de datos en algunos casos, por lo que se debe usar con precaución.

### Clases envoltorio

En Java, las clases envoltorio (también conocidas como clases wrapper) son clases que envuelven tipos de datos primitivos para permitir que se comporten como objetos.

Esto significa que los tipos de datos primitivos, como int, boolean y float, pueden ser convertidos en objetos utilizando las clases envoltorio correspondiente, como Integer, Boolean y Float, respectivamente. Estas clases envoltorio proporcionan métodos útiles para trabajar con estos tipos de datos de una manera más orientada a objetos, como la conversión de valores, la comparación de valores y la realización de operaciones matemáticas.

Además, las clases envoltorio también son útiles para trabajar con colecciones de datos en Java, ya que las colecciones, como List y Set, requieren objetos en lugar de tipos de datos primitivos. Al utilizar las clases envoltorio, los tipos de datos primitivos pueden ser encapsulados en objetos y almacenados en colecciones. Por norma general los objetos de las clases de envoltorio son inmutables, no se pueden modificar.Las clases envoltorio cuentan con métodos estáticos que permiten la conversión explicita a otros tipos de datos.

¿Qué es el autoboxing/unboxing?

El autoboxing es un proceso automático en Java que convierte tipos de datos primitivos en objetos de las clases envoltorio correspondiente sin necesidad de realizar una conversión explícita. En otras palabras, cuando se utiliza una variable de tipo primitivo en un contexto en el que se espera un objeto de una clase envoltorio, el autoboxing convierte automáticamente el tipo de datos primitivo en un objeto de la clase envoltorio correspondiente.
Ejemplos 
```java
  Integer ent = 200;
  Double db = 45.7;
```
El unboxing en Java es el proceso mediante el cual un objeto de una clase envoltorio es convertido de nuevo a su tipo de dato primitivo correspondiente. En otras palabras, cuando se tiene un objeto de una clase envoltorio y se necesita utilizar su valor primitivo, el unboxing convierte automáticamente el objeto en su valor primitivo correspondiente. Ej. Int n = ent;

### Secuencia de escape de caracteres

En Java, una secuencia de escape de caracteres es una combinación de caracteres que se utiliza para representar caracteres especiales en una cadena de texto. Las secuencias de escape comienzan con un carácter de escape (una barra invertida ""), seguido de uno o más caracteres que representan el carácter especial deseado.

<table>
  <tr>
    <th>Secuencia de escape</th>
    <th>Descripcion</th>
  </tr>
  <tr>
    <td>\'</td>
    <td>Comilla simple</td>
  </tr>
  <tr>
    <td>\"</td>
    <td>Comilla doble</td>
  </tr>
  <tr>
    <td>\\</td>
    <td>Barra invertida</td>
  </tr>
  <tr>
    <td>\r</td>
    <td>Retorno de carro</td>
  </tr>
  <tr>
    <td>\n</td>
    <td>Nueva línea</td>
  </tr>
  <tr>
    <td>\f</td>
    <td>Salto de formulario</td>
  </tr>
  <tr>
    <td>\t</td>
    <td>Tabulación horizontal</td>
  </tr>
  <tr>
    <td>\b</td>
    <td>Retroceso</td>
  </tr>
  <tr>
    <td>\ddd</td>
    <td>Constante octal (donde ddd es la constante octal)</td>
  </tr>
  <tr>
    <td>\uxxxx</td>
    <td>Constante hexadecimal (donde xxxx es la constante hexadecimal)</td>
  </tr>
</table>

# Inicialización por defecto

Las variables dependiendo del ámbito de uso se pueden inicializar por defecto o no.
Cuando se tratan de variables locales, NO se inicializan por defecto, ya que es necesario asignarles un valor antes de utilizarlas.

Cuando se tratan de variables de clase o de atributo si se inicializan por defecto, según el tipo de variable se inicializan con estos valores:

-	Enteros: 0
-	Decimales 0.0
- Boolean false.
-	Char ‘\u0000’ (carácter nulo).
-	Objeto null.

# La indiferencia de tipo

La indiferencia de tipo, también conocida como "type erasure" en inglés, es un concepto importante en Java que se refiere a la forma en que se manejan los tipos genéricos en tiempo de compilación y en tiempo de ejecución. En Java, los tipos genéricos son una característica que permite a los programadores escribir código que pueda funcionar con diferentes tipos de datos. Por ejemplo, en lugar de escribir un método que funcione solo con listas de enteros, se puede escribir un método genérico que funcione con listas de cualquier tipo de objeto.

No pueden ser valores nulos, siempre tienen que venir inicializadas, ya que si no tiene valor el compilador no es capaz de saber o identificar el tipo que almacena la variable.

No se puede realizar las inicializaciones múltiples (var a, c = 10 ó var b=5, x=30), tampoco vale con la inicialización abreviada de los arrays.
Fue incorporada en Java 10 y consiste en declarar variables locales usando la palabra reservada var, Ej. var num = 100; 

# Operadores aritméticos, asignación, envoltorio, ternarios y lógicos.

## Operadores aritméticos

Los operadores aritméticos son aquellos que se utilizan para realizar operaciones matemáticas básicas.

- Operador de suma (+)
- Operador de resta (-).
- Operador de multiplicación (*).
- Operador división (/).
- Operador módulo de la división (%).
- Operador de incremento (++): se utiliza para aumentar el valor de una variable en uno.
- Operador de decremento (--): se utiliza para restar el valor de una variable en uno.
  * Delante de la variable: se realiza primero la operación y luego se lo asigna a la variable el resultado.
  * Detrás de la variable: primero se asigna el valor a la variable y luego se opera.

## Operadores asignación

Los operadores de asignación de resultados, son operadores que se encargan de realizar las operaciones y asignarles el resultado directamente a la variable
- Operador de asignación de suma (+=). 
- Operador de asignación de resta (-=). 
- Operador de asignación de multiplicación (*=). 
- Operador de asignación de división (/=). 
- Operador de asignación de modulo (%=).

## Operadores envoltorio

Los operadores lógicos de igualdad que se utilizan a la hora de usarlo con objetos son == o equals.

Operador == se encarga de comparar la referencia de los objetos, es decir, solo retornara el valor true cuando ambas variables apuntan a la misma instancia de objeto.

Operador/método equals:  lo tienen todas las clases objeto java, ya que es un método propio de la clase objetc. Su función es comparar el contenido de dos variables y retorna verdadero sin son iguales. Deberemos de tener en cuenta que detecta entre mayúsculas y minúsculas.

Operador/método equalsIgnoreCase: realiza la misma función que equal salvo que aquí ignora las mayúsculas y minúsculas, solo lo posee la clase String, no es propio de la clase object.


## Operador ternario

El operador ternario es una forma abreviada de escribir una instrucción condicional if-else en una sola línea del código. La sintaxis del operador ternario es la siguiente 

- Variable = (expresión booleana) ? valor si verdadero : valor si falso;

El principal motivo del uso del operador ternario es hacer que el código sea más conciso y fácil de leer en situaciones donde una instrucción condicional simple es suficiente, sin embargo, se debe de tener cuidado al utilizarlo en situaciones más complejas, ya que puede hacer que el código sea menos legible si se usa en exceso o se anida demasiado.

## Operadores lógicos

Los operadores de condicionales son operadores ternarios que permiten evaluar una expresión booleana y producir un resultado en función del resultado de la evaluación.
- Operador menor (<). 
- Operador mayor (>). 
- Operador menor o igual (<=). 
- Operador mayor o igual (>=). 
- Operador igual (==). 
- Operador distinto de igual (!=).

Los operadores lógicos son símbolos especiales que se utilizan para combinar expresiones lógicas y producir un resultado lógico. Hay tres operadores lógicos principales en Java: AND lógico (&&), OR lógico (||) y NOT lógico (!).

El operador new encargado de obtener la referencia del espacio de memoria de un objeto.

El operador instanceof encargado de evaluar si un objeto es del tipo dado, retorna un boolean.

Los operadores lógicos de cortocircuito son aquellos operadores que permiten evaluar una expresión booleana de manera eficiente y rápida, deteniendo la evaluación de la expresión en cuanto se determina el resultado final. Los operadores lógicos de cortocircuito son && (AND lógico de cortocircuito) y || (OR lógico de cortocircuito).

La diferencia entre los operadores lógicos de cortocircuito y los operadores lógicos normales (& y |) es que los operadores de cortocircuito no evalúan el segundo operando si el primer operando ya proporciona suficiente información para determinar el resultado de la expresión completa. Esto puede ser útil para mejorar la eficiencia y evitar errores en la evaluación de expresiones complejas. Por ejemplo, si se tiene la siguiente expresión:

```java 
if (a > 0 && b < 10) {
    // código si se cumple la expresión
}
```
El operador && permite cortocircuitar la evaluación de la expresión en cuanto se determina que a es menor o igual a cero, ya que independientemente del valor de b, la expresión completa no puede ser verdadera. De esta manera, se evita la evaluación innecesaria de la segunda parte de la expresión, lo que puede mejorar la eficiencia del código.
De manera similar, si se tiene la siguiente expresión:

``` java
if (a == null || a.isEmpty()) {
    // código si se cumple la expresión
}
```

El operador || permite cortocircuitar la evaluación de la expresión en cuanto se determina que a no es nulo y no está vacío, ya que independientemente del valor de la segunda parte de la expresión, la expresión completa ya es verdadera. De esta manera, se evita la evaluación innecesaria de la segunda parte de la expresión, lo que puede mejorar la eficiencia del código.

# String
En Java, los objetos String son inmutables, lo que significa que una vez creados, no se pueden modificar. Si se intenta modificar un objeto String, lo que realmente ocurre es que se crea un nuevo objeto String con el resultado de la operación de modificación.

Por ejemplo, en el siguiente código:
``` java
String str = "Hola";
str = str + " Mundo";
```

Primero se crea un objeto String con el valor "Hola", y luego se crea un nuevo objeto String con el resultado de concatenar " Mundo" al final de "Hola". Finalmente, la variable str se actualiza para apuntar al nuevo objeto String creado.

Esta inmutabilidad de los objetos String tiene algunas ventajas, por ejemplo:
- Seguridad en la programación concurrente: como los objetos String son inmutables, no es posible que varios hilos de ejecución modifiquen el mismo objeto String al mismo tiempo, lo que puede evitar problemas de concurrencia.
- Facilidad de uso: al ser inmutables, los objetos String pueden ser usados de manera segura sin preocuparse de que su contenido sea modificado inesperadamente.

Sin embargo, también puede tener algunas desventajas en situaciones donde se realizan muchas operaciones de modificación de cadena, ya que en estos casos se pueden generar muchos objetos String temporales, lo que puede afectar el rendimiento del programa.

Esto no funciona para las cadenas usadas con StringBuilder ya que tiene que ser a través de sus métodos.
 
## Igualdad de StringBuilder
StringBuilder es una clase en Java que se utiliza para crear y manipular cadenas de texto de manera eficiente. La clase StringBuilder es similar a la clase String, pero en lugar de crear una nueva instancia de cadena cada vez que se realiza una operación de concatenación o modificación de cadena, la clase StringBuilder modifica la misma instancia de cadena, lo que puede mejorar significativamente el rendimiento y la eficiencia en situaciones donde se realizan muchas operaciones de concatenación o modificación de cadena.

No sobrescribe el método equals por lo que el resultado == y equals producen el mismo efecto. Solo es verdadero cuando apuntan al mismo objeto.

```java
StringBuilder sb1 = new StringBuilder("Hola");
StringBuilder sb2 = new StringBuilder("Hola");
StringBuilder sb3 = sb1;
System.out.println(sb1.equals(sb2)); // Imprime false, porque los contenidos de los objetos son iguales, pero las referencias son diferentes
System.out.println(sb1 == sb2); // Imprime false, porque las referencias apuntan a objetos diferentes
System.out.println(sb1 == sb3); // Imprime true, porque ambas referencias apuntan al mismo objeto.
```
## Pool de objetos (caracteres, integer, double)
En Java, un pool de caracteres (también conocido como String pool o pool de cadenas) es un espacio en memoria donde se almacenan las cadenas de texto que son creadas en un programa Java. Es una optimización de Java que permite reutilizar cadenas de texto que ya han sido creadas previamente, en lugar de crear nuevas instancias de esas cadenas cada vez que se necesitan. 

Cuando se crea una cadena de texto en Java utilizando comillas dobles (") o el operador de concatenación (+), Java busca en el pool de caracteres si ya existe una cadena con el mismo valor. Si existe, en lugar de crear una nueva instancia de la cadena, Java devuelve una referencia a la instancia existente en el pool de caracteres. Si no existe, Java crea una nueva instancia de la cadena y la agrega al pool de caracteres.

El uso del pool de caracteres puede mejorar significativamente el rendimiento y la eficiencia de una aplicación Java que utiliza cadenas de texto, ya que evita la creación innecesaria de nuevas instancias de cadenas de texto que ya existen en el pool.
Por ejemplo, si se tiene el siguiente código:
``` java
String a = "Hola";
String b = "Hola";
String c = new String("Hola");
System.out.println(a == b); // imprime true
System.out.println(a == c); // imprime false
```
En este caso, se crea la cadena "Hola" dos veces: una vez utilizando comillas dobles y otra vez utilizando el constructor new String(). Sin embargo, debido al pool de caracteres, las variables a y b apuntan a la misma instancia de la cadena "Hola" en el pool, mientras que la variable c apunta a una nueva instancia de la cadena "Hola" creada utilizando el constructor new String(). Por lo tanto, la comparación a == b devuelve true, mientras que la comparación a == c devuelve false.

# Estructuras de control

Las instrucciones de control son sentencias que permiten controlar el flujo de ejecución de un programa. Estas instrucciones se dividen en tres categorías:
- Instrucciones de selección o condicionales
-	Instrucciones de iteración o de bucle.
-	Instrucciones de acceso o salto.

## Instrucción IF.

La función principal del if es evaluar la condición de tipo boolean y ejecutar el bloque de la sentencia si cumple la condición boolean. Las llaves solo serán obligatorias solo si el bloque contiene más de una instrucción. 

Opcionalmente una sentencia if puede contener un bloque else. Bloque que solo se ejecutara cuando la condición evaluada en el if no sea correcta.
Pueden darse el caso del uso de if anidados, es decir, múltiples if seguidos.
Puede combinarse el uso de if con condiciones if-else-if

## Instrucción Switch.
Permite la evaluación múltiple de una expresión insertada como parámetro.
Switch es más óptimo y legible frente a la anidación de múltiples if, porque principalmente lee todos los resultados del condicional switch y si encuentra uno ejecuta el bloque de código que este asociado a ese resultado de evaluación. En versión anterior de JDK7 el parámetro de evaluación era un tipo básico numérico, pero a partir de esa versión se pueden evaluar también cadenas de caracteres. 

Cuando una expresión coincide con uno de los valores indicados en los case, se ejecutará el bloque correspondiente de la sentencia, sino se ejecutará el bloque default que ejecutara el bloque cuando se produce este tipo de situaciones, este bloque es opcional.

Dentro de cada bloque case se puede indicar la salida de la instrucción (break) de manera opcional, esto permite finalizar la ejecución del switch. Se pueden tener switch anidados. El valor de los case solo podrán ser literales o constantes.

# Estructuras de repetición

## Bucle for
Un bucle for es una estructura de control de flujo en la programación que permite iterar sobre un conjunto de valores conocido previamente. En otras palabras, es una forma de repetir un bloque de código varias veces, una vez por cada elemento de un conjunto.
Deberemos de tener en cuenta los siguientes aspectos:
-	Las llaves son obligatorias si hay más de una instrucción
-	La sentencia de control siempre debe de ser el resultado un boolean.
-	Las instrucciones de control pueden contener más de una sentencia, separada por una coma. Ej. 
```java
for(int a =0, b =10; a<b; a++, b--)
```
- Las tres instrucciones de control son opcionales
```java
int i = 1;
for (;i<10;) {
	System.out.println(i);
	i++;
}
```
### Variantes del bucle for: Enhanced for (foreach)

En Java, el bucle foreach (también conocido como "bucle for-each") es una forma simplificada de iterar sobre los elementos de un arreglo o una colección, sin necesidad de utilizar un contador o un índice para acceder a cada elemento.
Ej. 
```java
for (tipoDeDato variable : arreglo o colección) {}
```

## Bucle while

El bucle while es una estructura de control de flujo que permite repetir un bloque de código mientras se cumple una determinada condición. El bucle while se utiliza cuando no se sabe el número exacto de veces que se debe repetir un bloque de código, pero se sabe que la repetición debe continuar mientras se cumpla una determinada condición. La condición puede evaluarse al principio, o después de ejecutar el bloque de instrucciones (variante do-While). Las acciones dentro del bloque provocaran que en algún momento la condición deje de cumplirse, sino se considerara un bloque infinito.

La sintaxis básica del bucle while es la siguiente:
```java
while (condición) {
  // instrucciones
}

do {
  //instrucciones
}while(condición)
```
## Break y continue
Son operaciones que alteran el funcionamiento básico de un bucle.
- Break fuerza la salida del bucle
- Continue fuerza a pasar la siguiente iteración
En caso de usar estas sentencias en la ejecución de bucles anidados debemos de tener en cuenta que si no indicamos nada la sentencia break/continue afecta al bucle mas interno pero si queremos cambiar este comportamiento deberemos de indicar un alias/etiqueta para que afecte al bucle que queramos.

# Programación Orientada a objetos

## Métodos.
Son funciones que se encargan de realizar una tarea. Pueden recibir parámetros y devolver un resultado.

Su estructura es (visibilidad) modificador tipo de retorno (si no retorna nada será void) nombre del método(parámetros) {}.

Los métodos se definen dentro de clases, para llamarlo se debe de crear un objeto de la clase y utilizar la sintaxis objeto.metodo(argumentos). En caso de que el método que queramos usar está dentro de la misma clase no es necesario crear un objeto.

Un método se puede sobrecargar, que quiere decir esto, que podemos tener el mismo método, pero con diferentes parámetros de entrada (en cantidad o tipo). El tipo de devolución no afecta en la sobrecarga, puede ser el mismo o diferente. 

Cuando hay varios posibles métodos que se pueden ejecutar con la llamada, primero se intenta obtener una coincidencia exacta, después promoción de tipos (por ejemplo, de int buscar long) y en último lugar autoboxing.

### Paso de parámetros

Al pasar un tipo primitivo a un método, estamos pasando una copia del dato, si el método modifica su contenido, solo afecta a la copia no al original. Al pasar un tipo objeto a un método, estamos pasando la referencia del objeto, esto quiere decir que si modificamos algún dato tanto la copia como el original se actualizara la información, para el caso de los String no funciona igual ya que son inmutables.
 
## Miembros estáticos

Los métodos estáticos (también conocidos como métodos de clase) son aquellos que pertenecen a una clase en particular en lugar de pertenecer a una instancia (objeto) de la clase. Estos métodos son llamados "estáticos" porque su comportamiento y resultado son predecibles y no dependen del estado de los objetos creados a partir de la clase.

Los métodos estáticos se pueden utilizar para realizar cálculos, manipulaciones de datos o cualquier otra tarea que no dependa del estado actual de los objetos de la clase. Debido a que no dependen del estado de los objetos, los métodos estáticos no tienen acceso a las variables de instancia y no pueden hacer referencia al operador "this" en el cuerpo del método.

Un método estático solo puede llamar a métodos y atributos que también sean estáticos (no se pueden usar en su interior ni this ni super).

Para llamar a un método estático, no es necesario crear una instancia de la clase. En su lugar, el método se llama directamente en la clase, seguido del nombre del método y cualquier argumento que se requiera, aunque se puede usar con una instancia de la clase. Se declaran con la palabra static.

## Variables y bloques estáticos

Las variables estáticas compartidas por todos los objetos de la clase, se definen con la palabra static. Todos los objetos inicializados comparten el mismo valor.
Los bloques estáticos se ejecutan una vez durante la vida de una clase, solo pueden acceder a otros miembros estáticos.

## Constructores

Un constructor es un método especial que se llama automáticamente cuando se crea una instancia (objeto) de una clase. El constructor se utiliza para inicializar los valores de los atributos de la clase cuando se crea un objeto de esa clase.

Cuando creamos un objeto no es necesario definir un constructor, ya que de forma explícita en una clase el compilador agrega uno por defecto, que no tiene parámetros y tampoco ninguna instrucción. Pero si se define explícitamente un constructor, el compilador no crea el constructor por defecto.

Los constructores tienen el mismo nombre que la clase y no tienen tipo de retorno. Pueden tener parámetros o no, y se pueden sobrecargar (tener varios constructores con diferentes parámetros).

Un constructor puede llamara a otro constructor de la misma clase utilizando la expresión this(argumentos), debe de ser la primera instrucción del constructor.

Se pueden definir bloques de inicialización de instancia. Son bloques de código que se ejecutan cada vez que se crea un objeto de la clase, antes del constructor, se delimita por llaves.

## This

"this" es una palabra clave que se utiliza dentro de una clase para hacer referencia al objeto actual (la instancia de la clase en la que se está trabajando).

La palabra clave "this" se utiliza principalmente en dos situaciones:
Para referirse a un atributo o método de la clase actual: Cuando hay un atributo o método con el mismo nombre que un parámetro local, se puede utilizar "this" para hacer referencia al atributo o método de la clase actual.

Para llamar a otro constructor de la misma clase: Cuando una clase tiene varios constructores, se puede utilizar "this" para llamar a otro constructor de la misma clase.

## Modificadores de acceso

Los modificadores de acceso determinan la visibilidad de una clase y sus miembros.

<table>
  <tr>
    <th>Public</th>
    <hd>Protected</th>
    <th>Default</th>
    <th>Private</th>
  </tr>
  <tr>
    <td>SI</td>
    <td>NO</td>
    <td>SI</td>
    <td>NO</td>
  </tr>
  <tr>
    <td>SI</td>
    <td>SI</td>
    <td>SI</td>
    <td>SI</td>
  </tr>
  <tr>
    <td>SI</td>
    <td>SI</td>
    <td>SI</td>
    <td>SI</td>
  </tr>
  <tr>
    <td>SI</td>
    <td>SI</td>
    <td>SI</td>
    <td>SI</td>
  </tr>
</table>

- Public
Si una clase o miembro de la misma es public, puede utilizarse desde cualquier clase que esté en su mismo paquete o en cualquier otro. Es poco común ver que los atributos sean públicos ya que no cumplirían la encapsulación, solo son públicos si se trata de constantes.

-	Default
Es el ámbito que se aplica cuando no se indica ningún modificador. El elemento que lo lleve solo será visible desde clases de su mismo paquete.

- Private
Solo es accesible desde el interior de la clase. Muy habitual en atributos para encapsulación.

## Encapsulación

Principio que se basa en mantener como privados los atributos que definen características de un objeto, proporcionando acceso a los datos a través de métodos y constructores, evitando así corromper los objetos.

Se accede a los atributos mediante los métodos getter y setter y mediante el constructor permite inicializar los atributos durante la creación del objeto.
 
## Clases abstractas

Es una clase que cuenta, al menos, con un método abstracto, que es aquel que esta declarado en la clase, pero no implementado. Las clases abstractas se definen con la palabra reservada abstract. 
Las clases abstractas tienen una serie restricciones, estas son:
- No es posible crear objetos de una clase abstracta
-	Pueden incluir atributos, constructores, métodos estándar aparte de los métodos abstractos.
-	Una clase que herede una clase abstracta esta obligada a sobrescribir los métodos
abstractos heredados (o declararse también como abstract).
-	El objetivo de los métodos abstractos es forzar a que todas las subclases tengan el mismo
formato de método.

## Método abstracto vs final

Un método final es lo contrario a un método abstracto, ya que un método final es aquel que no puede ser sobrescrito, ya que utiliza la palabra reservada final.

## Interfaces

Una interfaz es un conjunto de métodos abstractos y su objetivo es definir el formato de ciertos métodos, que posteriormente las clases se encargan de implementar. También puede incluir constantes que serán públicas y estáticas. Aunque no se especifique los métodos puede ser abstractos y públicos., en el caso de las constantes se omiten las palabras public final y static.

Las interfaces se definen usando la pablara reservada interface. Todas las clases que implemente una interfaz está obligada a sobrescribir(implementar) todos los métodos de la misma. Para implementar una interfaz deberemos de usar la palabra reservada implements.

Las interfaces nos dan una flexibilidad enorme ya que podemos implementar varias interfaces o heredar de una clase padre que implemente una o varias interfaces. 

Además, una interfaz puede heredar de otra interfaz. En caso de que una clase la implemente tendrá que sobrescribir todos los métodos de las interfaces que herede dicha interfaz.
Todos los métodos de la interfaz deben de ser públicos, en caso de no estar definida la palabra public su comportamiento por defecto es public.

### Interfaces posteriores a Java 8 y 9

Las nuevas versiones de java han proporcionado una implementación por defecto, que puede ser utilizada por las clases que implementan la interfaz, estos métodos se definen usando la palabra reservada default. Se usan para métodos genéricos que no queremos que las clases que la implementen tengan que volver a realizarlo, pero en caso de que no se desee este funcionamiento se puede sobrescribir.

Existe un problema de herencia múltiple, este caso se da cuando tu clase implementa dos interfaces con dos métodos default iguales en cada interfaz, esto va a provocar un error de compilación, para solventarlo deberemos de sobrescribir el método en nuestra clase.

Se pueden definir métodos estáticos en las interfaces, pero no están disponibles en la clase que implementa (sobrescribir) la interfaz y no podemos llamarlo con la propia clase ni con la instancia, solo puede llamarse usando la propia interfaz.

Se pueden definir métodos privados en las interfaces. Esta funcionalidad se aplica principalmente para dar soporte a los métodos default que tiene nuestra interfaz.
Interfaces funcionales

Las interfaces funcionales son aquellas interfaces que solo poseen un método abstracto, lo curioso de esta nueva funcionalidad es la implementación de las mismas sin necesidad de crear clases, sino a través de expresiones lambda. Para detectar que nos encontramos ante una interfaz funcional deberemos de buscar la anotación @FunctionalInterface (no es obligatorio).

Si una interfaz cuenta con métodos que heredan de la clase objeto no cuentan para determinar si una interfaz es funcional o no. 

## Herencia

La herencia es un concepto fundamental de la programación orientada a objetos que permite crear nuevas clases basadas en clases existentes. En la herencia, una clase de hija (subclase) hereda características y comportamientos de una clase padre (superclase), ya que esta primera puede utilizar todos los campos y métodos de su clase padre, además de poder agregar nuevos campos y métodos o sobrescribir (modificar) los que ya existen.

La herencia en java se implementa utilizando la palabra clave extends, debemos de tener en cuenta que solo se puede heredar de una sola clase, aunque una superclase puede heredar a su vez a otra y así hasta n niveles, creando una jerarquía de clases. Por otro lado, solo se podrá usar el concepto de herencia en aquellas clases que no sean final.

A la hora de la privacidad una hija nunca va a poder ver los miembros privados de la superclase.

### Herencia de Object

Por defecto java aplica a la hora de crear objeto la herencia de la clase Object de manera directa o indirectamente. Como se aplica este concepto de la siguiente manera. Si la clase no hereda explícitamente de otra clase implícitamente heredará de Object. Esta herencia nos permite el uso de los métodos toString, equals y hashCode.

### Los constructores por herencia.

Todas las clases incluyen de forma implícita en sus constructores como primera línea de código la instrucción super();, que es una línea de ejecución que permite realizar la llamada al constructor de la clase padre en la clase hija. 

Podemos seleccionar a que constructor padre podemos ejecutar usando la instancia super y le pasamos el número de parámetros que necesite con su tipo correspondiente.

### Sobreescritura de métodos
Es un concepto importante de la programación orientada a objetos que permite a una clase hija proporcionar una implementación diferente para un método que ya esta definido en su clase padre.

A la hora de sobrescribir un método deberemos de seguir una serie de normas:
-	se debe de definir un método con el mismo nombre, parámetros y tipo de retorno del método
-	debe poseer el mismo modificador de acceso o más permisivo (menos restrictivo).
-	La nueva implementación no debe de propagar ninguna excepción que no estén definidas en el original (no afecta a las excepciones Runtime)

Para que el compilador detecte esta nueva implementación tenemos que usar la anotación @Override.

### Uso de protected

El modificador de acceso protected puede utilizarse en la declaración de atributos y métodos. Si uno de estos elementos se declara como protected, significa que es accesible desde cualquier clase de su mismo paquete y de sus subclases, independientemente de donde estas se encuentren. Por tanto, el modificador protected establece una visibilidad a los miembros de una clase que es superior a la default (ámbito de paquete), pero inferior a la public. El acceso desde una subclase a un miembro protected de la superclase se debe hacer siempre dentro del contexto de la herencia.

Sin embargo, si desde una subclase que se encuentre en otro paquete distinto a p1 creamos un objeto de la clase Prueba, no tendremos acceso a los miembros protegidos a través de este objeto. Esto es lo que significa que el acceso solo sea a través del contexto de la herencia.
Instancias por referencia.

### Instancias por referencia.

La instancia por referencia por herencia en Java se refiere a la creación de un objeto de una subclase y asignar una referencia a ese objeto a una variable de referencia de la clase padre. En otras palabras, se crea un objeto de una subclase y se asigna a una variable de referencia de la clase padre, lo que permite que el objeto de la subclase se trate como un objeto de la clase padre.

La instancia por referencia por herencia es útil cuando se quiere utilizar una clase padre como tipo de referencia para objetos de sus subclases, lo que permite una mayor flexibilidad y modularidad en el diseño del programa. Además, esto también facilita la implementación de polimorfismo en Java.

Tendremos que tener en cuenta que el compilador permite a ver casting der una referencia de un tipo a cualquier tipo de sus subclases, pero si el objeto no es de ese tipo se producirá una ClassCastException

## Clases anidadas

En Java, una clase anidada es una clase que se define dentro de otra clase. Las clases anidadas pueden ser de dos tipos: clases internas y clases estáticas anidadas.

Clases internas (Inner classes): Son clases que se definen dentro de otra clase y pueden tener acceso a los miembros (atributos y métodos) de la clase que las envuelve, incluso a los miembros privados. Las clases internas se utilizan principalmente para encapsular la implementación de una clase dentro de otra, y se pueden dividir en cuatro tipos:

-	Clases internas regulares (Member inner classes): Son clases que se definen como miembros de una clase y están asociadas a una instancia de la clase que las envuelve. Pueden acceder a todos los miembros de la clase que las envuelve, incluyendo los miembros privados.
A la hora de instanciar la clase se realiza de la siguiente forma: 
Externa ext = new Externa();
Externa.Interna inter = new ext.new Interna();

-	Clases internas estáticas (Static nested classes): Son clases internas que se definen con la palabra clave static y no están asociadas a una instancia de la clase que las envuelve. Pueden ser accedidas directamente desde la clase que las envuelve, sin necesidad de crear una instancia de la clase externa. A la hora de instancia la clase se realiza de la siguiente forma: Externa.Interna inter = new Externa.Interna();

-	Clases internas locales a métodos: Son clases que se definen dentro de un método o un bloque de código, y solo son accesibles dentro de ese método o bloque de código. Son útiles cuando se necesita una clase que sea local a un método específico, solo tiene acceso a variables que sean finales.

-	Clases internas anónimas (Anonymous inner classes): Son clases internas que se definen sin un nombre y se crean y se instancian al mismo tiempo en que se necesitan. Son útiles para implementar interfaces o clases abstractas de forma rápida y concisa.

Clases estáticas anidadas (Static nested classes): Son clases anidadas que se definen con la palabra clave static y no están asociadas a una instancia de la clase que las envuelve. Son similares a las clases internas estáticas, pero no pueden acceder a los miembros no estáticos de la clase que las envuelve.

Las clases anidadas en Java proporcionan una forma de organizar y encapsular la lógica relacionada en una misma unidad de código, y se utilizan en situaciones específicas donde se requiere una relación cercana entre las clases.
 
## Enumeraciones

Una enumeración (enum) es un tipo de dato especial que permite definir un conjunto fijo de constantes con nombre en un tipo de dato enumerado. Una enumeración en Java se define usando la palabra clave enum y puede contener un conjunto de constantes llamadas "valores enumerados" o "elementos enumerados". Son tipos de datos estáticos y final, lo que significa que las constantes enumeradas son inmutables y no se pueden cambiar una vez que se definen. Las enumeraciones se utilizan comúnmente para representar un conjunto fijo de opciones o valores posibles en un dominio específico.

Las variables de tipo enumerado se pueden utilizar con el operador == para comprobar la igualdad. También pude utilizar en un switch.

Existen enumeraciones compuestas, estas enumeraciones son aquellas que almacenan mas de un dato, para ello se usan los constructores (que son de ámbito privado)
Los enumerados cuentas con métodos propios como:
-	Values(). Método estatico que devuelve un array con todos los valores de la enumeración.
-	Name(). Cadena de caracteres con el nombre del valor.
-	Ordinal(). Posicion del valor dentro de la enumeración, siendo 0 la posición del primero.
-	toString(). Devuelve el mismo resultado que name().

## Clases Genéricas

La programación genérica tiene como objetivo facilitar el desarrollo de algoritmos (o métodos en la POO) de manera tal que el tipo de datos especifico manipulado por el algoritmo sea especificado al momento de ejecutarlo y no al momento de desarrollarlo.
-	Se decalran en clases abstractas o interfaces
-	Pdemos especificar que los tipos extienda de una interfaz con T extends myInterfaces
-	La convención para nombrar los parámetros de tipo es
  *	E – Elemento
  *	K – Llave
  *	N – Numeros
  *	T – Tipo
  *	V – Valor

## Clases Anónimas

Una clase anónima es Java es una solución rápida para implementar una clase abstracta o una interface que solo se va a usar una vez sin necesidad de crea un archivo separado

# Arrays y Colecciones

Conjuntos de datos de un misto tipo a los que se les accede mediante una única variable. Cada dato tiene asociado un índice dentro del array empezando por la posición 0. 

## Arrays unidimensionales y multidimensionales

Un array es una estructura de datos estática una vez definido su tamaño no se puede modificar. Los arrays se declaran de la siguiente manera tipoDato[posiciones] nombre.
Un array se crea como cualquier objeto a través del operador new, indicando entre corchetes el tamaño.
```java
int [] s = new int [20]; // Cada posición del array se inicializa con el valor por defecto (0) o null.
Int [] datos:
int vals [];
```

Para acceder al contenido de una posición se le indica entre corchetes el índice del elemento

El tamaño de un array se obtiene usando el método length, pero la última posición de este será array.lenght -1.

Los array se recorren usando estructuras repetitivas como for y foreach.
Los array multidimensionales es una red de varias dimensiones como su nombre nos indica en dos, tres, cuatro… dimensiones, funcionan igual que los unidemsionales, pero usando dos punteros.
Se pueden declarar de la siguiente manera Int[][] ar; int[]ar1[]; int [][][]ar2;
Existen arrays irregulares, que son aquellos que a la hora de crear un array multidimensionales, se puede dejas las ultimas dimensiones sin asignar tamaño.
A cada posición definida se le puede asignar un array con tantas dimensiones como queden sin tamaño. Importante no se pueden dejar dimensiones intermedias sin asignar tamaño  
ej. 
```java 
Int [][][] h = new int [6][][4]; 
```
Si se inicializa asi en cada posición deberemos de asignar las dimensiones de cada fila
Igual que con los array de una dimensión, un array multidimensional puede declararse, crearse e inicializarse en una única instrucción. Se puede dejar las últimas dimensiones sin asignar tamaño e inicializarlas después.
 
## Genéricos

Los genéricos son aquellas clases que permiten trabajar con cualquier tipo de objeto en lugar de un tipo de objeto específico, es decir una clase genérica puede tomar un tipo de objeto como parámetro de tipo y luego trabajar con ese tipo de objeto dentro de la clase. No pueden ser primitivos. Una clase genérica se define usando el operador diamante con la letra T (<T>).

Ej. 
```java
MyClass<String> mc = new MyClass<>();
```

A la hora de definir un parámetro de tipo genérico, se debe emplear el operador comodín. El método podrá ser llamado con un objeto Bean de cualquier tipo.
Se puede definir una clase que solo admita objetos de un determinado subtipo 
MyClass<T extends Number>{}. Esto quiere decir que la clase no pueda trabajar con cualquier tipo de Java sino solamente con el tipo definido.
Se puede definir parámetros de tipo genéricos se puede utilizar tanto extends como super para establecer restricciones.

Una clase no genérica puede incluir métodos que utilicen un tipo genérico (en parámetros o como resultados). Se incluirá la expresión <T> en la definición del método.

### Iterables

Es un objeto que puede ser recorrido mediante un enhanced for. Los objetos iterables implementan la interfaz java.lang.Iterable, que entre sus métodos más destacados esta Iterator<T> iterato(). Devueleve un objeto Iterator. Las listas y los conjuntos de son ejemplos de objetos iterables.

El objeto tipo cursor que permite recorrer el contenido de un Iterable es Iterator del cual destacan los métodos hasNext (Indica si hay más elementos que recorrer) y next se desplaza al siguiente elemento y devuelve una referencia al mismo.

### Collection

Una colección (Collection) en Java es un objeto que agrupa elementos similares en una estructura de datos única y que se puede utilizar para manipular y almacenar los datos de manera eficiente. Las colecciones proporcionan una manera flexible y conveniente para trabajar con grupos de objetos, como matrices o listas, y ofrecen una amplia gama de funcionalidades para agregar, eliminar, buscar y modificar elementos.

Las colecciones se utilizan comúnmente en Java para almacenar datos de manera dinámica, es decir, sin tener que especificar el tamaño de la colección de antemano. Algunos ejemplos de colecciones incluyen Listas (List), Conjuntos (Set), Mapas (Map), Colas (Queue) y Pilas (Stack). Cada tipo de colección tiene sus propias características y métodos específicos, lo que las hace útiles en diferentes situaciones y aplicaciones.
 
### Listas

Es una agrupación de objetos donde cada elemento tiene una posición asociada a partir del orden de llegada, siendo 0 la posición del primer elemento. Las listas implementa la interfaz List que a su vez implementa Collection. Son colecciones de tipo genérico (preparadas para admitir cualquier objeto Java), La principal clase de colección que se usa es ArrayList.

Las listas generadas con Arrays.asList son listas fijas que no admite inserciones ni eliminaciones.
Las listas generadas con List.of y con List.copyOf(copiar de otra lista) son listas Inmutables, no admite la eliminación, modificación e inserciones de elementos, ni valores null, no permite ordenarlo.

Principales métodos para listas
-	Add(dato): añade el dato a la colección y lo colocal al final de la misma.
-	Add(int pos, dato):  añade el elemento a la posición indicada, desplazando hacia adelante los que se encuentren en dicha posición(las posiciones deben de existir).
-	Set(int pos, dato): sustituye el elemento existente en la posición indicada por el nuevo dato suministrado como parámetro. Devuelve el elemento sustituido.
-	Size(): Devuelve el total de elementos de la colección.
-	Get(int pos): Devuelve el elemento que ocupa la posición indicada. Si la posición es menor que 0 o mayor o igual que size(), se producirá una excepción.
-	Remove(int pos): Elimina el elemento que ocupa la posición indicada y lo devuelve. Si la posición es menor que 0 o mayor o igual que size, se producirá una excepción.
-	Remove(objeto): Elimina el elemento indicado en caso de que exista. Devuelve true si dicho elemento estaba presente en la colección. Si hay más de un elemento, elimina la primera ocurrencia.

Recorrer una lista
-	Un bucle estándar for
-	Un bucle for each
-	Método forEach (usando programación funcional)


### Tablas

En Java, un Map es una colección de elementos que se almacenan como pares clave-valor. Cada elemento en un Map consiste en una clave única que se utiliza para acceder a su valor correspondiente. Los Map son útiles para asociar una clave con un valor, y para recuperar rápidamente el valor asociado con una clave determinada.

Java proporciona varias implementaciones de la interfaz Map, cada una de las cuales tiene diferentes características y se utiliza para diferentes propósitos. Algunas de las implementaciones más comunes incluyen HashMap, TreeMap(ordenados por clave), LinkedHashMap, Hashtable.
 
Los Map se puede generar usando Map.ofEntries() o Map.copyOf(), ambos son inmutables, no admiten la eliminación, modificación e inserción de elemento. No admite ni calves ni valores null.

Principales métodos para mapas
-	Put(clave, valor):Añade el dato a la colección y le asocia la clave indicada como primer parámetro. Si ya existiera esa clave, el valor existente será sustituido por el nuevo. Admite claves null.
-	putIfAbsent(clave, valor): Añade la entrada en caso de que la clave no exista o tenga asociado el valor null.
-	Get(clave): Devuelve el dato que tenga asociada dicha clave. Si no hay ninguno , devolverá null
-	Size(): devuelve el tamaño de la colección
- Remove(clave): elimina el dato que tenga dicha clave asociada y devuelve el elemento eliminado.
-	containsKy(clave):Indica si hay algún elemento en la colección con dicha clave asociada.
-	ContainsValue(valor): Indica si el elemento está presente en la colección.

Recorrer una tabla
-	Usando values (): retorna una lista de los valores, se recorren con for each.
-	Usando keySet(): devuelve el conjunto de claves de la tabla, se recorren con for each.
-	Metodo forEach (usando lambdas).

#### TreeMap

Es similar a HashMap, con la diferencia de que los objetos están ordenados por la clave. Si la clave es numérica se ordenaría de menor a mayor.

### Conjuntos

En Java, un Set es una colección que no permite elementos duplicados. Esto significa que si agregas un elemento a un Set que ya se encuentra en él, el Set no se modificará. La interfaz Set es parte del framework de colecciones de Java y extiende la interfaz Collection. Algunas de las características que distinguen a un Set de otras colecciones son:

-	No se permiten elementos duplicados: si intentas agregar un elemento que ya se encuentra en el Set, no se agregará.
-	No tiene orden específico: los elementos del Set no tienen un orden definido.
-	Operaciones de conjunto: la interfaz Set proporciona métodos para realizar operaciones comunes de conjunto, como la unión, intersección y diferencia.

Existen varias implementaciones de la interfaz Set en Java, como HashSet, LinkedHashSet, y TreeSet. Cada implementación tiene sus propias características y ventajas, por lo que es importante seleccionar la implementación correcta para la tarea que se está realizando.

Los Set se pueden generar usando of y copy, ambos son inmutables, no admiten la eliminación, modificación e inserción de elementos, tampoco valores null.

Principales métodos para los set
-	Add (dato): añade el dato a la colección si no está presente. Devuelve true si lo ha podido añadir
-	Remove(dato): Elimina el elemento si se encuentra en la colección
-	Size: Devuelve el tamaño de la colección
-	Contains: Devuelve true si el objeto existe en la colección.

Recorrer un set
-	Usando for each.
-	Método forEach (usando lambdas).
 
### Colas dobles (Cola y pila)

Un "Deque" (también conocido como "Double Ended Queue") en Java es una estructura de datos que permite la inserción y eliminación de elementos en ambos extremos de la cola. La clase Java "Deque" es parte del paquete "java.util" y se puede usar para implementar una cola doblemente terminada. Esta clase extiende la interfaz "Queue" y proporciona métodos adicionales para agregar y eliminar elementos tanto en el frente como en la parte posterior de la cola. Los métodos "addFirst()" y "addLast()" se utilizan para agregar elementos al principio y al final de la cola, respectivamente. Los métodos "removeFirst()" y "removeLast()" se utilizan para eliminar elementos del principio y del final de la cola, respectivamente. Además de los métodos de cola estándar, la interfaz Deque también proporciona métodos adicionales para acceder a los elementos en ambas direcciones, como "getFirst()" y "getLast()".
 
A la hora de crear un Deque no tenemos métodos de factorías sino que se crean directamente usando el operador new

Principales métodos para los deque
-	Add (dato): añade el dato al final de Deque, comportándose como una cola.
-	Push (dato): Añade el elemento a la cabecera del Deque comportándose como una  pila.
-	poll: Extrae y elimina el elemento de la cabecera.
-	Remove: extra y elimina el elemento de la cabecera.
-	Peek y element: Devuelven el elemento de cabecera, pero sin eliminarlo.
-	Size: Indica el tamaño de la colección.

Recorrer un deque
-	Usando for each.
-	Método forEach (usando lambdas).
 
## Ordenar arrays y listas

Este tipo de colecciones pueden ser ordenados según el orden natural de los objetos. Este orden natural se define a través de la interfaz Comparable, que deberá ser implementada por los objetos que ordena. Si las clases no implementan Comparable, se deberá definir el orden natural en otra interfaz llamada Comparator.

### La interfaz comparable

Es una interfaz con un único método llamado compareTo donde se define la lógica de aplicación. Esta interfaz es implementa por clases de envoltorio y String. Para poder ordenar listas y arrays de otro tipo de objetos, sus clases deberán implementar esta interfaz.

Métodos de ordenación
-	Para los arrays usamos el método sort.

### La interfaz Comparator

Utilizada para poder definir el orden natural para aquellos tipos de objetos cuyas clases no implementan Comparable. Esta interfaz es implementa por clases de envoltorio y String. Para poder ordenar listas y arrays de otro tipo de objetos, sus clases deberán implementar esta interfaz Métodos de ordenación

-	Para arrays usamos Arrays.sort
-	Para List usamos sort.

### Búsqueda binaria

Los Arrays proporcionan el siguiente método para realizar una búsqueda en un array.

-	binarySearch(int array, int valor):Devuelve la posición del valor dentro del array, que previamente debe de estar ordenado. Debemos de tener en cuenta lo siguiente, si el array no está ordenado, el resultado es impredecible. Si el array esta ordenado y el elemento no se encuentra, se devuelve –plns-l. Donde plns es la posición que le correspondería al elemento.
-	Comparate(array1, array2): Devuelve el resultado de la comparación lexicográfica de ambos arrays. 
  *	El resultado de la comparación seria -1 si array1 es menor que array2
  * El resultado de la comparación es 0 si ambos arrays son iguales
  *	El resultado de la comparación es 1 si array1 es mayor que array2.
-	Mismatch(array1, array2):Devuelve la posición de la primera diferencia entre los dos arrays, o -1 si no hay diferencias.

# Modularidad

La modularidad en Java se refiere a la capacidad de dividir una aplicación Java en módulos o unidades lógicas independientes y bien definidas, lo que permite una mejor organización del código y una mayor facilidad de mantenimiento y escalabilidad del sistema. La modularidad en Java se introdujo en la versión 9 de la plataforma Java como una característica importante, y se basa en el concepto de "Java Platform Module System" (JPMS).

La modularidad en Java se logra mediante la creación de módulos que contienen un conjunto de paquetes relacionados, y que pueden ser exportados o importados por otros módulos. Cada módulo tiene su propio espacio de nombres y se puede definir como un conjunto de requisitos y capacidades, lo que significa que los módulos pueden especificar qué otros módulos necesitan para funcionar correctamente y qué servicios ofrecen a otros módulos.

En resumen, la modularidad en Java es una forma de dividir una aplicación en componentes lógicos separados, lo que permite una mejor organización del código y una mayor facilidad de mantenimiento y escalabilidad.

Las ventajas de usar la modularidad son las siguientes:
-	Mejorar el control de acceso. Permite que ciertos paquetes sean utilizados solo por otros paquetes.
-	Claridad en las dependencias. A través de module-info, se especifica claramente las dependencias entre módulos, que son evaluadas al compilar y al lanzar la aplicación.
-	Paquetes de distribución mas pequeños. Facilita la distribución de aplicaciones y mejora el rendimiento.
-	Existencia de paquetes únicos. No puede haber dos módulos que expongan el mismo paquete.

## Module-info.class

Es un archivo de clase que se genera cuando se compila un módulo en Java 9 o posterior. Este archivo contiene la información sobre el módulo, como su nombre, versión, dependencias y paquetes que exporta. El propósito principal del archivo es permitir la modularidad en Java. La ubicación de este documento debe de ser la raíz del directorio modulo.

## Compilación de un módulo

Desde el directorio raíz, el que contiene al módulo a compilar

```
Javac -- module-path dir_modulo_dep -d dir_destino ficheros 
javac -d modulo2 modulo2/*.java (no necestia module-path pues no depende de ningún)
```

## Abreviatura de argumentos
--module-path = -p
--module = -m
Ejemplo: javac -p . -m modulo1/com.cliente.Test
Empaqueta en archivos
Para empaquetar un modulo en un .jar debemos hacer uso del comando

```Jar –c –file=dir_destrino|nombre_archivo.jar –C path_modulo.```

Dir destino es el directorio de destino del modulo y path_modulo el directorio raíz del modulo. El punto “.” Indica que se incluya todo el contenido del directorio

```
Modulo2: jar –c –file=ejecutables/modulo2.jar –C modulo2
Modulo1: jar –c –file=ejecutables/modulo1.jar –C modulo1
Para ejecutar com.module1 desde ejecutables
Java –p  . –m com.module1/com.cliente.Test
```

Otro sistema de empaquetado pero no es muy común es el archivo .jmod, es muy similar a .jar, si bien debe ser utilizado para librerías nativas en lugar de modulos en generar. Debemos de tener en cuenta que no se puede utilizar el formato en la ejecución de modulos.

```
Jmod create –class-path dir_modulo fichero.jmod
Modulo2: jmod create –class-paht modulo2 ejecutables/modulo2.jmod
Modulo1: jmod create –class-paht modulo1 ejecutables/modulo1.jmod
```

## Comando jdeps

Se emplea para obtener información sobre la dependencia de modulos
-	Jdeps –s dir_modulo O jdeps –s dir_modulo/archivo.jar
Si depende de algún modulo extra
-	Jedps –module-path dir_mod_dependiente –s dir_modulo

## Módulos anónimos

Conjunto de paquetes de clases de una aplicación que no forma parte de un modulo. Habitualmente, se distribuyen en un .jar
Desde estas clases, se puede acceder a cualquier paquete de clases que se encuentre en el classpath, incluyendo tanto otros módulos anónimos como estándares.
Solo pueden acceder a las clases de un modulo anónimos las clases de otros módulos anónimos.

Cuando un modulo anónimo se incluye en el module-path de una aplicación modular, se convierte en un modulo automático. Desde estos, se puede acceder a cualquier paquete de clases, tanto de módulos anónimos/automáticos como de estándares.
Exportan implícitamente todas sus clases, que podrán ser utilizadas por otros módulos que lo requieran

## Otras características

Se puede  indicar que un determinado paquete de un modulo sea accesible únicamente por cierto modulo. Se emplea la palabra reservado to.
- Dependencias Transitivas:
Los módulos pueden tener dependencias transitivas, esto quiere decir, evitar redundancias a la hora de requerir dos módulos en los que, a su vez, uno requiere a otro. Usaríamos la palabra reservada transitive.
- Servicios:
Funcionalidad que expone una funcionalidad y la usan otros aplicaciones. Los servicios se describen a través de una interfaz de java. Por lo que tendremos que tener en cuenta 3 conceptos:
- Servicio: interfaz que define el modulo
-	Proveedor: Modulo que implementa la interfaz (provides com.interfaz1 with com.Clase1)
-	Consumidor: Modulo que utiliza el servicio (uses com.Interfaz1)

-	Acceso por reflexión:
Es posible especificar que los paquetes especificados del modulo son accesibles vía reflexión a otros módulos (opens com.paquete). Incluso, que lo sean solo a ciertos módulos (opens com.paquete to moda, modB).


# Clase Optional

La clase Optional en Java es una clase introducida en Java 8 que se utiliza para representar un valor que puede o no estar presente. Es decir, es una forma de indicar que un valor puede ser nulo o no existir, es decir, encapsula el resultado de una operación final.

La clase Optional se utiliza para evitar excepciones de tipo NullPointerException que pueden ocurrir al trabajar con referencias nulas. Al usar Optional, en lugar de devolver un valor nulo, se devuelve una instancia de Optional que puede contener un valor nulo o no nulo.
La clase Optional tiene métodos para verificar si el valor está presente o no, para obtener el valor si está presente, o para obtener un valor predeterminado si el valor no está presente.

-	Get: Devulebe el valor encapsulado. So no hay ningún valor, lanza una excepción de tipo NoSuchElementException.
-	orElse. Devuelve el valor encapsulado. Si no hay ninguno, entonces devuelve el valor pasado como parámetro.
-	isPresent: Permite comprobar si contiene o no algún valor.

Existen las variantes OptionalInt y OptionalDouble que encapsulan los tipos primitivos.

# Expresiones lambda

## ¿Qué es una interfaz funcional?

Una interfaz funcional es una interfaz de Java que contiene solo un método abstracto, también conocido como "método de función única". Esta característica es clave para el uso de funciones lambda en Java. Las interfaces funcionales se utilizan en el contexto de la programación funcional para permitir que una función sea tratada como un objeto y, por lo tanto, sea pasada como argumento a otra función. En otras palabras, se utilizan como un medio para permitir la programación funcional en Java. La anotación @FunctionalInterface se utiliza para indicar que una interfaz es una interfaz funcional. Esta anotación no es obligatoria, pero es recomendable para evitar errores.

## ¿Qué es?

En Java, las funciones lambda son una característica introducida en Java 8 que permite crear funciones anónimas de una manera más concisa y fácil de leer. Una función lambda se define como una expresión que representa una función sin nombre que se puede pasar como argumento a otro método o función. Las funciones lambda son funciones de un solo método que no requieren una declaración formal, un modificador de acceso o un nombre.
Las funciones lambda son útiles para simplificar el código al evitar la necesidad de crear clases anónimas para implementar interfaces funcionales. Además, permiten una programación funcional más natural y menos verbosa en Java.
Las funciones lambda se definen utilizando una sintaxis reducida que hace uso de la flecha 
"->". La parte izquierda de la flecha representa los parámetros de la función y la parte derecha representa el cuerpo de la función.

Por ejemplo, la siguiente expresión lambda toma dos argumentos y devuelve la suma de ellos: 
```java (int a, int b) -> a + b.```


Los parámetros pueden indicar o no el tipo. 
La lista de parámetros se puede indicar o no entre paréntesis (obligatorio si hay dos o más) y también si se indica el tipo. En caso de devolver un resultado la implementación puede omitir la palabra return si consta de una sola instrucción.

## Inferencia de tipos

La utilidad de la indiferencia se usa principalmente para determinados tipos de anotaciones en la definición de los parámetros del método, por ejemplo @NotNull var c.

Es posible inferir el tipo en los parámetros de las expresiones lambda, aunque no se puede combinar inferencia de tipos y tipos específicos en una misma expresión.

## Interfaces funcionales asociadas a expresiones lambda 

Conjunto de interfaces funcionales incorporadas en Java SE 8 dentro del paquete java.util.function. Utilizadas como argumentos en métodos que manipulas datos para el establecimiento de criterios de filtrado, operación sobre elementos, transformación etc.
Existen variantes para los datos primitivos sobre todo para int, long y double. Estas variaciones son:
-	IntPredicate
-	IntFunction
-	IntConsumer
-	IntSupplier
-	IntUnaryOperator.

### Interfaz Predicate

La interfaz Predicate es una interfaz funcional en Java que se utiliza para representar una función que toma un objeto y devuelve un valor booleano. Esta interfaz se utiliza comúnmente para la evaluación de condiciones y filtrado de datos en colecciones.
La interfaz Predicate tiene un único método abstracto llamado test().

La interfaz Predicate también tiene varios métodos predeterminados (default methods) que se pueden utilizar para combinar o negar predicados. Estos métodos incluyen:

-	and(Predicate<? super T> other): devuelve un predicado que representa la combinación lógica AND de este predicado y otro predicado dado.
-	or(Predicate<? super T> other): devuelve un predicado que representa la combinación lógica OR de este predicado y otro predicado dado.
-	negate(): devuelve un predicado que representa la negación lógica de este predicado.
Tiene una variante que es BiPredicate con dos parametros.

### Interfaz Function

La interfaz Function es una interfaz funcional en Java que se utiliza para representar una función que toma un objeto de entrada de un tipo y produce un objeto de salida de otro tipo. En otras palabras, se utiliza para transformar un objeto de un tipo a otro.
La interfaz Function tiene un único método abstracto llamado apply() que toma un objeto de entrada y devuelve un objeto de salida.
Tiene varios métodos predeterminados que se pueden utilizar para combinar funciones. Estos métodos incluyen:
-	andThen(Function<? super T, ? extends V> after): devuelve una función que representa la composición de esta función y otra función dada.
-	compose(Function<? super V, ? extends T> before): devuelve una función que representa la composición de esta función y otra función dada, en orden inverso.
-	identity(): devuelve una función identidad que simplemente devuelve su argumento sin transformación.

Tiene una variante que es BiFunction con dos parametros.

### Interfaz Consumer

La interfaz Consumer es una interfaz funcional en Java que se utiliza para representar una operación que toma un objeto de entrada de un tipo y no devuelve nada. En otras palabras, se utiliza para realizar alguna operación o efecto secundario en un objeto sin producir ningún resultado. La interfaz Consumer tiene un único método abstracto llamado accept() que toma un objeto de entrada y no devuelve nada.

Tiene varios métodos predeterminados que se pueden utilizar para combinar o encadenar consumidores. Estos métodos incluyen:
-	andThen(Consumer<? super T> after): devuelve un consumidor que representa la composición de este consumidor y otro consumidor dado.

Tiene variante BiConsumer.

### Interfaz Supplier

La interfaz Supplier es una interfaz funcional en Java que se utiliza para representar una función que no toma ningún argumento y devuelve un objeto de un tipo determinado. En otras palabras, se utiliza para generar o proveer un valor sin tomar ningún parámetro de entrada. La interfaz Supplier tiene un único método abstracto llamado get() que no toma argumentos y devuelve un objeto de un tipo determinado.

### Interfaz UnaryOperator

La interfaz UnaryOperator es una interfaz funcional en Java que extiende la interfaz Function. Se utiliza para representar una función que toma un objeto de un tipo determinado y devuelve un objeto del mismo tipo. En otras palabras, se utiliza para realizar una operación en un objeto y devolver el mismo objeto actualizado. Tiene versión para datos primitivos.
La interfaz UnaryOperator tiene un único método abstracto llamado apply() que toma un objeto de un tipo determinado y devuelve el mismo objeto actualizado
Tiene varios métodos predeterminados que se pueden utilizar para combinar o encadenar operadores. Estos métodos incluyen:
-	compose(Function<? super T, ? extends T> before): devuelve una función que representa la composición de este operador y otra función dada.
-	andThen(Function<? super T, ? extends T> after): devuelve una función que representa la composición de este operador y otra función dada.

Posee una variante BinaryOperator equivalente a BIFunction.

# Referencia a métodos

Es una funcionalidad que puede sustituir a una expresión lambda cuya única instrucción consiste en la llamada a un método. El compilador infiera las variables dadas por parámetro en el argumento del método
<table>
  <tr>
    <th>Tipo de referencia</th>
    <th>Referencia método</th>
    <th>Expresion lambda</th>
  </tr>
  <tr>
    <th>Método estático</th>
    <td>String::valueOf</td>
    <td>s->String.valueOf(s)</td>
  </tr>
  <tr>
    <th>Método de un objeto especifico</th>
    <td>Var r = new Random()
    r::nextInt</td>
    <td>Var r = new Random()
    n -> r::nextInt(n)</td>
  </tr>
  <tr>
    <th>Método arbitrario</th>
    <td>Stirng::equals</td>
    <td>(s1,s2) -> s1.equals(s2)</td>
  </tr>
  <tr>
    <th>Método constructor</th>
    <td>Person::new</td>
    <td>a -> person(A)</td>
  </tr>
</table>

# Stream

Un stream es una secuencia de datos que se procesa de manera secuencial. Los streams proporcionan una forma de trabajar con colecciones de datos de manera más flexible, legible y concisa, utilizamos la interfaz Stream de java.util.stream.
En términos generales, un stream se compone de tres elementos principales:
- Origen de datos: Es la fuente de datos, como un arreglo, una lista o una fuente de entrada / salida.
-	Operaciones intermedias: Son las operaciones que se realizan en los datos mientras se procesan en el stream, como filtrar, mapear o ordenar.
-	Operaciones terminales: Son las operaciones finales que se realizan en los datos del stream, como contar, reducir o recolectar los elementos en una colección.

Los streams en Java permiten el procesamiento de grandes cantidades de datos de manera eficiente y efectiva, utilizando el paradigma de programación funcional. También permiten el procesamiento de datos de forma paralela y asíncrona, mejorando aún más el rendimiento y la eficiencia en la manipulación de grandes volúmenes de datos.

Los stream tiene versiones para los datos primitivos, estas versiones son IntStream, LongStream y DoubleStream.

Su funcionamiento es simple, recorre los datos desde el principio hasta el final y durante el recorrido realiza algún tipo de cálculo u operación. Una vez realizado el recorrido, el stream se cierra y no puede volver a utilizarse.

Los stream se pueden crear a partir de una colección, un array (Arrays.stream(array)), una seride discreta de datos (Stream.of(2.4,7.4,9.1)) o a partir de un rango de datos(IntStream.range(1,10)).

## Principales métodos de Stream

Métodos intermedios: El resultado de su ejecución es un nuevo Stream. Esto sucede cuando se filtra y transforma datos, ordenación…
Métodos finales: Generan un resultado. Puede ser void o devolver un valor resultado de alguna operación. Esto sucede con cálculo de operaciones, búsquedas reducción…
- Conteo y procesado (métodos finales)
  *	Long count. Devuelve el número de elementos de un Stream
  *	Void forEach. Realiza una acción para cada elemento del stream.
-	Extracción de datos (métodos intermedios)
  *	Stream Distinct. Devuelve un Stream eliminado los elementos duplicados, según aplicación de equals().
  * Stream limit. Devuelve un nuevo Stream con lo n primeros elementos del mismo.
  * Stream skip. Devuelve un nuevo Stream, saltándose los n primeros elementos.
-	Comprobaciones (métodos finales)
Funcionan en modo cortocircuito, es decir, si encuentra un elemento que cumple la condición no comprueba más.
  *	Boolean anyMatch: Devuelve true si algún elemento del Stream cumple con la condición del predicado.
  *	Boolean allMatch: Devuelve true si todos cumplen con la condición del predicado.
  *	Boolean noneMatch: Devuelve true si ninguno cumple con la condifcion del predicado.
- Filtrado (Método Intermedio)
  *	Stream filter: Aplica un filtro sobre el Stream, devolviendo un nuevo Stream con los elementos que cumplen el predicado.
- Búsquedas (Métodos finales)
  *	Optional findFirst(): Devuelve el primer elemento del Stream, o un Optional vacio si no hay nada
  *	Optional findAny(): Devuelbe cualquiera de los elementos del Stream.Normalmente, el primero
-	Obtención de extremos (Métodos finales)
  *	Optional max: Devuelve el mayor de lo elementos, según el criterio de compracion del objeto Comparator.
  *	Optional mix: Operación contraria a max.
-	Transformacion (Métodos intermedios)
  *	Stream map: Transforma cada elemento del Stream en otro según el criterio definido por el objeto Function que se le pasa como parámetro.
  *	IntStream mapToInt: Aplica una función a cada elemento del Stream que genera un int de cada elemento. El resultado se devuelve como IntStream.
  *	flatMap: Devuelve un nuevo Stream, resultante de unir los Streams generados por la aplicación de una función sobre cada elemento.
- Procesamiento intermedio (Método intermedio)
  *	Stream Peek: Aplica el consumer a cada elemento del Stream, devolviendo un nuevo stream idéntico para continuar con la manipulación de los elementos. Las operaciones se aplican en modo Lazy(se queda en memoria) y solo serán operativas tras una operación final.
-	Ordenacion (Métodos intermedios)
  *	Stream sorted: Devuelbe un Stream con los elementos ordenados, según el orden natural de los mismos
  *	Stream sorted(Comparator): Devuelve un Stream con los elementos ordenados según el criterio de comparación especificado.
-	Reducción (Método final)
  *	Optional reduce: Realiza la reducción de los elementos del stream a un único valor, utilizando la función proporcionada como parámetro.

## Collect

-	Reducción
  *	 R collect: Devuelve un List, Map, o Set con los datos del Stream, en función de la implementación de Collector proporcionada.
-	Agrupación 
  *	Collector groupingBy: Devuelve un Collector que implementa una agrupación de tipo  groupBy. El método recibe como parámetro un objeto Function con el crtiterio de agrupación. Con este tipo de Collector la llamada a collect devolverá un Map de listad. Cada elemento map a tiene una clave, que es el dato por el que se hace la agrupación y un valor con la lista de objetos de cada grupo. 
-	Partición
  *	Collector partitioningBy: Devuelve un Collector para generar una agrupación Map de clave boolean y valor lista de objetos. El método recibe como parámetro un predícate para aplicar la condición a cada elemento, de modo que los que la cumplan serán agregados en una lista con clave true, y los que no en otra lista con clave false.
-	Otros usos
  *	Podemos convertir un Stream en un colección inmutable gracias al método toUnmodifiableList o toUnmodifiableSet
  *	Collector averagingDouble: Permite calcular la media a partir de los valores devueltos por la función. Existe también averagingInt y averagingLong.
  *	Collector summingInt: Permite calcular la suma a partir de los valores devueltos por la función. Existe summingLong y summingDouble.
  *	Collector joining: Devuelve un Collector que concatena en un único String todos los String resultantes de la llamada a toString sobre cada objeto del Stream.

## Stream en paralelo

Un stream paralelo en Java es una secuencia de datos que se procesa en paralelo mediante múltiples hilos de ejecución, en lugar de un solo hilo como en un stream secuencial. Esto permite un procesamiento más rápido de grandes volúmenes de datos en situaciones en las que el rendimiento es crítico. Los Stream paralelos siguen siendo objetos Stream, que utilizan los mismos métodos estudiados, pero operando de forma más eficiente. Debemos preocuparnos en operaciones que requieran realizarse en un determinado orden. Los stream paralelos se crean al usar el método parallelStream en lugar de stream en el caso de collection y para el propio stream será el método parallel.

Para las operaciones finales de ordenación los stream paralelos devuelen los datos ordenados según los datos almacenados que posea cada hilo, provocando que los datos no salgan en el orden esperado. Para evitar esto podemos realizar las operaciones intermedias de manera asíncrona y usar el método sequential para transformar el stream paralelo en un stream secuencial.

### Referencias a métodos

Las referencias a métodos sustituyen a expresiones lambda cuya única instrucción consiste en una llamada a un método. Indica que método debe ser llamado en circunstancias donde los parámetros y objeto al que aplicarlo pueden ser deducidos por el contexto.
Sintaxis: Clase/objeto::nombre_metodo
Existen 4 tipos

Tipo	Expresión lambda equivalente	Referencia a método
Referencia a método estatico	s->String.valueOf(s)	String::valueOf
Referencia a método de objeto especifico	s-> System.out.println(s)	System.out::println
Referencia a método de objeto arbitrario	(a,b)->a.equals(b)	String::equals
Referencia a constructor	a->new MiClase(a)	MiClase::new

### Stream de tipos primitivos

Las interfaces IntStream, DoubleStream y LongStream, cuyos objetos son obtenidos los métodos mapToInt, mapToDouble y mapToLong, respectivamente, proprcionan los siguientes métodos de cálculo:
-	Sum: Método final que devueleve la suma de todos los elementos del stream.
-	Average:Metodo final que devuelve la media encapsulada en un OptionalDouble en los tres casos.
-	Max y min: Devuelve el mayor y menos de los números respectivamente. En DoubleStream  y LongStream el tipo de devolución es OptionalDouble y OptionalLong, respectivamente.

# Entrada/Salida
La entrada y salida se refiere a operaciones de recuperación de datos desde una fuente externa (entrada) y envió de datos desde el programa al exterior (salida).
Salida

## java.io

-	OutputStream: Clase abstracta que representa un flujo de salida
-	PrintStream: Subclase que proporciona métodos para enviar datos a cualquier flujo de salida
-	FileOutStream: Subclase de OutputStream que representa un flujo de salida asociado a un fichero.
-	FileWriter: Clase específica para escritura de texto en un fichero.

### Escritura por consola

System.out es un objeto de la clase PrintStream que nos permite realizar las siguientes operaciones
-	Print: Escritura de cualquier tipo de dato Java, sin incluir salto de línea al final
-	Println: Escritura de cualquier tipo de dato Java, con salto de línea al final.
-	Printf(String forrmat, object…args): Escritura de datos con formato

### Escritura a ficheros

Para la escritura de información en un fichero usaremos la propia clase PrintStream a la cual le pasaremos en el constructor la ruta del documento o un FileOutputStream.
-	Constructor ruta del documento: 
  *	Se graba la información en modo sobrescritura
  *	Si no existe el fichero se crea
  *	Escritura con formato.
-	 Constructor FileOutputStream (con ruta y boolean): 
  *	Si el boolean es true se indica que se escribirá el documento agregando el contenido.
 
#### Métodos principales de  FileWriter

-	Constructor ruta del documento
  *	Graba los datos en modo sobrescritura
  *	Crea el fichero si no existe
-	Constructor ruta del documento mas boolean
  *	Graba los datos en mod append si es true el boolean
  *	Crea el fichero si no existe

### Metodos principales BufferedWriter

Permite la escritura a través de un buffer mejorando el rendimiento
-	Constructor con FileWriter.

#### Entrada

Principales clases para operaciones de entrada de datos
-	InputStream: Clase abstracta que representa un flujo de entrada de bytes.
-	FileInputStream: Subclase de InputStream que representa un flujo de entrada asociado a un fichero.
-	FileReader: Clase específica para lectura de texto en un fichero
-	BufferedReader: Proporciona un mecanismo eficiente para la lectura de cadenas de texto de una fuente externa.

#### Lectura por teclado

-	Usando BufferedReader: Se debe crear un InputStreamReader asociado a la entrada estándar(System.in)
-	Lectura mediante Scanner

#### Lectura de fichero

-	Usando BufferedReader:
  *	Lectura de todas las línea del fichero
  *	Si el fichero no existe se produce una excepción
  *	Se Inicializa con una clase FileReader
-	FileInputStream
  *	Utilizado para lectura de ficheros binarios
  *	Se inicializa con un File.

## java.nio

Nuevo paquete de entradsa/salida para lectura y escritura en ficheros

-	Path: Representa una ruta a un fichero o directorio
-	Paths: Clase utilizad apara crear instancias de Path
-	Files: Dispone de diversos métodos estáticos para operar contra un fichero o directorio

### Inertfaz Path

Es parte de la API de manejo de archivos introducida en la versión 7 de Java. Esta interfaz se encuentra en el paquete java.nio.file y se utiliza para representar una ruta o dirección a un archivo o directorio en el sistema de archivos.

La interfaz Path proporciona una forma de trabajar con rutas de archivos independientemente del sistema operativo subyacente. Es decir, se puede trabajar con rutas de archivos en Windows, Linux, macOS u otros sistemas operativos, utilizando los mismos métodos y propiedades de la interfaz Path.

Algunos de los métodos que se pueden utilizar con Path incluyen la creación de una nueva instancia de Path, la obtención de información sobre la ruta, la concatenación de rutas, la verificación de si una ruta existe o no, y la obtención de los componentes de una ruta, como el nombre del archivo o directorio.

Para crear una implementación de path usaremos el método of o el método get de la clase Paths.

Principales métodos
-	getFileName: Nombre del fichero o ultimo elemento del Path
-	toAbsolutePath: Ruta completa del fichero o directorio.
-	Normalize: Resuelve las rultas relativas y devuelve el path normalizado
-	Relativize: Devuelve la ruta relativa de other respecto al path principal.
-	Resolve: Resuelve la ruta de other frente a la principal
-	getNameCount: Devuelve el numero de elementos del path, sin incluir el raíz
-	genaName(index): Devuelve la parte del path que ocupa la posición indicada. El primer elemento (sin incluir la raiz)tiene índice 0.

#### Clase Files

Es parte de la API de manejo de archivos introducida en la versión 7 de Java. Esta clase se encuentra en el paquete java.nio.file y se utiliza para realizar operaciones de bajo nivel en archivos y directorios, como copiar, mover, borrar, crear y modificar archivos.

La clase Files proporciona una amplia gama de métodos útiles para trabajar con archivos y directorios, incluyendo la creación de nuevos archivos y directorios, la lectura y escritura de archivos, la verificación de la existencia de un archivo o directorio, la obtención de información de metadatos del archivo, como la fecha de creación y la última fecha de modificación, y la realización de operaciones de archivos en paralelo.
Además, la clase Files también proporciona métodos para trabajar con enlaces simbólicos y para realizar operaciones atómicas en archivos, lo que significa que las operaciones se realizan como una sola unidad y no se pueden interrumpir por otras operaciones en el sistema.

Principales métodos
-	lines: Devuelve un Stream con todas las líneas del fichero. A partir de ahí, se pueden aplicar los métodos stream para realizar búsquedas, transformaciones, filtrados, etc.
-	readAllLines: Devuelve una lista con las cadenas del fichero, donde cada elemento corresponde con una línea
-	newBufferedReader: Devuelve un objeto BufferedReader para realizar la lectura de forma clásica.
-	writeString: Escribe en el fichero indicado como primer parámetro, la cadena especificada en el segundo, utilizando el juego de caracteres del tercero y las opciones de escritura del cuarto.
-	Write: Escribe en el fichero indicado como primer parámetro la conleccion de cadenas especificas en el segundo, utilizando el juego de caraceteres del tercero y las opciones de escritura del cuarto.
-	Copy: Copia el contenido del un fichero en otro.
  *	Si el fichero target ya existe y no se indica opción, se produce una excepción. Aunque si ambas rutas son iguales, el método se ejecutara sin cambios
  *	Si Source es un directorio, se creara en taget un directorio vacio
  *	Si target es un directorio, FileAlreadyExistsException
  *	Si el tercer parámetro es StanderdCopyOption.REPLACE_EXISTING, en fichero target será sustituido en caso de que exista
  *	Si el tercer parámetro incluye StandarCopyOption.COPY_ATTIBUTES, se copiaran tamibien las propiedades del fichero origen en el destino.
-	Move: Mueve un fichero de origen a otro de destino
  *	Si el fichero target ya existe y no se indica opción, se produce una excepción. Aunque si ambas rutas son iguales, el método se ejecuta sin cambios
  *	Si Source es un directorio, se creara en target un directorio vacio
  *	Si target es un directorio, FileAreadyExistsException
  *	Si el tercer parámetro es StandardCopyOption.REPLACE_EXISTING, en fichero target será sustituido en caso de que exista.
-	Delete: Elimina el fichero si existe, si no se produce una excepción, Si es un directorio, deberá estar vacio
-	Delete ifExists: Elimina el fichero si existe, sino no hace nada. Si es un directorio, deberá estar vacio.
-	createFile: Si el fichero existe, se produce una excepción.
