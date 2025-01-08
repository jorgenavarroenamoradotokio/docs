<div align="center">
  <img src="https://raw.githubusercontent.com/jorgenavarroenamoradotokio/docs/main/logos/Redis-logo.svg">
</div>

## Índice
- [Introducción](#introducción)
  - [Ventajas de GraphQL frente a REST](#ventajas-de-graphql-frente-a-rest)
  - [Conceptos Clave](#conceptos-clave)
  - [Diferencias entre GraphQL Server y GraphQL Client en Arquitectura](#diferencias-entre-graphql-server-y-graphql-client-en-arquitectura)
- [Diseño y Estructuración del Schema](#diseño-y-estructuración-del-schema)
  - [Consideraciones al Diseñar un Schema](#consideraciones-al-diseñar-un-schema)
  - [Mejores Prácticas en la Definición de Esquemas Escalables](#mejores-prácticas-en-la-definición-de-esquemas-escalables)
  - [Uso de Interfaces y Unions para Estructurar Esquemas Complejos](#uso-de-interfaces-y-unions-para-estructurar-esquemas-complejos)
  - [Organización Modular del Esquema](#organización-modular-del-esquema)
  - [Manejo de Tipos Personalizados (Scalars) y Validaciones](#manejo-de-tipos-personalizados-scalars-y-validaciones)
  - [Evolución del Esquema: Deprecación de Campos y Versionado](#evolución-del-esquema-deprecación-de-campos-y-versionado)
- [Queries, Mutations y Subscriptions avanzadas](#queries-mutations-y-subscriptions-avanzadas)
  - [Queries Avanzadas](#queries-avanzadas)
  - [Mutations](#mutations)
  - [Subscriptions](#subscriptions)
  - [Técnicas de Fragmentación y Reutilización de Consultas](#técnicas-de-fragmentación-y-reutilización-de-consultas)
- [Resolvers](#resolvers)
  - [Organización y Estructuración de Resolvers](#organización-y-estructuración-de-resolvers)
  - [Uso de DataLoader para Optimización y Prevención de Problemas de N+1](#uso-de-dataloader-para-optimización-y-prevención-de-problemas-de-n1)
  - [Encadenamiento de Resolvers y Composición de Lógica de Negocio](#encadenamiento-de-resolvers-y-composición-de-lógica-de-negocio)
  - [Manejo de Errores en Resolvers](#manejo-de-errores-en-resolvers)


# Introducción
GraphQL es un lenguaje de consulta para APIs y un entorno de ejecución que satisface esas consultas utilizando un esquema de datos definido por el desarrollador. Fue desarrollado por Facebook en 2012 y se lanzó al público en 2015. GraphQL permite a los clientes solicitar exactamente los datos que necesitan, sin importar la complejidad de la estructura del servidor o la profundidad de la relación entre los datos.

## Ventajas de GraphQL frente a REST
- Flexibilidad en las Consultas
En REST, cada recurso generalmente se expone mediante una URL específica, y para obtener datos relacionados, los clientes deben realizar múltiples solicitudes a diferentes endpoints. En GraphQL, los clientes pueden realizar una única consulta para recuperar múltiples recursos, estructurando la respuesta según sus necesidades.
Ejemplo práctico: En REST, una aplicación que necesita información del usuario y sus publicaciones podría requerir dos endpoints (/user y /user/posts). En GraphQL, una consulta puede obtener ambos datos simultáneamente.
- Performance Mejorada
Reducción de Overfetching y Underfetching: En REST, las respuestas suelen incluir datos que el cliente no necesita (overfetching) o carecen de información adicional que requiere otra solicitud (underfetching). GraphQL elimina este problema permitiendo al cliente definir exactamente qué campos y relaciones necesita.
Optimización de la Red: Una sola solicitud de GraphQL puede reemplazar múltiples llamadas REST, reduciendo el tiempo de ida y vuelta (RTT) y optimizando el uso del ancho de banda.
- Evolución de APIs sin Rupturas (Backward Compatibility)
En GraphQL, las nuevas funcionalidades se añaden al esquema sin afectar las consultas existentes. Los campos obsoletos permanecen accesibles mientras los clientes migran a las nuevas versiones.
- Documentación Incorporada
GraphQL incluye introspección, lo que permite a los clientes inspeccionar el esquema y descubrir qué operaciones y tipos están disponibles. Herramientas como GraphiQL o Apollo Studio aprovechan esta característica para ofrecer interfaces interactivas y de autocompletado.
- Ecosistema Declarativo y Orientado al Cliente
GraphQL permite a los desarrolladores definir requisitos de datos en un formato declarativo, lo que resulta en aplicaciones front-end más predecibles y modulares.

## Conceptos Clave
- Schema: El schema es el núcleo de GraphQL y define la forma de los datos que el servidor puede proporcionar. Describe los tipos de datos disponibles, sus campos y relaciones, y los métodos para acceder y modificar esos datos.
Tipos Escalares: Definen datos primitivos como String, Int, Float, Boolean y ID.
Tipos Personalizados: Representan entidades complejas como User o Product.

```graphql
type User {
  id: ID!
  name: String!
  posts: [Post]
}

type Post {
  id: ID!
  title: String!
  content: String
}

type Query {
  getUser(id: ID!): User
  getPosts: [Post]
}
```

- Queries: Las queries son solicitudes de lectura que el cliente realiza para obtener datos. Son análogas a las operaciones GET en REST.
- Mutations: Las mutations se utilizan para realizar operaciones de escritura o modificación, como crear, actualizar o eliminar datos. Son equivalentes a las operaciones POST, PUT, PATCH y DELETE en REST.
- Subscriptions: Las subscriptions permiten a los clientes recibir notificaciones en tiempo real cuando ocurren cambios en el servidor. Utilizan WebSockets para mantener una conexión persistente.
- Resolvers: Los resolvers son funciones responsables de conectar las operaciones del esquema con las fuentes de datos subyacentes (como bases de datos, APIs externas, etc.).

## Diferencias entre GraphQL Server y GraphQL Client en Arquitectura
- GraphQL Server
El servidor GraphQL es el punto central que expone el esquema y gestiona las solicitudes de los clientes. Actúa como un middleware entre los clientes y las fuentes de datos.
Responsabilidades Principales:
  - Definir el schema.
  - Resolver consultas y mutaciones utilizando funciones resolvers.
  - Integrarse con sistemas de backend como bases de datos, microservicios o APIs externas.
  - Manejar la autorización y la autenticación.
  - Optimizar las respuestas mediante técnicas como data loaders para reducir solicitudes redundantes a la base de datos.

Ecosistema Popular para Servidores:
  - Node.js: Apollo Server, Express GraphQL.
  - Otros Lenguajes: GraphQL Ruby, Graphene (Python), GraphQL .NET.

- GraphQL Client
El cliente GraphQL es la interfaz que consume la API, típicamente en aplicaciones front-end. Facilita la creación de consultas, manejo de cache, estado de la aplicación, y suscripciones en tiempo real.

Responsabilidades Principales:
  - Construir y enviar consultas al servidor.
  - Gestionar el estado de los datos (cache local, normalización, y reactividad).
  - Manejar errores y reintentos de solicitudes fallidas.
  - Proveer herramientas de depuración para desarrollo.

Ecosistema Popular para Clientes:
  - Apollo Client: Soporte completo para queries, mutations, subscriptions y caching.
  - Relay: Diseñado para aplicaciones escalables con un enfoque en la eficiencia del runtime.
  - Urql: Cliente ligero y modular.

# Diseño y Estructuración del Schema
El esquema de GraphQL es el núcleo de cualquier API GraphQL. Actúa como contrato entre el cliente y el servidor, definiendo qué datos están disponibles, sus relaciones y cómo pueden interactuar. Un esquema bien diseñado es esencial para garantizar escalabilidad, claridad y facilidad de mantenimiento.

## Consideraciones al Diseñar un Schema
- Modelado de Datos
  - Analizar las entidades principales de la aplicación y sus relaciones.
  - Traducir las entidades a tipos (type) de GraphQL.
- Consultas y Mutaciones
  - Identificar las operaciones comunes que realizarán los clientes.
  - Crear un tipo Query para las operaciones de lectura y un tipo Mutation para las de escritura
- Modularidad: Mantener el esquema organizado y segmentado en módulos para facilitar el mantenimiento.
- Validación de Entradas y Salidas: Utilizar tipos personalizados para garantizar que los datos cumplen con las expectativas.

##  Mejores Prácticas en la Definición de Esquemas Escalables
- Mantener la Consistencia
  - Utilizar una convención de nombres clara y consistente para tipos, campos y argumentos.
  - Ejemplo: getUser, createPost son preferibles a fetchUser o addPost.
- Limitar las Consultas Profundas: Prevenir consultas excesivamente complejas utilizando herramientas como limite de profundidad o cost analysis.
- Documentación Incorporada: Documentar cada campo y tipo en el esquema para facilitar su comprensión
- Usar Enum para Valores Finitos: Reemplazar cadenas repetitivas por enum para evitar errores de entrada
- Evitar Sobrecarga del Tipo Root: No abarrotar Query o Mutation. En su lugar, organizar operaciones por contexto

## Uso de Interfaces y Unions para Estructurar Esquemas Complejos
- Interfaces: Una interface define un conjunto de campos comunes que deben implementarse en múltiples tipos. Ej, Si tenemos varios tipos de contenido (artículos, videos, etc.), podemos usar una interface Content
- Unions: Las unions permiten definir un campo que puede devolver diferentes tipos, sin necesidad de campos comunes.

## Organización Modular del Esquema
- Schema Stitching: El schema stitching permite combinar múltiples esquemas GraphQL en uno solo. Ideal para aplicaciones con servicios independientes.
- Federation: La federación (GraphQL Federation) de Apollo es una arquitectura más avanzada para construir esquemas distribuidos.

## Manejo de Tipos Personalizados (Scalars) y Validaciones
- GraphQL incluye tipos escalares básicos como Int, Float, String, Boolean, e ID, pero también permite crear tipos personalizados.
- Validaciones: Se pueden usar resolvers para realizar validaciones adicionales

## Evolución del Esquema: Deprecación de Campos y Versionado
- Deprecación de Campos: GraphQL permite marcar campos como obsoletos sin romper las consultas existentes
- Versionado: Aunque GraphQL evita el versionado explícito de APIs, se pueden manejar versiones a través de tipos y entradas

# Queries, Mutations y Subscriptions avanzadas
## Queries Avanzadas
- Queries Anidadas: GraphQL permite realizar consultas anidadas, lo que resulta útil para explorar relaciones complejas entre los datos. Estas consultas aprovechan la naturaleza jerárquica del esquema.
- Paginación: La paginación es fundamental para manejar grandes cantidades de datos. GraphQL soporta dos enfoques comunes:
  - Offset-Based: Utiliza un índice de desplazamiento y un límite.
  - Cursor-Based: Utiliza un cursor único para manejar eficientemente datos dinámicos.

## Mutations 
- Operaciones CRUD: Las mutations se utilizan para crear, leer, actualizar y eliminar datos
- Bulk Updates: Para manejar actualizaciones masivas, se puede aceptar una lista de entradas

## Subscriptions
Las subscriptions permiten a los clientes recibir datos en tiempo real cuando ocurren cambios en el servidor.

## Técnicas de Fragmentación y Reutilización de Consultas
- Uso de Fragmentos: Los fragmentos permiten reutilizar estructuras de consultas y mantener el código limpio.
- Consultas Parametrizadas: Se pueden reutilizar consultas mediante parámetros

# Resolvers
Los resolvers son funciones responsables de procesar las solicitudes de los clientes en GraphQL. Cada campo de un esquema está vinculado a un resolver que se ejecuta para devolver los datos solicitados.
- Contexto (context) El contexto es un objeto compartido que contiene información global (como usuarios autenticados, bases de datos, etc.) accesible por todos los resolvers en una ejecución.
- Parent (Root) El argumento parent permite encadenar resolvers para campos dependientes.
- Arguments (args) Los argumentos permiten filtrar o modificar los datos consultados.

## Organización y Estructuración de Resolvers
Conforme crece una API, organizar los resolvers por modelo o dominio se vuelve esencial para mantener el código limpio y escalable.
- Organización por Dominio: Dividir los resolvers en módulos según el modelo o el dominio de la aplicación

## Uso de DataLoader para Optimización y Prevención de Problemas de N+1
El Problema de N+1. Cuando se consulta una lista de elementos relacionados, puede generarse una gran cantidad de consultas innecesarias a la base de datos. En este caso, una consulta para obtener usuarios puede desencadenar múltiples consultas adicionales para obtener publicaciones de cada usuario.
DataLoader es una herramienta que agrupa y cachea consultas para optimizar el acceso a datos.
```bash
npm install dataloader
```
- Ventajas de DataLoader
  - Evita consultas redundantes a la base de datos.
  - Reduce la latencia al agrupar solicitudes.
  - Cachea resultados para futuras consultas.

## Encadenamiento de Resolvers y Composición de Lógica de Negocio
- Encadenamiento de Resolvers: Permite dividir la lógica en pequeños fragmentos reutilizables.
- Composición de Lógica de Negocio: Se puede usar un patrón de middleware en resolvers para aplicar validaciones o transformaciones comunes.
  - Middleware

## Manejo de Errores en Resolvers
- Errores Personalizados: GraphQL permite devolver errores personalizados para proporcionar más contexto a los clientes.
- Códigos de Estado: Aunque GraphQL no utiliza códigos HTTP explícitos, se pueden emular con extensiones.