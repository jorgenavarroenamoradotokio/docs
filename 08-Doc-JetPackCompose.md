## Índice
- [Introducción](#introducción)
  - [¿Por qué migrar a Compose?](#por-qué-migrar-a-compose)
  - [Comparativa rápida: XML vs Compose](#comparativa-rápida-xml-vs-compose)
  - [Requisitos Previos](#requisitos-previos)
- [Fundamentos de Jetpack Compose](#fundamentos-de-jetpack-compose)
  - [¿Qué es un `@Composable`?](#qué-es-un-composable)
  - [Composición y recomposición](#composición-y-recomposición)
  - [visualizar vistas previas (@Preview)](#visualizar-vistas-previas-preview)
  - [Ciclo de vida básico en Jetpack Compose](#ciclo-de-vida-básico-en-jetpack-compose)
  - [Gestión de estado: remember y mutableStateOf](#gestión-de-estado-remember-y-mutablestateof)
- [Componentes Principales de Jetpack Compose](#componentes-principales-de-jetpack-compose)
  - [Text](#text)
  - [Buttons](#buttons)
  - [Layout](#layout)
    - [Box](#box)
    - [Column (Vertical)](#column-vertical)
    - [Row (Horizontal)](#row-horizontal)
  - [TextField - Entrada de datos](#textfield---entrada-de-datos)
  - [Checkbox y RadioButton - Selección](#checkbox-y-radiobutton---selección)
    - [Checkbox](#checkbox)
    - [RadioButton](#radiobutton)
  - [LazyColumn - Listas dinámicas (como RecyclerView)](#lazycolumn---listas-dinámicas-como-recyclerview)
- [Temas y Estilos en Jetpack Compose (Material 3)](#temas-y-estilos-en-jetpack-compose-material-3)
  - [¿Qué es un Tema en Compose?](#qué-es-un-tema-en-compose)
  - [Estructura de theming](#estructura-de-theming)
  - [Definición de colores personalizados (`Color.kt`)](#definición-de-colores-personalizados-colorkt)
  - [Tipografía personalizada (Type.kt)](#tipografía-personalizada-typekt)
  - [Usar el tema dentro de tus Composables](#usar-el-tema-dentro-de-tus-composables)
  - [Estilos reutilizables y consistentes](#estilos-reutilizables-y-consistentes)
- [Arquitectura Recomendada: MVVM + Jetpack Compose](#arquitectura-recomendada-mvvm--jetpack-compose)
  - [Capas de la arquitectura](#capas-de-la-arquitectura)
  - [Estructura de paquetes sugerida](#estructura-de-paquetes-sugerida)
  - [Flujo de datos en Compose con MVVM](#flujo-de-datos-en-compose-con-mvvm)
  - [Ventajas del enfoque MVVM con Compose](#ventajas-del-enfoque-mvvm-con-compose)
  - [Previsualizar UI con fake ViewModel](#previsualizar-ui-con-fake-viewmodel)


# Introducción

Jetpack Compose es la revolucionaria herramienta declarativa de Google para construir interfaces de usuario en Android de forma moderna y eficiente. A diferencia del tradicional sistema basado en archivos XML y vistas imperativas, Compose permite diseñar la UI directamente en Kotlin, combinando reactividad, flexibilidad y simplicidad.

Este cambio de paradigma hace que crear interfaces sea mucho más intuitivo: describes qué quieres mostrar y Compose se encarga del cómo. Así, la UI se vuelve más mantenible, fácil de entender y altamente adaptable a los cambios de estado o configuración.

## ¿Por qué migrar a Compose?

* Menos código y más claridad: Se elimina gran parte del boilerplate y la fragmentación entre XML y lógica, facilitando la lectura y mantenimiento.
* Integración nativa con el ciclo de vida y ViewModel
* Soporte completo para Material Design
* Ideal para apps modernas, reactivas y mantenibles
* Productividad y velocidad: Gracias a las vistas previas en tiempo real (@Preview) y a un modelo declarativo, el desarrollo y prototipado son mucho más rápidos.

## Comparativa rápida: XML vs Compose

| Característica          | XML + Views                     | Jetpack Compose                  |
|-------------------------|----------------------------------|----------------------------------|
| Definición de UI        | Archivos XML                    | Funciones Kotlin (`@Composable`) |
| Reactividad             | Limitada                        | Reactivo por defecto              |
| Boilerplate             | Alto                            | Bajo                              |
| Preview en IDE          | Sí                              | Sí (más rápido y flexible)        |
| Mantenimiento           | Fragmentación en clases y XML   | Todo en un solo lugar (Kotlin)    |


## Requisitos Previos

* Android Studio **Hedgehog o superior**
* Kotlin **1.9.0 o superior**
* Experiencia con Android tradicional
* Gradle versión 8.0+

# Fundamentos de Jetpack Compose

Jetpack Compose introduce un enfoque declarativo para construir interfaces de usuario en Android. Esto significa que, en lugar de describir paso a paso cómo construir la UI, tú simplemente defines qué quieres mostrar y Compose se encarga de gestionarlo de forma eficiente y reactiva.

Entender los fundamentos de Compose es clave para sacarle el máximo provecho y construir apps modernas, escalables y fáciles de mantener. En esta sección exploraremos los conceptos básicos que todo desarrollador debe conocer para dominar Compose.

Uno de los grandes beneficios de Compose es que puedes construir tus propios componentes UI con estilos predefinidos para usarlos en toda la app:

```kotlin
@Composable
fun BotonPrimario(texto: String, onClick: () -> Unit) {
    Button(
        onClick = onClick,
        colors = ButtonDefaults.buttonColors(
            containerColor = MaterialTheme.colorScheme.primary
        ),
        modifier = Modifier.fillMaxWidth()
    ) {
        Text(
            text = texto,
            style = MaterialTheme.typography.bodyMedium,
            color = MaterialTheme.colorScheme.onPrimary
        )
    }
}
```

## ¿Qué es un `@Composable`?

Un @Composable es una función especial que describe una porción de la interfaz de usuario. En lugar de crear vistas manualmente o inflar XML, defines la UI usando funciones Kotlin anotadas con @Composable.

Estas funciones son puras en la medida que reciben datos y devuelven elementos visuales, pero lo más importante es que Compose las vuelve a ejecutar automáticamente cuando cambian los datos de los que dependen, manteniendo la UI siempre actualizada.

```kotlin
@Composable
fun Bienvenida(nombre: String) {
    Text(text = "Bienvenido, $nombre")
}
```

## Composición y recomposición

Cuando usas Compose, tu UI se representa como un árbol de composición similar al DOM en web. Cada llamada a una función @Composable agrega un nodo a este árbol.

* **Composición**: Es el proceso inicial donde Compose crea este árbol a partir de las funciones @Composable.
* **Recomposición**: Ocurre cuando los datos cambian y Compose debe actualizar solo las partes afectadas del árbol. Gracias a esto, la UI se actualiza de forma eficiente sin necesidad de reconstruir todo.

Este modelo reactivo permite que la UI siempre refleje el estado actual sin esfuerzo manual para sincronizar datos y vista.

## visualizar vistas previas (@Preview)

Una de las ventajas más potentes de Compose es la capacidad de previsualizar componentes directamente en Android Studio, sin necesidad de compilar y ejecutar la app en un emulador o dispositivo.

Al usar la anotación @Preview junto con tus funciones @Composable, puedes:
* Ver cómo se ve un componente en diferentes configuraciones (modo oscuro, tamaños, idiomas).
* Agilizar el desarrollo probando cambios visuales al instante.

Opciones comunes en @Preview:

| Opción           | Descripción                                |
| ---------------- | ------------------------------------------ |
| `showBackground` | Muestra un fondo claro                     |
| `name`           | Título de la preview                       |
| `showSystemUi`   | Simula navegación, barra de estado, etc.   |
| `uiMode`         | Cambia entre dark mode, night mode, etc.   |
| `locale`         | Simula localización (`"es"`, `"en"`, etc.) |

```kotlin
@Preview(showBackground = true, name = "Vista Bienvenida")
@Composable
fun PreviewBienvenida() {
    Bienvenida(nombre = "Carlos")
}
```

## Ciclo de vida básico en Jetpack Compose

Aunque Compose no usa los métodos tradicionales de ciclo de vida (onCreate, onResume, etc.) en sus funciones UI, tiene un ciclo propio basado en composición y recomposición:

| Etapa          | Equivalente en Views               | Descripción                                  |
| -------------- | ---------------------------------- | -------------------------------------------- |
| Composición    | `onCreateView()`                   | Construcción inicial del árbol de UI         |
| Recomposición  | `invalidate()` / `requestLayout()` | Actualización parcial ante cambios de estado |
| Descomposición | `onDestroyView()`                  | Limpieza de recursos y nodo del árbol        |

Este ciclo permite que Compose gestione automáticamente la creación, actualización y destrucción de UI sin que tengas que preocuparte por ello manualmente.

## Gestión de estado: remember y mutableStateOf

**¿Qué es el estado?**
En Compose, el estado representa los datos que pueden cambiar y que deben reflejarse en la UI, como texto ingresado, selección o conteo.

* remember: Retiene un valor en memoria mientras el Composable está presente en el árbol de composición. Evita que el valor se reinicie en recomposiciones, pero no lo conserva al rotar la pantalla o recrear la actividad.
* mutableStateOf: Crea un valor observable que cuando cambia provoca la recomposición automática de las funciones afectadas.

```kotlin
@Composable
fun Contador() {
    var contador by remember { mutableStateOf(0) }

    Button(onClick = { contador++ }) {
        Text("Contador: $contador")
    }
}
```
>Nota: Este estado se pierde si el Composable desaparece (por ejemplo, rotación de pantalla). Para conservarlo en esos casos usa rememberSaveable.


# Componentes Principales de Jetpack Compose

Jetpack Compose ofrece una colección rica de componentes UI reutilizables que reemplazan a los clásicos TextView, Button, RecyclerView, EditText, entre otros. Estos componentes son 100% declarativos, personalizables y adaptables al estado de la aplicación.

## Text

El componente Text se usa para mostrar texto en pantalla. Puedes personalizar su estilo, color, alineación y tipografía usando MaterialTheme.

```kotlin
Text(
    text = "Monto Total",
    style = MaterialTheme.typography.titleMedium,
    color = Color.Blue
)
```

## Buttons

Los botones ejecutan acciones al ser presionados. Puedes combinarlos con Text, íconos o estilos personalizados. También puedes usar variantes como OutlinedButton o TextButton.

```kotlin
Button(onClick = { /* Acción */ }) {
    Text("Guardar")
}
```

## Layout

Los layouts (diseños) son componentes @Composable que se utilizan para organizar y posicionar otros elementos de la interfaz de usuario en pantalla. Son el equivalente moderno de los LinearLayout, RelativeLayout, ConstraintLayout, etc., del sistema tradicional de Views.

### Box

Permite colocar elementos uno encima de otro, como un FrameLayout.

```kotlin
fun MyBox(){
    Box(Modifier.fillMaxSize(), contentAlignment = Alignment.Center){
        Box(
            Modifier
                .size(50.dp)
                .background(Color.Red)
                .verticalScroll(rememberScrollState())){
            Text("Hola Hola Hola Hola Hola Hola")
        }
    }
}
```

### Column (Vertical)

Organiza elementos uno debajo del otro (de arriba hacia abajo).

```kotlin
Column {
    Text("Opción 1")
    Text("Opción 2")
}
```

### Row (Horizontal)

Organiza elementos de forma horizontal (uno al lado del otro).

```kotlin
Row(verticalAlignment = Alignment.CenterVertically) {
    Text("Modo oscuro")
    Switch(checked = true, onCheckedChange = {})
}
```

## TextField - Entrada de datos

Los TextField permiten capturar texto del usuario. Son equivalentes a EditText en el sistema clásico.

``` kotlin
var nombre by rememberSaveable { mutableStateOf("") }

TextField(
    value = nombre,
    onValueChange = { nombre = it },
    label = { Text("Nombre del cliente") },
    modifier = Modifier.fillMaxWidth()
)
```

>Usa rememberSaveable para que el valor se mantenga tras rotar la pantalla.

## Checkbox y RadioButton - Selección

### Checkbox

``` kotlin
var aceptado by rememberSaveable { mutableStateOf(false) }

Row(verticalAlignment = Alignment.CenterVertically) {
    Checkbox(checked = aceptado, onCheckedChange = { aceptado = it })
    Text("Acepto términos y condiciones")
}
```

### RadioButton

``` kotlin
val opciones = listOf("Efectivo", "Tarjeta", "Transferencia")
var seleccion by rememberSaveable { mutableStateOf(opciones[0]) }

Column {
    opciones.forEach { opcion ->
        Row(verticalAlignment = Alignment.CenterVertically) {
            RadioButton(
                selected = (opcion == seleccion),
                onClick = { seleccion = opcion }
            )
            Text(opcion)
        }
    }
}
```

## LazyColumn - Listas dinámicas (como RecyclerView)

LazyColumn es el equivalente moderno de RecyclerView. Permite mostrar listas eficientes, con carga bajo demanda (lazy loading).

``` kotlin
val clientes = listOf("María", "Pedro", "Laura")

LazyColumn(modifier = Modifier.fillMaxSize()) {
    items(clientes) { cliente ->
        Text(
            text = cliente,
            modifier = Modifier
                .fillMaxWidth()
                .padding(12.dp)
        )
        Divider()
    }
}
```

>Puedes usar variantes como LazyRow (horizontal), o LazyColumn { itemsIndexed(...) } si necesitas el índice.

# Temas y Estilos en Jetpack Compose (Material 3)

Uno de los pilares de Jetpack Compose es su integración total con Material Design 3 (Material You), el sistema de diseño visual moderno de Google. Esto permite que tu aplicación tenga una apariencia profesional, coherente y adaptable con poco esfuerzo.

Compose facilita aplicar estilos globales y crear componentes consistentes mediante temas reutilizables, en lugar de definir colores o tipografías en cada elemento por separado.

## ¿Qué es un Tema en Compose?

Un **tema** en Jetpack Compose define la apariencia visual global de la app:
* Paleta de colores (`colorScheme`)
* Tipografía (`Typography`)
* Formas (`Shapes`)
* Estilos de componentes (`MaterialTheme`)

Gracias al tema, puedes cambiar el estilo completo de tu app en un solo lugar, sin necesidad de modificar cada Composable individualmente.

## Estructura de theming

Compose suele organizar los estilos en la carpeta ui/theme/, separando las distintas definiciones por tipo:

```
├── ui/
│   └── theme/
│       ├── Color.kt     // Paleta de colores
│       ├── Type.kt      // Tipografía
│       ├── Shape.kt     // Esquinas y formas (opcional)
│       └── Theme.kt     // Punto de entrada del tema

```

## Definición de colores personalizados (`Color.kt`)

Puedes crear tu propia paleta adaptada al branding de tu empresa o cliente:

```kotlin
val AzulEmpresarial = Color(0xFF0050B3)
val GrisFondo = Color(0xFFF5F5F5)
val RojoError = Color(0xFFD32F2F)
```

Luego se asignan dentro de un ColorScheme, para que MaterialTheme.colorScheme los reconozca globalmente.

## Tipografía personalizada (Type.kt)

Define estilos de texto globales para títulos, subtítulos y cuerpo:

```kotlin
val TipografiaEmpresarial = Typography(
    titleLarge = TextStyle(
        fontFamily = FontFamily.SansSerif,
        fontWeight = FontWeight.Bold,
        fontSize = 22.sp
    ),
    bodyMedium = TextStyle(
        fontSize = 16.sp
    )
)
```

Esto permite usar estilos consistentes en toda la aplicación con solo acceder a MaterialTheme.typography.

##  Usar el tema dentro de tus Composables

Este archivo es el punto central donde se unen los colores, tipografías y formas. Allí defines cómo se ve tu app

```kotlin
@Composable
fun MiAppTheme(content: @Composable () -> Unit) {
    val colores = lightColorScheme(
        primary = AzulEmpresarial,
        background = GrisFondo,
        error = RojoError
    )

    MaterialTheme(
        colorScheme = colores,
        typography = TipografiaEmpresarial,
        shapes = Shapes(), // si defines formas personalizadas
        content = content
    )
}
```

Y luego, simplemente envuelves tu app:

```kotlin
setContent {
    MiAppTheme {
        AppContent()
    }
}
```

## Estilos reutilizables y consistentes

Una vez aplicado el tema, puedes acceder a sus propiedades en cualquier parte de tu UI

```kotlin
Text(
    text = "Bienvenido",
    style = MaterialTheme.typography.titleLarge,
    color = MaterialTheme.colorScheme.primary
)

Button(
    onClick = { /* Acción */ },
    colors = ButtonDefaults.buttonColors(
        containerColor = MaterialTheme.colorScheme.primary
    )
) {
    Text("Aceptar")
}
```

# Arquitectura Recomendada: MVVM + Jetpack Compose

Jetpack Compose se integra de forma natural con arquitecturas modernas basadas en patrones como MVVM (Model - View - ViewModel), promoviendo un desarrollo limpio, escalable y testable.

Gracias a su enfoque declarativo y a la gestión de estado reactiva, Compose elimina la necesidad de controlar manualmente el ciclo de vida de la UI, haciendo que MVVM brille aún más como patrón de arquitectura base para aplicaciones empresariales.

## Capas de la arquitectura

| Capa       | Rol                                                                 |
|------------|----------------------------------------------------------------------|
| View       | UI declarativa (`@Composable`)                                       |
| ViewModel  | Maneja el estado de UI, lógica de presentación                       |
| Repository | Abstracción para acceder a datos (base de datos, red, etc.)         |
| Model      | Entidades y estructuras de datos                                     |

## Estructura de paquetes sugerida

Una organización modular y coherente del código es fundamental para escalar aplicaciones reales. Aquí tienes una estructura típica para una app basada en Compose + MVVM:

```
├── data/
│   ├── model/          # Clases de datos y entidades
│   └── repository/     # Acceso a datos (API, BD, etc.)
├── ui/
│   ├── screen/         # Pantallas (composables agrupados por feature)
│   ├── components/     # Elementos reutilizables
│   └── theme/          # Colores, tipografías y estilos globales
├── viewmodel/          # ViewModels por pantalla o feature
└── MainActivity.kt     # Punto de entrada de la app
```

## Flujo de datos en Compose con MVVM

View (Composable) <== Observa ==> ViewModel <== Lógica y datos ==> Repository / Model

* ViewModel expone el estado mediante State, StateFlow, o LiveData.
* @Composable se suscribe a ese estado y se reconfigura automáticamente cuando cambia.

## Ventajas del enfoque MVVM con Compose

| Ventaja                         | Descripción                                        |
| ------------------------------- | -------------------------------------------------- |
| Separación de responsabilidades | La UI no tiene lógica de negocio                   |
| Estados reactivos               | La UI se actualiza automáticamente con `StateFlow` |
| Pruebas más sencillas           | Puedes testear ViewModel sin depender de la UI     |
| Reutilización de componentes    | Composables pequeños y probados                    |

## Previsualizar UI con fake ViewModel

Para probar composables sin depender de un ViewModel real, puedes crear datos de prueba:

```kotlin
@Preview(showBackground = true)
@Composable
fun VistaPreview() {
    val contadorFalso = remember { mutableStateOf(10) }

    Column(horizontalAlignment = Alignment.CenterHorizontally) {
        Text("Valor actual: ${contadorFalso.value}")
        Button(onClick = { contadorFalso.value++ }) {
            Text("Sumar")
        }
    }
}
```