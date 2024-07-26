<div align="center">
  <img src="https://raw.githubusercontent.com/jorgenavarroenamoradotokio/docs/feature/jUnit/logos/JUnit-Logo.svg">
</div>

# Intoduccion

JUnit se trata de un framework Open Source para la automatización de pruebas (tanto unitarias, como de integración) en los proyectos de Software. JUnit provee al usuario de herramientas, clases y métodos que facilitan la tarea de realizar pruebas en sus sistemas y así asegurar su consistencia y funcionalidad. 

JUnit 5 está compuesto por 3 subproyectos:

- La plataforma JUnit: sirve como base para lanzar el framework sobre la JVM. 
  - API TestEngine: Framework para el desarrollo de pruebas que permite la ejecución de test sobre la plataforma
  - JUnit Plataform Suite Engine: permite la ejecución de pruebas personalizadas utilizando uno o más motores de pruebas sobre la plataforma.
  - Unit Plataform: IDEs
- JUnit Jupiter: Es la combinación del nuevo modelo de programación y el modelo de extensiones para escribir pruebas. Este subproyecto proporciona su  propia TestEngine para ejecutar las pruebas en la plataforma.
- JUnit Vintage: Proporciona un TestEngine para ejecutar pruebas basadas en JUnit 3 y JUnit 4

# Fundametos basicos de una clase unitaria (TestCase)

La principal funcion es realizar test unitarios.
Estos test unitarios los podemos definir como  metodos de pruebas de software mediante el cual se prueban unidades individuales de codigo fuente para determinar si realiza el funcionamiento esperado. 

La principal razon para el uso de estas clases es la verificacion en un futuro lejano que el codigo siga funcionando correctamente

Estas clases tienen la siguiente estructura basica:
- La clase de prueba que contiene uno o más metodos de prueba
- Los métodos no necesitan que sean públicos para ejecutarse.
- Anotaciones y anotaciones especiales
- Asercciones (Assertions).

## Anotaciones

- @Test: Se usa para indicar que metodo se va a usar para ejecutar una prueba unitaria
- @BeforeEach se ejecuta antes de cada método @Test.
- @AfterEach se ejecuta después de cada método @Test.
- @BeforeAll se ejecuta antes de todos los @Test y una sola vez
- @AfterAll se ejecuta después de todos los @Test y una sola vez.

## Anotaciones especiales

Utilidad que nos permite agregar funcionalidades extra que no son obligatorias de usar

- DisplayName: sirve para agregar un texto más explicativo al test
- Disabled: sirve para skiped un test unitario

## Asserts

Las Aserciones son una colección de métodos de utilidad que admite afirmaciones de condiciones en las pruebas. Para ello se usan los siguientes métodos:

- AssertEqual: Afirma que lo esperado y lo real sean iguales. Se usa para objeto primitivos ya que su función es parecida al usar ==, importante, admite un tercer parametro denominado delta que nos facilita para el tema de numeros un rango mas amplio de verificacion (importante para los decimales)
- AssertSame: Afirma que lo esperado y lo real se refieren al mismo objeto.
- AssertNotSame: Afirma que lo esperado y lo real se refieren a diferentes objeto.
- AssertTrue: Afirma que el valor esperado sea True.
- AssertFalse: Afirma que el valor esperado sea False.
- AssertNull: Afirma que el valor esperado sea null.
- AssertNotNull: Afirma que el valor esperado no sea null.
- AssertExcepcion: Permite comprobar si se ha lanzado el error de un método
- AssertTimeout: Permite verificar si la prueba unitaria a tardado en el tiempo estimado.
- AssertThrow: Permite verificar que se ha lanzado la excepción esperada. 
```java  
assertThrows(AritmeticExcepcion.class,() -> 1/0, "No se puede dividir entre 0");
```

### Grupo Assertions.

Es la agrupación de multiples assert que se ejecutan de manera individual y si falla alguna de ellas no impide que la ejecución se termine, ya se informara del error posteriormente. Para agrupar todas las aserciones usaremos el método assertAll en el que le pasaremos una descripción y posteriormente los diferentes assert. 

```java
assertAll(
    ()-> assertEquals(20, 10+10),
    ()-> assertEquals(0, 10-10)
);
```

## Nested

Nos permite separar el código de pruebas y agruparlo en bloques que se ejecutaran de manera independiente unos de otros, se puede agregar el displayName

## Repetir el numero de test

Se usa cuando queremos que un test se repita varias veces ya que algunos test pueden cambiar las propiedades o atributos globales y lo que hacemos es que se reinicien. Podemos indicar el numero de veces, para ello usaremos la anotación @RepeatedTest(numero de veces), importante este tipo de métodos no deben de llevar la anotación @Test y pueden recibir como parámetro de método RepetitionInfo.

