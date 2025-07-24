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
  - [Layout](#layout)
    - [Box](#box)
    - [Column (Vertical)](#column-vertical)
    - [Row (Horizontal)](#row-horizontal)
  - [Text](#text)
  - [TextField - Entrada de datos](#textfield---entrada-de-datos)
  - [Componente Buttons](#componente-buttons)
    - [Buttons](#buttons)
    - [OutlinedButton](#outlinedbutton)
    - [TextButton](#textbutton)
    - [ElevatedButton](#elevatedbutton)
    - [FilledTonalButton](#filledtonalbutton)
  - [Images e Iconos](#images-e-iconos)
  - [Icono](#icono)
  - [Image](#image)
    - [Imágenes desde la web (usando Coil)](#imágenes-desde-la-web-usando-coil)
  - [ProgressBar](#progressbar)
    - [CircularProgressIndicator](#circularprogressindicator)
    - [LinearProgressIndicator](#linearprogressindicator)
    - [Loading con Lottie (animaciones)](#loading-con-lottie-animaciones)
  - [Control de selección](#control-de-selección)
    - [Switch](#switch)
    - [Checkbox](#checkbox)
    - [TriStateCheckbox](#tristatecheckbox)
    - [RadioButton](#radiobutton)
  - [Slider y RangeSlider](#slider-y-rangeslider)
    - [Slider](#slider)
    - [RangeSlider](#rangeslider)
  - [DropdownMenu](#dropdownmenu)
    - [ExposedDropdownMenuBox](#exposeddropdownmenubox)
  - [Scaffold](#scaffold)
    - [TopAppBar](#topappbar)
    - [BottomAppBar](#bottomappbar)
    - [BottomNavigation](#bottomnavigation)
    - [FloatingActionButton (FAB)](#floatingactionbutton-fab)
    - [SnackbarHost y Snackbar](#snackbarhost-y-snackbar)
    - [Content (slot principal)](#content-slot-principal)
  - [Card](#card)
  - [Badge](#badge)
  - [Divider](#divider)
  - [Diálogos](#diálogos)
    - [AlertDialog](#alertdialog)
    - [DatePicker](#datepicker)
    - [TimePicker](#timepicker)
  - [Comportamientos avanzados](#comportamientos-avanzados)
    - [IntractionSource](#intractionsource)
    - [LaunchEffect](#launcheffect)
    - [DerivatedStatedOf](#derivatedstatedof)
- [Listas dinámicas (antiguos RecyclerView)](#listas-dinámicas-antiguos-recyclerview)
  - [LazyColumn](#lazycolumn)
  - [LazyRow](#lazyrow)
  - [LazyVerticalGrid](#lazyverticalgrid)
  - [LazyHorizontalGrid](#lazyhorizontalgrid)
  - [Gestión del estado de listas](#gestión-del-estado-de-listas)
- [Navegación](#navegación)
  - [Navegación Básica](#navegación-básica)
  - [Navegación con parámetros primitivos](#navegación-con-parámetros-primitivos)
  - [Navegación con parámetros complejos](#navegación-con-parámetros-complejos)
    - [Usar Parcelable](#usar-parcelable)
    - [Usar Serializable](#usar-serializable)
    - [Usar JSON (más flexible)](#usar-json-más-flexible)
  - [Navegación usando tipo genérico (Type-safe)](#navegación-usando-tipo-genérico-type-safe)
  - [Manejo del back stack](#manejo-del-back-stack)
  - [BackHandler](#backhandler)
- [Animaciones](#animaciones)
  - [\*AsState](#asstate)
  - [Crossfade](#crossfade)
  - [AnimatedContent](#animatedcontent)
  - [AnimatedContentSize](#animatedcontentsize)
  - [InfiniteTranstitio](#infinitetranstitio)
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

## Text

El componente Text se usa para mostrar texto en pantalla. Puedes personalizar su estilo, color, alineación y tipografía usando MaterialTheme.

```kotlin
Text(
    text = "Monto Total",
    style = MaterialTheme.typography.titleMedium,
    color = Color.Blue
)
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

## Componente Buttons

Los Buttons son componentes interactivos que permiten a los usuarios realizar acciones. En Jetpack Compose, existen varios tipos de botones basados en Material Design 3, cada uno con un estilo visual diferente para reflejar su importancia o propósito en la interfaz.

**Tipos principales**:
* Button: Botón principal con fondo sólido. Para acciones destacadas.
* OutlinedButton: Con borde y sin fondo. Para acciones secundarias.
* TextButton: Solo texto, sin fondo ni borde. Para acciones discretas.
* ElevatedButton: Con sombra destacada. Útil cuando el botón necesita resaltar sobre el fondo.
* FilledTonalButton: Fondo tonal (menos intenso que el principal). Para acciones secundarias con mayor visibilidad.

| Composable          | Fondo  | Borde | Elevación | Uso típico                          |
| ------------------- | ------ | ----- | --------- | ----------------------------------- |
| `Button`            | Sólido | No    | Baja      | Acción principal                    |
| `OutlinedButton`    | No     | Sí    | No        | Acción secundaria                   |
| `TextButton`        | No     | No    | No        | Acción menor/discreta               |
| `ElevatedButton`    | Claro  | No    | Alta      | Acción destacada, no principal      |
| `FilledTonalButton` | Tonal  | No    | Baja      | Acción secundaria visualmente clara |


### Buttons

Es el botón elevado estándar en Material Design. Tiene un fondo sólido y se utiliza para acciones principales.

**Características**:
* Color de fondo sólido (por defecto usa primary del tema).
* Elevación baja.
* Usa ButtonDefaults.buttonColors() para personalizar colores.
* Puede contener íconos y texto.

```kotlin
Button(
    onClick = {},
    colors = ButtonDefaults.buttonColors(
        containerColor = Color.Blue,
        contentColor = Color.White
    ),
    shape = RoundedCornerShape(8.dp),
    elevation = ButtonDefaults.buttonElevation(defaultElevation = 6.dp)
) {
    Icon(Icons.Default.Favorite, contentDescription = null)
    Spacer(Modifier.width(8.dp))
    Text("Favorito")
}
```

### OutlinedButton

Botón con un borde visible y fondo transparente. Útil para acciones secundarias.

**Características**:
* Borde visible (1dp) que usa el color outline del tema.
* Fondo transparente.
* Sin elevación.
* Usa ButtonDefaults.outlinedButtonColors().
  
```kotlin
OutlinedButton(
    onClick = {},
    border = BorderStroke(1.dp, Color.Gray),
    shape = RoundedCornerShape(12.dp)
) {
    Text("Cancelar")
}
```

### TextButton

Botón solo con texto, sin fondo ni borde. Ideal para acciones discretas o en diálogos.

```kotlin
TextButton(
    onClick = {},
    colors = ButtonDefaults.textButtonColors(
        contentColor = Color.Red
    )
) {
    Text("Eliminar")
}
```

**Características** :
* Sin fondo ni borde.
* Usualmente se usa en diálogos o barras inferiores.
* Usa ButtonDefaults.textButtonColors().

### ElevatedButton

Es un botón con una elevación más notoria, útil para destacarse sobre fondos de igual color.

```kotlin
ElevatedButton(onClick = { /* Acción */ }) {
    Text("Continuar")
}
```

**Características**:
* Más sombra que Button, pero fondo menos prominente.
* Útil cuando hay que resaltar una acción pero no tanto como el botón primario.
* Usa ButtonDefaults.elevatedButtonColors().

### FilledTonalButton

Es un botón con fondo tonal (menos prominente que el botón principal). Ideal para botones secundarios con más peso visual que un TextButton o OutlinedButton.

```kotlin
FilledTonalButton(onClick = { /* Acción */ }) {
    Text("Agregar")
}
```

**Características**:
* Fondo tonal (por ejemplo secondaryContainer).
* Suavemente elevado.
* Usa ButtonDefaults.filledTonalButtonColors().

## Images e Iconos

Estos composables se utilizan para mostrar elementos visuales como íconos e imágenes en la interfaz de usuario.

| Composable | Usado para    | Fuente de datos      | Escalable | Común en...             |
| ---------- | ------------- | -------------------- | --------- | ----------------------- |
| `Icon`     | Íconos vector | `Icons.Default`, SVG | Sí        | Botones, menús, etc.    |
| `Image`    | Imágenes      | Recursos, red        | Depende   | Avatares, ilustraciones |


## Icono

El composable Icon se utiliza para mostrar íconos vectoriales, como los de Icons.Default, Icons.Filled, o íconos personalizados.

```kotlin
Icon(
    imageVector = Icons.Filled.Home,
    contentDescription = "Inicio",
    tint = Color.Blue,
    modifier = Modifier.size(32.dp)
)
```

**Recursos**:
* Viene con paquetes como androidx.compose.material.icons.Icons.
* Puedes importar íconos desde SVG o utilizar librerías como Material Icons Extended.

**Parámetros importantes**:
* imageVector: Un ImageVector como los de Icons.Default o tus propios vectores.
* contentDescription: Descripción para accesibilidad (útil para lectores de pantalla)
* modifier: Para ajustar tamaño, padding, color, etc.
* tint: Color del ícono. Por defecto toma el color de LocalContentColor.

## Image

El composable Image se usa para mostrar imágenes rasterizadas o vectoriales desde archivos, recursos o URLs (con librerías).

```kotlin
Image(
    painter = painterResource(id = R.drawable.profile),
    contentDescription = "Foto de perfil",
    contentScale = ContentScale.Crop,
    modifier = Modifier
        .size(100.dp)
        .clip(CircleShape)
        .border(2.dp, Color.Gray, CircleShape)
)
```

**Parámetros importantes**:
* painter: Fuente de la imagen. Puede ser:
  * painterResource() para imágenes locales.
  * rememberImagePainter() o AsyncImage() (con Coil) para imágenes remotas.
* contentDescription: Importante para accesibilidad.
* contentScale: Cómo se escala la imagen (como Crop, FillBounds, Fit, etc.).
* modifier: Para ajustar tamaño, forma, etc.

### Imágenes desde la web (usando Coil)

Para cargar imágenes desde internet, puedes usar la librería Coil:

```grandle
implementation("io.coil-kt:coil-compose:2.4.0") // Revisa la última versión
```

```kotlin
import coil.compose.AsyncImage

AsyncImage(
    model = "https://example.com/image.png",
    contentDescription = "Imagen remota",
    contentScale = ContentScale.Crop,
    modifier = Modifier.size(120.dp)
)
```

## ProgressBar

Los indicadores de progreso son elementos visuales que informan al usuario que una operación está en curso. Pueden ser de progreso determinado (cuando se conoce cuánto falta) o indeterminado (cuando solo se sabe que está cargando).

| Composable                  | Tipo          | Determinado | Estilo         | Ideal para...                      |
| --------------------------- | ------------- | ----------- | -------------- | ---------------------------------- |
| `CircularProgressIndicator` | Nativo        | ✔️          | Círculo        | Carga general                      |
| `LinearProgressIndicator`   | Nativo        | ✔️          | Barra          | Descargas, formularios, etc.       |
| `LottieAnimation`           | Personalizado | ✔️/✖️       | Animación JSON | UI atractiva, animaciones modernas |


### CircularProgressIndicator

Muestra un círculo giratorio. Puede ser indeterminado (por defecto) o determinado (progreso entre 0.0 y 1.0).

* Uso indeterminado
```kotlin
CircularProgressIndicator()
```
* Uso determinado
```kotlin
CircularProgressIndicator(progress = 0.6f) // 60%
```
* Personalizacion
```kotlin
CircularProgressIndicator(
    progress = 0.75f,
    color = Color.Red,
    strokeWidth = 6.dp,
    modifier = Modifier.size(48.dp)
)
```

### LinearProgressIndicator

Muestra una barra horizontal que se llena. También puede ser indeterminado o determinado.

* Uso indeterminado
```kotlin
LinearProgressIndicator()
```
* Uso determinado
```kotlin
LinearProgressIndicator(progress = 0.4f) // 40%
```
* Personalizacion
```kotlin
LinearProgressIndicator(
    progress = 0.9f,
    color = Color.Green,
    trackColor = Color.LightGray,
    modifier = Modifier.fillMaxWidth().height(8.dp)
)
```
### Loading con Lottie (animaciones)

Usa animaciones JSON exportadas desde Lottie (por ejemplo desde lottiefiles.com) para mostrar animaciones atractivas mientras se carga contenido.

```grandle
implementation "com.airbnb.android:lottie-compose:6.3.0" // Verifica la última versión
```

```kotlin
import com.airbnb.lottie.compose.*

@Composable
fun LottieLoadingAnimation() {
    val composition by rememberLottieComposition(LottieCompositionSpec.RawRes(R.raw.loading))
    val progress by animateLottieCompositionAsState(composition)

    LottieAnimation(
        composition,
        progress,
        modifier = Modifier.size(150.dp)
    )
}
```

**Fuente de animación**:
* LottieCompositionSpec.RawRes(R.raw.loading): desde recursos.
* LottieCompositionSpec.Url("https://..."): desde la web.
* LottieCompositionSpec.Asset("loading.json"): desde assets.

```kotlin
val progress by animateLottieCompositionAsState(
    composition,
    iterations = LottieConstants.IterateForever,
    speed = 1.5f,
    isPlaying = true
)
```

## Control de selección

| Composable         | Tipo      | Estados                        | Selección múltiple | Uso común                         |
| ------------------ | --------- | ------------------------------ | ------------------ | --------------------------------- |
| `Switch`           | Binario   | On / Off                       | ❌                  | Configuraciones                   |
| `Checkbox`         | Binario   | Checked / Unchecked            | ✔️                 | Listas de opciones                |
| `TriStateCheckbox` | Ternario  | On / Off / Indeterminate       | ✔️ (con jerarquía) | Selección parcial en listas       |
| `RadioButton`      | Exclusivo | Seleccionado / No seleccionado | ❌ (1 por grupo)    | Formularios con una sola elección |


### Switch

Un interruptor deslizante (on/off). Útil para configurar estados como "Activado/Desactivado".

``` kotlin
Switch(
    checked = isChecked,
    onCheckedChange = { isChecked = it },
    colors = SwitchDefaults.colors(
        checkedThumbColor = Color.Green,
        uncheckedThumbColor = Color.Gray,
        checkedTrackColor = Color.LightGreen
    )
)
```

### Checkbox

Permite seleccionar o deseleccionar una opción. Puede usarse individualmente o en listas.

``` kotlin
Row(verticalAlignment = Alignment.CenterVertically) {
    Checkbox(
        checked = checked,
        onCheckedChange = { checked = it },
        colors = CheckboxDefaults.colors(
            checkedColor = Color.Blue,
            uncheckedColor = Color.Gray
        )
    )
    Text("Aceptar términos")
}
```

### TriStateCheckbox

Ideal para listas de selección jerárquica (por ejemplo, seleccionar "Todos", "Algunos", "Ninguno").

Permite tres estados:
* On (seleccionado) -> ToggleableState.On
* Off (no seleccionado) -> ToggleableState.Off
* Ideterminate (estado parcial) -> ToggleableState.Indeterminate

``` kotlin
var state by remember { mutableStateOf(ToggleableState.Indeterminate) }

TriStateCheckbox(
    state = state,
    onClick = {
        state = when (state) {
            ToggleableState.Off -> ToggleableState.On
            ToggleableState.On -> ToggleableState.Indeterminate
            ToggleableState.Indeterminate -> ToggleableState.Off
        }
    }
)
```

### RadioButton

Permite al usuario seleccionar una sola opción dentro de un grupo. Ideal para formularios con varias alternativas.

``` kotlin
var selectedOption by remember { mutableStateOf("Opción A") }

Row(verticalAlignment = Alignment.CenterVertically) {
    RadioButton(
        selected = selectedOption == "Opción A",
        onClick = { selectedOption = "Opción A" },
        colors = RadioButtonDefaults.colors(
            selectedColor = Color.Red,
            unselectedColor = Color.Gray
        )
    )
    Text("Opción A")
}

```

## Slider y RangeSlider

Los sliders son controles visuales que permiten al usuario seleccionar un valor (o rango de valores) dentro de un intervalo numérico definido. Son ideales para opciones como volumen, brillo, edad, precio, etc.

| Composable    | Tipo de valor           | Control de extremos | Uso común                      |
| ------------- | ----------------------- | ------------------- | ------------------------------ |
| `Slider`      | Un solo valor (`Float`) | Un thumb            | Volumen, edad, nivel           |
| `RangeSlider` | Rango (`Float..Float`)  | Dos thumbs          | Precio mínimo/máximo, duración |

### Slider

Un componente que permite seleccionar un solo valor dentro de un rango continuo o discreto

**Propiedades importantes**:
* value: Valor actual del slider.
* onValueChange: Callback que actualiza el valor.
* valueRange: Rango permitido (por ejemplo 0f..1f, 0f..100f).
* steps: Cantidad de pasos discretos (no incluye los extremos).
* enabled: Habilita o deshabilita el control.

```kotlin
Slider(
    value = sliderValue,
    onValueChange = { sliderValue = it },
    valueRange = 0f..10f,
    steps = 4, // Crea 5 pasos intermedios (1, 2, 3, 4)
    onValueChangeFinished = {
        println("Valor final: $sliderValue")
    },
    colors = SliderDefaults.colors(
        thumbColor = Color.Red,
        activeTrackColor = Color.Red,
        inactiveTrackColor = Color.Gray
    )
)
```

### RangeSlider

Permite seleccionar un rango de valores con dos "thumbs" (deslizadores). Ideal para filtros como "precio mínimo y máximo".

**Propiedades importantes**:
* values: Objeto ClosedFloatingPointRange<Float> con los valores seleccionados (ej. 10f..50f).
* onValueChange: Callback que actualiza el rango.
* valueRange: Rango total permitido.
* steps: Como en Slider, controla los pasos discretos.

```kotlin
RangeSlider(
    values = range,
    onValueChange = { range = it },
    valueRange = 0f..100f,
    steps = 9 // divide el rango en 10 pasos
)
```

## DropdownMenu

DropdownMenu es un componente de interfaz que muestra una lista de opciones flotantes debajo de un botón o icono al hacer clic. Es útil para menús de acciones, filtros, ajustes y selección contextual.

**Componentes clave**

| Propiedad          | Descripción                                                            |
| ------------------ | ---------------------------------------------------------------------- |
| `expanded`         | Controla si el menú está visible o no (`true` = visible).              |
| `onDismissRequest` | Se llama cuando el menú debería cerrarse (clic fuera o ESC).           |
| `DropdownMenuItem` | Representa una opción dentro del menú. Puede tener texto, íconos, etc. |
| `modifier`         | Puedes usarlo para alinear o limitar el tamaño del menú.               |

**Recomendaciones**
* DropdownMenu debe estar anclado a un elemento visual, normalmente dentro de un Box.
* Puedes combinarlo con un OutlinedTextField para crear un selector tipo “spinner”.
* Usa ExposedDropdownMenuBox si quieres un campo desplegable tipo AutoComplete.

```kotlin
var expanded by remember { mutableStateOf(false) }

Box {
    Button(onClick = { expanded = true }) {
        Text("Seleccionar opción")
    }

    DropdownMenu(
        expanded = expanded,
        onDismissRequest = { expanded = false },
        modifier = Modifier.width(180.dp)
    ) {
        DropdownMenuItem(
            leadingIcon = { Icon(Icons.Default.Settings, contentDescription = null) },
            text = { Text("Configuración") },
            onClick = { /* Acción */ expanded = false }
        )

        DropdownMenuItem(
            text = { Text("Opción 2") },
            onClick = { expanded = false }
        )
    }
}
```

**Comparativa entre DropdownMenu y ExposedDropdownMenuBox**

| Propiedad   | `DropdownMenu`               | `ExposedDropdownMenuBox`               |
| ----------- | ---------------------------- | -------------------------------------- |
| Anclaje     | Manual (usualmente en `Box`) | Automático con `OutlinedTextField`     |
| Apariencia  | Estilo flotante              | Campo editable con menú desplegable    |
| Uso común   | Menús contextuales           | Formularios y selección estilo spinner |
| Dependencia | Material 2 o 3               | Requiere `androidx.compose.material3`  |


### ExposedDropdownMenuBox

Ideal para campos de selección con apariencia de TextField

```kotlin
var expanded by remember { mutableStateOf(false) }
var selectedOption by remember { mutableStateOf("Opción A") }
val options = listOf("Opción A", "Opción B", "Opción C")

ExposedDropdownMenuBox(
    expanded = expanded,
    onExpandedChange = { expanded = !expanded }
) {
    OutlinedTextField(
        value = selectedOption,
        onValueChange = {},
        readOnly = true,
        label = { Text("Selecciona una opción") },
        trailingIcon = { ExposedDropdownMenuDefaults.TrailingIcon(expanded = expanded) },
        modifier = Modifier.menuAnchor()
    )

    ExposedDropdownMenu(
        expanded = expanded,
        onDismissRequest = { expanded = false }
    ) {
        options.forEach { selectionOption ->
            DropdownMenuItem(
                text = { Text(selectionOption) },
                onClick = {
                    selectedOption = selectionOption
                    expanded = false
                }
            )
        }
    }
}
```

## Scaffold

Scaffold es un contenedor de diseño de alto nivel en Jetpack Compose. Te proporciona una estructura básica para pantallas siguiendo Material Design, con slots (espacios) predeterminados para colocar:

* TopAppBar (barra superior)
* BottomAppBar o BottomNavigation
* FloatingActionButton (FAB)
* Drawer (navegación lateral)
* Snackbar
* Contenido principal (content)

**Parametros clave**

| Parámetro                      | Descripción                                                         |
| ------------------------------ | ------------------------------------------------------------------- |
| `topBar`                       | Slot para la `TopAppBar`.                                           |
| `bottomBar`                    | Slot para `BottomAppBar` o `BottomNavigation`.                      |
| `floatingActionButton`         | Botón flotante (FAB).                                               |
| `floatingActionButtonPosition` | Posición del FAB (`Center` o `End`).                                |
| `isFloatingActionButtonDocked` | Si el FAB debe estar acoplado al `BottomAppBar`.                    |
| `drawerContent`                | Contenido del menú lateral (Drawer).                                |
| `drawerGesturesEnabled`        | Habilita/deshabilita el deslizamiento lateral para abrir el Drawer. |
| `snackbarHost`                 | Permite mostrar mensajes con `SnackbarHost`.                        |
| `containerColor`               | Color de fondo general.                                             |
| `content`                      | Contenido principal de la pantalla. Recibe `PaddingValues`.         |

**Relación con otros composables**

| Composable             | Función                                    |
| ---------------------- | ------------------------------------------ |
| `TopAppBar`            | Barra de título, navegación, acciones      |
| `BottomAppBar`         | Barra inferior con botones o FAB           |
| `BottomNavigation`     | Navegación inferior con múltiples pestañas |
| `FloatingActionButton` | Botón flotante para acciones principales   |
| `Drawer`               | Menú lateral desplegable                   |
| `Snackbar`             | Mensaje temporal flotante                  |

**Estructura Basica**
```kotlin
@Composable
fun MiPantalla() {
    val scaffoldState = rememberScaffoldState()
    val coroutineScope = rememberCoroutineScope()

    Scaffold(
        scaffoldState = scaffoldState,
        topBar = {
            TopAppBar(
                title = { Text("Scaffold Demo") },
                navigationIcon = {
                    IconButton(onClick = {
                        coroutineScope.launch {
                            scaffoldState.drawerState.open()
                        }
                    }) {
                        Icon(Icons.Default.Menu, contentDescription = "Abrir menú")
                    }
                }
            )
        },
        drawerContent = {
            Text("Menú lateral", modifier = Modifier.padding(16.dp))
        },
        floatingActionButton = {
            FloatingActionButton(onClick = {
                coroutineScope.launch {
                    scaffoldState.snackbarHostState.showSnackbar("FAB presionado")
                }
            }) {
                Icon(Icons.Default.Add, contentDescription = "Agregar")
            }
        },
        content = { innerPadding ->
            Box(modifier = Modifier
                .fillMaxSize()
                .padding(innerPadding)
            ) {
                Text("Contenido principal", modifier = Modifier.align(Alignment.Center))
            }
        }
    )
}
```

### TopAppBar

La barra superior de la aplicación. Normalmente contiene el título de la pantalla, íconos de navegación y acciones.

* title: contenido principal (normalmente Text)
* navigationIcon: ícono para navegación (usualmente un Drawer)
* actions: lista de acciones (íconos a la derecha)

```kotlin
TopAppBar(
    title = { Text("Mi App") },
    navigationIcon = {
        IconButton(onClick = { /* abrir drawer */ }) {
            Icon(Icons.Default.Menu, contentDescription = "Menú")
        }
    },
    actions = {
        IconButton(onClick = { /* acción */ }) {
            Icon(Icons.Default.Settings, contentDescription = "Ajustes")
        }
    }
)
```

### BottomAppBar

Una barra fija en la parte inferior. Puede contener acciones, y opcionalmente un FAB anclado.

```kotlin
BottomAppBar {
    IconButton(onClick = { /* acción 1 */ }) {
        Icon(Icons.Default.Home, contentDescription = null)
    }
    Spacer(Modifier.weight(1f)) // para separar íconos
    IconButton(onClick = { /* acción 2 */ }) {
        Icon(Icons.Default.Settings, contentDescription = null)
    }
}
```

### BottomNavigation

Una barra inferior con íconos y texto, ideal para navegación entre secciones principales (tabs).

```kotlin
BottomNavigation {
    BottomNavigationItem(
        selected = true,
        onClick = { /* navegar */ },
        icon = { Icon(Icons.Default.Home, contentDescription = "Inicio") },
        label = { Text("Inicio") }
    )
    BottomNavigationItem(
        selected = false,
        onClick = { /* navegar */ },
        icon = { Icon(Icons.Default.Person, contentDescription = "Perfil") },
        label = { Text("Perfil") }
    )
}
```

### FloatingActionButton (FAB)

Un botón redondo que flota sobre el contenido. Suele representar una acción principal como “Agregar”.

```kotlin
FloatingActionButton(onClick = { /* acción */ }) {
    Icon(Icons.Default.Add, contentDescription = "Agregar")
}
```

**ExtendedFloatingActionButton**: incluye texto además del ícono.

```kotlin
ExtendedFloatingActionButton(
    icon = { Icon(Icons.Default.Add, contentDescription = null) },
    text = { Text("Nuevo") },
    onClick = { /* acción */ }
)
```

### SnackbarHost y Snackbar

Permite mostrar mensajes temporales informativos al usuario.

```kotlin
val result = snackbarHostState.showSnackbar(
    message = "¿Deshacer?",
    actionLabel = "Sí",
    duration = SnackbarDuration.Short
)
```

### Content (slot principal)

Este es el área central del Scaffold, donde va el contenido principal de la pantalla.

```kotlin
Scaffold(
    content = { innerPadding ->
        Box(modifier = Modifier.padding(innerPadding)) {
            Text("Contenido principal aquí")
        }
    }
)
```

>**Nota**:El parámetro innerPadding es importante para evitar que el contenido se solape con la topBar o bottomBar.

## Card

Card es un contenedor con estilo Material Design que ofrece una superficie con sombra, bordes redondeados y elevación. Se usa para agrupar contenido relacionado visualmente, como listas, detalles o tarjetas de presentación.

**Propiedades importantes**:
* modifier: para ajustar tamaño, margen, etc.
* elevation: sombra para dar profundidad.
* shape: bordes redondeados o personalizados.
* backgroundColor: color de fondo.
* contentColor: color del contenido interno.

```kotlin
Card(
    modifier = Modifier
        .padding(8.dp)
        .fillMaxWidth(),
    elevation = 8.dp,
    shape = RoundedCornerShape(12.dp)
) {
    Column(modifier = Modifier.padding(16.dp)) {
        Text("Título de la tarjeta", style = MaterialTheme.typography.h6)
        Text("Contenido de la tarjeta")
    }
}
```

## Badge

Badge es un pequeño indicador visual que muestra un número o un punto para notificaciones o estados (como mensajes no leídos o alertas).

* BadgedBox es el contenedor que posiciona el Badge respecto a otro contenido (ej. un ícono).
* Badge puede mostrar texto (como números) o simplemente un punto.

```kotlin
BadgedBox(
    badge = {
        Badge { Text("3") }
    }
) {
    Icon(Icons.Default.Email, contentDescription = "Correo")
}
```

## Divider

Divider es una línea fina que separa contenido visualmente, muy usada para dividir listas, secciones o áreas en la UI.

**Propiedades importantes**:
* color: color de la línea.
* thickness: grosor de la línea.
* modifier: para ajustar longitud o posición.

```kotlin
Column {
    Text("Sección 1")
    Divider(color = Color.Gray, thickness = 1.dp)
    Text("Sección 2")
}
```

## Diálogos

| Composable    | Función                                     | Nota importante                                      |
| ------------- | ------------------------------------------- | ---------------------------------------------------- |
| `AlertDialog` | Diálogo modal para alertas y confirmaciones | Composable nativo de Jetpack Compose                 |
| `DatePicker`  | Selección de fecha                          | Usar diálogo clásico de Android (`DatePickerDialog`) |
| `TimePicker`  | Selección de hora                           | Usar diálogo clásico de Android (`TimePickerDialog`) |


### AlertDialog

AlertDialog es un cuadro de diálogo modal que muestra información importante y generalmente requiere una acción del usuario (confirmar, cancelar, etc.). Es muy útil para alertas, confirmaciones o pedir permiso.

**Propiedades importantes**:
* onDismissRequest: llamado cuando el diálogo se debe cerrar (clic fuera o botón atrás).
* title: título del diálogo.
* text: contenido o mensaje.
* confirmButton: botón para confirmar.
* dismissButton: botón para cancelar o cerrar.

```kotlin
var openDialog by remember { mutableStateOf(true) }

if (openDialog) {
    AlertDialog(
        onDismissRequest = { openDialog = false },
        title = { Text("Título") },
        text = { Text("¿Quieres continuar?") },
        confirmButton = {
            TextButton(onClick = { 
                // acción de confirmar
                openDialog = false 
            }) {
                Text("Confirmar")
            }
        },
        dismissButton = {
            TextButton(onClick = { openDialog = false }) {
                Text("Cancelar")
            }
        }
    )
}
```

### DatePicker

Actualmente, Jetpack Compose no incluye un composable nativo oficial para DatePicker o TimePicker, pero puedes usar los diálogos clásicos de Android (MaterialDatePicker) integrados con Compose mediante APIs interoperables.

```gradle
implementation "androidx.compose.material:material:1.4.0" // o la versión que uses
```

```kotlin
@Composable
fun DatePickerDialogDemo() {
    val context = LocalContext.current
    val calendar = Calendar.getInstance()
    val year = calendar.get(Calendar.YEAR)
    val month = calendar.get(Calendar.MONTH)
    val day = calendar.get(Calendar.DAY_OF_MONTH)

    var selectedDate by remember { mutableStateOf("") }
    val datePickerDialog = remember {
        DatePickerDialog(
            context,
            { _, year, month, dayOfMonth ->
                selectedDate = "$dayOfMonth/${month + 1}/$year"
            },
            year,
            month,
            day
        )
    }

    Button(onClick = { datePickerDialog.show() }) {
        Text(text = "Seleccionar fecha")
    }

    if (selectedDate.isNotEmpty()) {
        Text(text = "Fecha seleccionada: $selectedDate")
    }
}
```

### TimePicker

Al igual que el DatePicker, Jetpack Compose no tiene un TimePicker nativo aún, pero puedes usar el clásico TimePickerDialog de Android integrado en Compose.

```kotlin
@Composable
fun TimePickerDialogDemo() {
    val context = LocalContext.current
    val calendar = Calendar.getInstance()
    val hour = calendar.get(Calendar.HOUR_OF_DAY)
    val minute = calendar.get(Calendar.MINUTE)

    var selectedTime by remember { mutableStateOf("") }

    val timePickerDialog = remember {
        TimePickerDialog(
            context,
            { _, selectedHour, selectedMinute ->
                selectedTime = String.format("%02d:%02d", selectedHour, selectedMinute)
            },
            hour,
            minute,
            true
        )
    }

    Button(onClick = { timePickerDialog.show() }) {
        Text("Seleccionar hora")
    }

    if (selectedTime.isNotEmpty()) {
        Text("Hora seleccionada: $selectedTime")
    }
}
```
## Comportamientos avanzados

| Composable / API    | Propósito principal                                   | Reactivo a cambios          | Uso común                         |
| ------------------- | ----------------------------------------------------- | --------------------------- | --------------------------------- |
| `InteractionSource` | Detectar interacciones del usuario (clic, foco, etc.) | Sí                          | Botones, inputs, efectos visuales |
| `LaunchedEffect`    | Ejecutar efectos secundarios controlados              | Sí, por clave               | Coroutines, animaciones, eventos  |
| `derivedStateOf`    | Calcular estados derivados optimizados                | Sí, si dependencias cambian | Filtrado, cálculos UI             |


### IntractionSource

InteractionSource es una clase que captura interacciones del usuario con un componente de la interfaz (como clics, enfoque, presionado, arrastrado, etc.). Se usa para observar el estado de interacción y reaccionar visualmente o lógicamente.

* Cambiar colores o animaciones al presionar.
* Detectar foco o estado de entrada personalizado.
* Crear componentes altamente interactivos y responsivos.

```kotlin
val interactionSource = remember { MutableInteractionSource() }
val isPressed by interactionSource.collectIsPressedAsState()

Button(
    onClick = { /* Acción */ },
    interactionSource = interactionSource
) {
    Text(if (isPressed) "Presionado" else "No presionado")
}
```

### LaunchEffect

LaunchedEffect es un composable que ejecuta código suspendido (coroutines) cuando una clave cambia o cuando se compone por primera vez. Es la forma recomendada de hacer efectos secundarios controlados en Compose.

* Mostrar Snackbars
* Lanzar animaciones
* Llamar APIs asincrónicas
* Escuchar eventos

```kotlin
LaunchedEffect(Unit) {
    delay(1000)
    println("Efecto lanzado al componer")
}
```

### DerivatedStatedOf

derivedStateOf es una función que crea un estado derivado computado, basado en otros estados. Solo se vuelve a calcular si la(s) dependencia(s) cambia(n), lo que mejora el rendimiento.

* Evitar recálculos innecesarios de valores derivados.
* Computar filtros, conteos, mapeos, validaciones, etc.
* Mantener la UI eficiente.

```kotlin
val list by remember { mutableStateOf(listOf(1, 2, 3, 4)) }
val evenCount by remember {
    derivedStateOf { list.count { it % 2 == 0 } }
}

Text("Números pares: $evenCount")
```

# Listas dinámicas (antiguos RecyclerView)

| Composable           | Dirección  | Tipo    | Ideal para             |
| -------------------- | ---------- | ------- | ---------------------- |
| `LazyColumn`         | Vertical   | Lista   | Chats, configuraciones |
| `LazyRow`            | Horizontal | Lista   | Carruseles, íconos     |
| `LazyVerticalGrid`   | Vertical   | Rejilla | Galerías, tarjetas     |
| `LazyHorizontalGrid` | Horizontal | Rejilla | Mosaicos desplazables  |
| `LazyListState`      | —          | Estado  | Control del scroll     |


## LazyColumn

Es una lista vertical que carga solo los elementos visibles en pantalla (renderizado perezoso). Ideal para listas largas como feeds, mensajes o configuraciones.

**Propiedades útiles**:
* contentPadding: agrega padding interior.
* verticalArrangement: controla el espacio entre ítems.
* reverseLayout: invierte el orden visual (útil para chats).
* state: puedes usar rememberLazyListState() para manejar scroll, posición, etc

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

## LazyRow

Es igual que LazyColumn, pero con disposición horizontal. Ideal para carruseles, categorías, tarjetas desplazables.

```kotlin
LazyRow(
    horizontalArrangement = Arrangement.spacedBy(8.dp),
    contentPadding = PaddingValues(horizontal = 16.dp)
) {
    items(20) { index ->
        Box(
            modifier = Modifier
                .size(100.dp)
                .background(Color.Gray),
            contentAlignment = Alignment.Center
        ) {
            Text("Item $index")
        }
    }
}
```

## LazyVerticalGrid

Requiere androidx.compose.foundation:foundation

Una cuadrícula vertical tipo rejilla. Ideal para mostrar imágenes, tarjetas, íconos, etc.

**Tipos de columnas**
* GridCells.Fixed(n): número fijo de columnas.
* GridCells.Adaptive(minSize): ajusta el número según el ancho disponible.

```kotlin
LazyVerticalGrid(
    columns = GridCells.Fixed(2),
    contentPadding = PaddingValues(8.dp),
    verticalArrangement = Arrangement.spacedBy(8.dp),
    horizontalArrangement = Arrangement.spacedBy(8.dp)
) {
    items(20) { index ->
        Box(
            modifier = Modifier
                .aspectRatio(1f)
                .background(Color.LightGray),
            contentAlignment = Alignment.Center
        ) {
            Text("Item $index")
        }
    }
}
```

## LazyHorizontalGrid

Una cuadrícula horizontal. Similar a LazyRow, pero con múltiples filas.

```kotlin
LazyHorizontalGrid(
    rows = GridCells.Fixed(2),
    modifier = Modifier
        .height(200.dp)
        .fillMaxWidth(),
    horizontalArrangement = Arrangement.spacedBy(8.dp),
    verticalArrangement = Arrangement.spacedBy(8.dp),
    contentPadding = PaddingValues(8.dp)
) {
    items(30) { index ->
        Box(
            modifier = Modifier
                .size(100.dp)
                .background(Color.Cyan),
            contentAlignment = Alignment.Center
        ) {
            Text("Item $index")
        }
    }
}
```
## Gestión del estado de listas

Jetpack Compose permite controlar el estado de scroll con rememberLazyListState().

**Cosas que puedes hacer con el estado**:
* Detectar el índice visible
* Desplazarte programáticamente
* Detectar si llegaste al final

```kotlin
val listState = rememberLazyListState()

LazyColumn(state = listState) {
    items(50) { Text("Ítem $it") }
}
```

# Navegación

Para usar navegación en Jetpack Compose, necesitas estas dependencias:

```kotlin
implementation "androidx.navigation:navigation-compose:2.7.5" // o la versión más reciente
```

## Navegación Básica

```kotlin
@Composable
fun AppNavigation() {
    val navController = rememberNavController()

    NavHost(navController, startDestination = "home") {
        composable("home") { HomeScreen(navController) }
        composable("details") { DetailsScreen() }
    }
}

@Composable
fun HomeScreen(navController: NavController) {
    Button(onClick = { navController.navigate("details") }) {
        Text("Ir a detalles")
    }
}
```

## Navegación con parámetros primitivos

Jetpack Compose permite pasar strings, ints, booleans, floats como parámetros en la ruta.

```kotlin
NavHost(navController, startDestination = "profile/{userId}") {
    composable("profile/{userId}") { backStackEntry ->
        val userId = backStackEntry.arguments?.getString("userId")
        ProfileScreen(userId)
    }
}

navController.navigate("profile/12345")
```

## Navegación con parámetros complejos

Los objetos complejos no se pueden pasar directamente en la ruta. Hay tres formas de hacerlo:

### Usar Parcelable
```kotlin
@Parcelize
data class User(val id: Int, val name: String) : Parcelable

// Navegacion
navController.currentBackStackEntry?.savedStateHandle?.set("user", user)
navController.navigate("profile")

// Recibirlo
val user = navController
    .previousBackStackEntry
    ?.savedStateHandle
    ?.get<User>("user")
```

### Usar Serializable

Misma lógica que Parcelable, pero con Serializable. Menos eficiente.

```kotlin
@Serializable
data class Product(val id: String, val price: Double) : java.io.Serializable

// Navegacion
navController.currentBackStackEntry?.savedStateHandle?.set("user", user)
navController.navigate("profile")

// Recibirlo
val user = navController
    .previousBackStackEntry
    ?.savedStateHandle
    ?.get<User>("user")
```

### Usar JSON (más flexible)

Con Gson o Moshi puedes convertir el objeto a JSON y pasarlo como string.

```kotlin
// Envio
val json = Uri.encode(Gson().toJson(product))
navController.navigate("productDetails/$json")

// Recibirlo
val json = backStackEntry.arguments?.getString("product")
val product = Gson().fromJson(json, Product::class.java)
```

> Ten en cuenta el límite de longitud de la ruta (~2kb).

## Navegación usando tipo genérico (Type-safe)

```kotlin
inline fun <reified T : Parcelable> NavController.navigateWithObject(
    route: String,
    key: String,
    value: T
) {
    this.currentBackStackEntry?.savedStateHandle?.set(key, value)
    this.navigate(route)
}

inline fun <reified T : Parcelable> NavBackStackEntry?.getObject(key: String): T? {
    return this?.savedStateHandle?.get<T>(key)
}

navController.navigateWithObject("details", "user", user)

val user = navBackStackEntry.getObject<User>("user")
```

## Manejo del back stack
```kotlin
navController.popBackStack()

navController.navigate("route") {
    popUpTo("currentRoute") { inclusive = true }
}

navController.navigate("home") {
    popUpTo(0)
}
```

## BackHandler

Intercepta la pulsación del botón físico de volver (back) para ejecutar lógica personalizada

**Puedes usarlo para**:

* Mostrar un diálogo de confirmación.
* Prevenir navegación no deseada.
* Implementar flujos tipo wizard (paso a paso).

```kotlin
BackHandler(enabled = true) {
    // Acción personalizada
    showExitDialog = true
}
```

# Animaciones

| API                          | Función                                  | Ideal para                      |
| ---------------------------- | ---------------------------------------- | ------------------------------- |
| `animate*AsState`            | Anima un valor al cambiar                | Tamaño, color, opacidad         |
| `Crossfade`                  | Cambia de un contenido a otro con fade   | Alternar pantallas/íconos       |
| `AnimatedContent`            | Transiciones de contenido con animación  | Contenido dinámico más complejo |
| `animateContentSize`         | Anima el cambio de tamaño del componente | Expansión de tarjetas, diálogos |
| `rememberInfiniteTransition` | Animación infinita                       | Carga, parpadeo, loops visuales |


## *AsState

Es una API que permite animar cualquier valor de forma automática cuando cambia.

**Variantes disponibles**:
* animateDpAsState
* animateFloatAsState
* animateColorAsState
* animateIntAsState
* animateOffsetAsState, etc.

```kotlin
import androidx.compose.animation.core.animate*AsState

val expanded = remember { mutableStateOf(false) }

val boxSize by animateDpAsState(
    targetValue = if (expanded.value) 200.dp else 100.dp,
    animationSpec = tween(durationMillis = 500)
)

Box(
    Modifier
        .size(boxSize)
        .background(Color.Blue)
        .clickable { expanded.value = !expanded.value }
)
```

## Crossfade

Permite animar entre dos contenidos diferentes con una animación de desvanecimiento cruzado.

**Puedes usarlo para**:
* Cambiar entre pantallas
* Mostrar estados vacíos/cargados
* Alternar íconos o vistas

```kotlin
var selected by remember { mutableStateOf(true) }

Crossfade(targetState = selected) { isSelected ->
    if (isSelected) {
        Text("Hola")
    } else {
        Icon(Icons.Default.Star, contentDescription = null)
    }
}
```

## AnimatedContent

Permite animar transiciones de contenido entre dos estados con mayor control que Crossfade, incluyendo animación de entrada y salida.

**Personalizable con**:
* transitionSpec
* Animaciones combinadas: slideIn + fadeIn with slideOut + fadeOut

```kotlin
var count by remember { mutableStateOf(0) }

AnimatedContent(targetState = count, transitionSpec = {
    slideInVertically { it } + fadeIn() with slideOutVertically { -it } + fadeOut()
}) { targetCount ->
    Text("Count: $targetCount")
}
```

## AnimatedContentSize

Es una extensión de Modifier que anima el cambio de tamaño de un componente.

**Ideal para**:
* Animar expansión de tarjetas
* Evitar cambios bruscos de tamaño
* Añadir suavidad a layouts dinámicos

```kotlin
var expanded by remember { mutableStateOf(false) }

Box(
    modifier = Modifier
        .clickable { expanded = !expanded }
        .background(Color.Gray)
        .animateContentSize() // 👈 aquí
        .padding(16.dp)
) {
    Text(if (expanded) "Texto largo con más líneas" else "Texto corto")
}
```

## InfiniteTranstitio

Permite crear una animación infinita (sin fin), útil para efectos visuales como pulsos, rotaciones, cargas, etc.

**Se usa comúnmente para**:
* Indicadores de carga
* Brillos o efectos pulsantes
* Animaciones visuales decorativas

```kotlin
val infiniteTransition = rememberInfiniteTransition()

val alpha by infiniteTransition.animateFloat(
    initialValue = 0.3f,
    targetValue = 1f,
    animationSpec = infiniteRepeatable(
        animation = tween(1000),
        repeatMode = RepeatMode.Reverse
    )
)

Box(
    modifier = Modifier
        .size(100.dp)
        .background(Color.Red.copy(alpha = alpha))
)
```

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