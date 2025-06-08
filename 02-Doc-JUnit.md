<div align="center">
  <img src="https://raw.githubusercontent.com/jorgenavarroenamoradotokio/docs/main/logo/JUnit-Logo.svg">
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

La parametrización de un test es una funcionalidad que nos permite realizar múltiples pruebas sobre un método gracias a que se le pasa una lista de valores. Los parámetros de entrada pueden ser tan sencillos como una lista de valores usando @ValueSource, o más complejos, pasándole un documento csv @CSVSource - @CSVFile, un método @MethodSource o un Enum @EnumSource.

Para que sean mas descriptivos las pruebas se ParameterizedTest tiene los siguientes placeholders
- {DisplayName} y {DisplayNameGeneration} para personalizar los nombres de las pruebas
    ```java
    @ParameterizedTest(name= "Check blank {displayName}")
    ``` 
- {index}: El índice de la ejecución del test (comienza en 1).
    ```java
    @ParameterizedTest(name= "Check blank {index}")
    ``` 
- {arguments}: Una representación basada en toString() de todos los argumentos.
    ```java
    @ParameterizedTest(name= "Check blank {arguments}")
    ``` 
- {0}, {1}, ..., {n}: Representaciones basadas en toString() de los argumentos individuales.
    ```java
    @ParameterizedTest(name= "Check blank {0}")
    ``` 

Parametros de entrada
- Parametrizacion mediante @ValueSource
    ```java
    @ParameterizedTest
    @ValueSource(strings = {"abc","asd",""})
    void checkBlanks(String value){
        assertTrue(StringsUtils.isBlank(value));
    }
    ``` 
- Parametrizacion mediante @EnumSource
    ```java
    enum EnumValues{
        ABC, ASD, WXY
    }

    @ParameterizedTest
    @EnumSource(value = EnumValues.class, names = {"ABC"}, mode = EnumSource.Mode.EXCLUDE)
    public void excludeEnumValue(Object value){
        System.out.println(value.toString());
    }

    @ParameterizedTest
    @EnumSource(value = EnumValues.class, names = {"A.."}, mode = EnumSource.Mode.MATCH_ALL)
    public void matchAllEnumValue(Object value){
        System.out.println(value.toString());
    }
    ```

- Parametrizacion mediante @MethodSource
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
- Parametrizacion mediante @CsvSource
    ```java
    @ParameterizedTest
    @CsvSource({
        "Audi,55", 
        "Tesla,99",
        "Ferrari,101"
    })
    public void csvSourceMethod(String car, int quantity){
        System.out.println(car + ": "+quantity);
    }
    ```