## Tag

Sirve para clasificar los test y agruparlos para que se ejecuten todas aquellas que tengan asociadas a ellas

## Parametrizar un test

La parametrización de un test es una funcionalidad que nos permite realizar múltiples pruebas sobre un método gracias a que se le pasa una lista de valores. Los parámetros de entrada pueden ser tan sencillos como una lista de valores usando @ValueSource, o más complejos, pasándole un documento csv @CSVSource - @CSVFile o un método @MethodSource.
```java
@ParameterizedTest(name = "{index} => a={0}, b={1}, sum={2}")
@MethodSource("addProviderData")
public void addTest(int a, int b, int sum){
    assertEquals(sum, a + b);
}

private static Stream<Arguments> addProviderData(){
    return Stream.of(
        Arguments.of(6,2,8),
        Arguments.of(-6,-2,-8),
        Arguments.of(6,-2,4)
    );
}
```

## Inyeccion de dependencias mediante testInfo y testReport

- TestInfo: Es un componente de unit que nos permite mostrar mensajes por consola mas detallados como puede ser el nombre del método, el displayname, los parámetros, los tags….
- TestReport: Es un componente de unit que nos permite registrar en el log información que queramos anexar en la salida junto un timestamp, algo mas elaborado que un simple mensaje por consola

## Limitar tiempo de ejecución

Junit 5 nos permite limitar el tiempo de ejecución de un test unitario cuando es demasiado pesado y necesita de muchos recursos del sistema, para ello nos da la anotación timeout en la cual indicaremos dentro de él el tiempo, por defecto la unidad de tiempo es segundos.
- Timeout (5)
- Timeout (value = 500, TimeUnit.MILISECONDS)

```java
@Test
void timeOutTest(){
    assertTimeOut(Duration.ofMillis(500), ()->{
        // operacion a realizar
    });
}

```

# Ciclo de vida de un Test

La vida útil de un test la podemos definir por método o por clase indicando el ciclo de vida o según las propiedades del sistema donde se ejecute.

Si forzamos la vida útil de un test por entorno tendremos las siguientes casuísticas:

- Habilitar o deshabilitar un Test según el sistema operativo instalado. @EnabledOnOS(org.junit.jupiter.api.condition.os.x)@DisabledOnOs(org.junit.jupiter.api.condition.os.x)
- Habilitar o deshabilitar un test por una versión concreta de un sistema operativo @EnabledIfSystemProperty(matches = “Windows 7”, named = ”os.name”) @DisabledIfSystemProperty(matches = “Windows 7”, named = ”os.name”)
- Habilitar o deshabilitar un Test por versión del JRE @EnabledOnJre(org.junit.jupiter.api.condition.JRE.JAVA_9) @DisabledOnJre(org.junit.jupiter.api.condition.JRE.JAVA_9)
- Habilitar un test por varible de entorno @EnabledIfEnvironmentVariable @DisabledIfEnvironmentVariable 

Si forzamos un test por ciclo de vida tendremos las siguientes casuísticas:
- Definimos el ciclo de vida usando la anotación @TestInstance(Lifecycle.x)
- Por defecto un Test tiene el ciclo de vida por metodo, PER_METHOD
- Podemos definir el ciclo de vida por clase, PER_CLASS
Forzamos un frgamento del código usando assumingThat y si se cumple una condición realiza dichas valizaciones.

# TDD

TDD o Test-Driven Development (desarrollo dirigido por tests) es una práctica de programación que consiste en escribir primero las pruebas (generalmente unitarias), después escribir el código fuente para que pase la prueba de manera satisfactoria y por último refactorizar el código escrito.
Con este patrón de diseño nos permite crear un código más robusto, más seguro y más mantenible.
La implementación de este patrón en metodologías agiles seria de la siguiente manera:
- El cliente escribe su historia de usuario.
- Se escribe junto al cliente los criterios de aceptación.
- Se selecciona un criterio de aceptación para su implementación (prueba unitaria).
- Se comprueba que esta falla.
- Se escribe el código para que pase la prueba.
- Se ejecutan las pruebas automatizadas.
- Se refactoriza y limpia el código 
- Se vuelven a pasar todas las pruebas automatizadas para comprobar que todo funciona.
- Volvemos al punto 3 y repetimos todo el proceso hasta acabar con los criterios de acceptacion.

Los principales puntos negativos de este patrón de diseño son los siguientes:
- Problemas sobre interfaces gráficas
- Base de datos, ya que debemos de contar con unos datos conocidos y verificar que el contenido de la base de datos sea el esperado, para esto la solución es usar objetos simulados (MockObject).
- Saber entender el correcto funcionamiento de este patrón para que realmente sea productivo. Saber refactorizar el código correctamente para que sea más optimo y consistente.

Para un correcto funcionamiento e implementación de los test debemos de tener encuenta lo siguiente:
- Deben de ser cortos.
- No deben de modificar o crear información para otros test.
- Deben de ser independientes (orden de ejecución al azar).
- Implementar test con datos que sean fáciles de leer y entender.
- Implementar métodos staticos de carga, para evitar que los datos que se puedan actalizar en nuestros objetos se pasen a otros test unitarios

Uso de datos reales o similares cuando sea necesario.

# Framework Mockito

Es un framework de pruebas compatible con Junit 5 que nos permite crear objetos simulados (mock) en un entorno controlado y determinado. Gracias a que nos permite simular funcionalidades de componentes/capas de servicios, apis, datos que no tenemos control sobre su funcionamiento y casuísticas posibles.

La metodología de pruebas que se suele implementar con este framework es BDD (Behavior Driven Development) o desarrollo impulsado por el comportamiento, aunque también se aplica el TDD.

Necesitaremos las dependencias de mockito-core y mockito-junit-jupiter

## Funcionamiento de mockito

Es un framework de pruebas compatible con Junit 5 que nos permite crear objetos simulados (mock) en un entorno controlado y determinado. Gracias a que nos permite simular funcionalidades de componentes/capas de servicios, apis, datos que no tenemos control sobre su funcionamiento y casuísticas posibles.

La metodología de pruebas que se suele implementar con este framework es BDD (Behavior Driven Development) o desarrollo impulsado por el comportamiento, aunque también se aplica el TDD.

Necesitaremos las dependencias de mockito-core y mockito-junit-jupiter

## Funcionamiento de mockito

- Los métodos que solo se les puede hacer mock son métodos de carácter publico o default
- Para inicializar un mock tenemos dos maneras una mediante implementación estatica o implementación nomal
  - Estatica = mock(nb-clase.class)
  - Normal = Mockito.mock(nb-clase.class)
- Para simular una llamada usaremos el método when en el cual indicaremos el método que usaremos, importante podemos indicarle unos parámetros en concreto o pasarle unos argumentos genercios como anyString, anyLong, anyMap….
- Para simular la respuesta usaremos thenReturn nada mas terminar el when y dentro del paréntesis le indicaremos el retorno
  - When (nb-clase.nb-metodo ()).thenReturn(resultadoSimulado)
    ```java
    @Test
    void addTest(){
        when(validNumber.check(3)).theReturn(false);
    }
    ```
- Para simular las llamadas de excepciones usaremos throwWhen lo que nos permitira que cuando se ejecute una parte de nuestro código se lance la excepción expecificada para que posteriormente usando un assertThrow comprobemos que realmente se lanza y verificamos el test Unitario
  - When (nb-clase.nb-metodo).thenThrow(nb-clase-excepion.class)
- Verify es un método estatico que se encarga de validar y verificar si realmente se han llamado a los métodos que estamos simulando. En caso de no ser simulados las pruebas se quedan como estado fallido, importante cuando se quiera verificar un meotodo que es posible que tuviera mas de una ejecución, verify fallara, necesitamos la aplicación del segundo parámetro del método que es times…. La estructura de la llamada básica seria asi
  - Verify (nb-mock).nb-metodo-mockeado(valor-parametro-enviado)
- Mockito nos permite capturar los argumentos que recibe de parámetro mediante la clase ArgumentCaptor para posteriormente evaluarlo con los assert de Junit. Para ello inicializaremos la clase ArgumentCapto<nb-clase> captor = ArgumentCaptor.forClass(nb-clase.class), para posteriormente en el verify pasarle comoparámetro captor.capture, para obtener el valor usaremos captor.getValue(). Existe otra manera de generar ArgumentCaptor, gracias a la anotación @Captor.
- Mock cuenta tambien con anotaciones como @Mock, @InjectMocks, @ExtendsWith… Son anotaciones que nos ayudan a ahorrar tiempo a la hora de escribir nuestro código de prueba. Estas anotaciones por defecto están deshabilitadas, para poder activarlas se puede hacer de dos maneras mediante MockitoAnnotations.openMocks(this) la otra es con la anotación @ExtendWith
  - @Mock: Es una anotiacion que no ahorra el escribir la inicialización del mock manual
  - @InjectMocks: Es una anotación que nos permite crear la instancia de un objeto y que agrege a ella los mock necesarios que hemos creado anteriormente. Importante no funciona con interfaces, demos de usarla con las implementaciones de estas
    ```java
            @InjectMocks
            private Add add;
            @Mock
            private ValidNumber validNumber

            @BeforeAll
            public void setUp(){
                MockitoAnnotations.initMocks(this)
            }

            @Test
            void addTest(){
                add.add(3,2);
                Mockito.verify(validNumber).check(3);

            }
    ```
  - @ExtennWith: Es una extensión de tipo clase que nos permite activar las anotaciones de @Mock e @InjectMocks para ellos pondreos @ExtendsWith (MockitoExtension.class)
  - @Captor: Es una anotación que nos permite definir AgumentCaptor