- Parametrizacion mediante @CsvFileSource
    ```java
    @ParameterizedTest
    @CsvFileSource(files = "src/test/java/resources/input.csv")
    public void csvFileSource(String car, int quantity){
        System.out.println(car + ": "+quantity);
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

## Caracteristicas basicas

- Los métodos que solo se les puede hacer mock son métodos de carácter publico o default
- Para inicializar un mock tenemos dos maneras una mediante implementación estatica o implementación nomal
  - Estatica = mock(nb-clase.class)
  - Normal = Mockito.mock(nb-clase.class)

## Implementacion de simulaciones

Mockito nos permite simular comportamientos de objetos para facilitar las pruebas unitarias.

Mock cuenta tambien con anotaciones como @Mock, @InjectMocks, @ExtendsWith… Son anotaciones que nos ayudan a ahorrar tiempo a la hora de escribir nuestro código de prueba. Estas anotaciones por defecto están deshabilitadas, para poder activarlas se puede hacer de dos maneras mediante MockitoAnnotations.openMocks(this) la otra es con la anotación @ExtendWith
- @ExtennWith: Es una extensión de tipo clase que nos permite activar las anotaciones de @Mock e @InjectMocks para ellos pondreos @ExtendsWith (MockitoExtension.class)
- @Captor: Es una anotación que nos permite definir AgumentCaptor 
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
### Argument Matchers

Los Argument Matchers son una característica de Mockito que permite hacer coincidir los argumentos de métodos simulados de manera flexible durante las pruebas unitarias. En lugar de especificar valores exactos, los Argument Matchers permiten definir condiciones que los argumentos deben cumplir, facilitando así la creación de pruebas más generalizadas y menos propensas a cambios específicos de datos.

```java
@Test
void argumentMatcherTest(){
    when(validNumber.check(anyInt())).theReturn(true);
    assertTrue(validNumber.check(4));
}
```

### Simulaciones Basicas

La funcionalidad más básica en Mockito es la capacidad de crear objetos simulados, conocidos como mocks, y definir comportamientos básicos para métodos específicos. Para lograr esto, utilizamos la estructura when-thenReturn.

- when: Indica que estamos configurando una expectativa para una llamada de método en el mock.
- nb-clase.nb-metodo(): Es la llamada al método específico en el objeto mock cuya respuesta queremos simular.
- thenReturn(resultadoSimulado): Define el resultado que se devolverá cuando el método especificado sea llamado.

Por ejemplo, si tenemos un mock de una clase Calculadora y queremos simular que el método sumar devuelva 5 cuando se le pasan los parámetros 2 y 3, escribiríamos:
```java
@Test
void addCalculadoraTest(){
    when(calculadora.sumar(2, 3)).thenReturn(5);
    assertEquals(5, calculadora.sumar(2, 3));
}
```

### Simulacion de excepciones

Para simular llamadas que lanzan excepciones en nuestros tests, utilizamos el método thenThrow de Mockito. Esto nos permite especificar que, cuando se ejecute un método particular en nuestro código, se lanzará una excepción predefinida. Posteriormente, podemos usar assertThrows para verificar que la excepción realmente se lanza, asegurando así la correcta funcionalidad de nuestro test unitario.

- when: Configura una expectativa para una llamada de método en el mock.
- nb-clase.nb-metodo(): Es la llamada al método específico en el objeto mock que queremos que lance una excepción.
- thenThrow(nb-clase-excepcion.class): Define la excepción que se lanzará cuando se llame al método especificado.

```java
@Test
void addMockExceptionTest(){
    when(validNumber.checkZero(0)).thenThrow(new AritmeticException("msg"));
}
```

### Verificar llamada de un metodo

El método verify en Mockito se utiliza para validar y comprobar si los métodos de un objeto simulado (mock) han sido llamados de la manera esperada durante la ejecución de un test. Este método es crucial para asegurar que la lógica de negocio de nuestro código interactúa correctamente con sus dependencias simuladas.

Los principales usos de verify

- Verificar la llamada de métodos: Asegura que un método específico en un mock ha sido llamado con ciertos parámetros. Esto es útil para confirmar que se han realizado las interacciones esperadas con el mock.
    ```java
    verify(mock).metodo(parametros);
    ```
- Verificar el número de veces que se ha llamado un método: A través del parámetro times, se puede comprobar cuántas veces se ha llamado un método. Esto es útil cuando un método debe ser invocado un número específico de veces.
    ```java
    verify(mock, times(n)).metodo(parametros);
    ```
- Verificar que un método no se ha llamado: Usando verify con never(), se puede confirmar que un método no ha sido llamado en absoluto, lo cual es útil para asegurarse de que ciertas condiciones no desencadenen interacciones no deseadas.
    ```java
    verify(mock, never()).metodo(parametros);
    ```
- Verifica que al menos se ejecute como mínimo se ejecuto 1 vez, pero se pudo ejecutar n veces
    ```java
    verify(mock, atLest(2)).metodo(parametros);
    ```
- Verifica que se ejecuto al menos una vez
    ```java
    verify(mock, atLestOnce(1)).metodo(parametros);
    ```
- Verifica que se ejecuto como máximo  n veces
    ```java
    verify(mock, atMost(4)).metodo(parametros);
    ```
- Verifica que no ha tenido inteactuado con nuestro mock
    ```java
    verify(mock, verifyNoInteraction()).metodo(parametros);
    ```

### ArgumentCaptor

Se utiliza para capturar los argumentos que se pasan a un método de un objeto simulado (mock) durante la ejecución de una prueba. Esto es especialmente útil cuando necesitas inspeccionar, verificar o hacer aserciones sobre los valores de los parámetros que se pasan a un método.

```java
@Test
void testProcesarGuardaDatoProcesado() {
    Repositorio repositorioMock = mock(Repositorio.class);
    Servicio servicio = new Servicio(repositorioMock);

    servicio.procesar("dato");

    ArgumentCaptor<String> captor = ArgumentCaptor.forClass(String.class);
    verify(repositorioMock).guardar(captor.capture());

    String valorCapturado = captor.getValue();
    assertEquals("dato_procesado", valorCapturado);
}
```

### Asnwer

Se utilizan para definir comportamientos personalizados cuando se invocan métodos en un objeto simulado (mock). Esto es útil cuando los comportamientos predefinidos de Mockito (como thenReturn y thenThrow) no son suficientes y necesitas una lógica más compleja que dependa de los parámetros de entrada u otros estados.

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

## Spy

Los Spy son un hibrido entre un objeto real y un objeto mockeado, la única diferencia entre un mock y el spy es que siempre se llama al método real. Solo se puede crear un spy en clases finales, no valen ni clases abstractas ni interfaces. Cuando usemos spy es recomendable el uso de doReturn, ya que con el when el spy ejecuta dos veces el método una la real y luego la simulada. Spy también posee anotaciones usa @Spy