- Mockito no solo nos permite retornar valores fijos, sino que también puede retornarnos Answer que son funciones anónimas que nos permiten modificar valores de nuestro objecto a retornar de manera dinámica, como puden ser simular la generación de un ID de manera autoincremental, en caso de no quere aplicar la anwser podemos aplicar directamente el método  doAnwser, funcionando de la siguiente manera doAnswer(lambda) doAnwser(invocation ->{}).when(nb-clase).nb-metodo(valor-parametro)
- Argument matcher se encarga de validar que los argumentos que pasamos a un mockito son los esperados, es decir que sean del mismo tipo y tengan el valor esperado, para ello usarmos
  - Estatic 
    - Mockito.argThat(arg -> propiedad lambda)
    - ArgumentMarchers.argThat(arg -> propiedad lambda)
  - Nomal argThat (arg -> propiedad lambda)
  - Implementar clase anónima en la que podamos implementar nuestro método un mensaje de error personalizado y nuestro método matches, donde implementaremos la lógica de validación que queramos realizar
- Mockito nos facilita la control de excepciones para los métodos que no retornan valores, para ello Mockito nos da el método doThrow(nb-clase.class), el único detalle que debemos de tener es que la invocación no es después de ejecutar el programa sino es antes. Para que posteriormente se pueda validar con assertThrow de Junit. doThrow(nb-clase.class).when(nb-clase) .nb-metodo(.nb-parametro)
- Mockito nos permite controlar y comprobar que se han ejecutado excepciones usando when-thenTrhow
    ```java
    @Test
    void addMockExceptionTest(){
        when(validNumber.checkZero(0)).thenThrow(new AritmeticException("msg"));
    }
    ```
- Mokito nos facilita el poder llamar de manera real el método que estamos simulando para ello usaremos doCallRealMethod().when(nb-class).nb-metodo(valor-parametro)
    ```java
    @Test
    void addRelMethod(){
        when(validNumber.check(3)).thenCallRealMethod();
        assertEquals(true,validNumber.check(3));
    }
    ```
- Mockito nos permite controlar de una manera más compleja usando una logica personalizada el valor de un metod que estamos simulando
    ```java
    @Test
    void addDoubleToIntTest(){
        Answer<Integer> answer = new Answer<Integer>(){
            @Override
            public Integer answer(InvocationOnMock invocationOnMock) throws Throwable{
                return 7
            }
        };

        when (validNumber.dobleToInt(7.7)).thenAnswer(answer);
        assertEquals(7, validNumber.dobleToInt(7.7));
    }
    ```
- Mockito nos permite verificar el orden de ejecución de los métodos que simulamos para ello usaremos el método inOrder el cual retorna un InOrder. 
- Mockito nos permite comprobar el numero de invocaciones que tiene nuestro método mockeado, para ello usaremos verify donde le pasaremos como segundo argumento un times que indicaría el numero de veces que creemos/esperamos que se ejecute verify (nb-clase, times(num-veces)).nb-metodo(valor-parametro). Tambien posee otros métodos como
  - atLest que indica que como mínimo se ejecuto 1 vez, pero se pudo ejecutar n veces
  - atLestOnce que se ejecuto al menos una vez
  - atMost que indica que como máximo se ejecuto n veces.atMostOnce indica que el máximo de ejecuciones se x.
  - never indica que nunca se ha ejecutado el método
  - verifyNoInteraction verifica que no ha tenido inteactuado con nuestro mock

## Spy

Los Spy son un hibrido entre un objeto real y un objeto mockeado, la única diferencia entre un mock y el spy es que siempre se llama al método real. Solo se puede crear un spy en clases finales, no valen ni clases abstractas ni interfaces. Cuando usemos spy es recomendable el uso de doReturn, ya que con el when el spy ejecuta dos veces el método una la real y luego la simulada. Spy también posee anotaciones usa @Spy
