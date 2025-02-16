# Tutorial sobre Bases de Datos NoSQL y MongoDB

![MongoDB Logo](https://www.techcoil.com/blog/wp-content/uploads/mongoDB-logo.jpg)

Este repositorio contiene un tutorial sobre bases de datos NoSQL, con un enfoque específico en MongoDB. También incluye una guía de instalación para usar un clúster de MongoDB Atlas junto con el plugin de VSCode.

## ¿Qué son las Bases de Datos NoSQL?

Las bases de datos NoSQL (Not Only SQL) son un tipo de sistema de gestión de bases de datos que permiten el almacenamiento y recuperación de datos estructurados, semiestructurados y no estructurados. A diferencia de las bases de datos relacionales tradicionales, las bases de datos NoSQL no utilizan tablas con filas y columnas. En su lugar, emplean diferentes modelos de datos, como documentos, grafos, clave-valor, y columnas amplias.

### Ventajas de las Bases de Datos NoSQL

- **Escalabilidad Horizontal**: Permiten escalar fácilmente añadiendo más servidores.
- **Flexibilidad de Esquema**: No requieren un esquema fijo, lo que facilita la modificación de la estructura de los datos.
- **Alto Rendimiento**: Optimizadas para operaciones de lectura y escritura rápidas.
- **Gestión de Datos Diversos**: Adecuadas para manejar grandes volúmenes de datos variados.

## MongoDB

MongoDB es una base de datos NoSQL orientada a documentos, donde los datos se almacenan en documentos similares a JSON con esquemas dinámicos. Esto proporciona una gran flexibilidad y permite una integración rápida de datos.

### Componentes de MongoDB

- **Base de Datos**: Colección de datos relacionados.
- **Colección**: Grupo de documentos dentro de una base de datos.
- **Documento**: Unidad de datos en MongoDB, similar a un objeto JSON.
- **Campo**: Par clave-valor dentro de un documento.

![Estructura mongoDB](https://formadoresit.es/wp-content/uploads/2019/05/image-4.png)

![Comparativa SQL-NoSQL](https://github.com/user-attachments/assets/a029a1fb-1b88-4e69-82ee-441bde1d45ab)

## ¿Qué es BSON?

BSON (Binary JSON) es un formato binario para representar documentos estructurados. Fue diseñado para ser eficiente en el almacenamiento y la consulta de datos en MongoDB. BSON extiende la representación JSON para incluir tipos de datos que no están disponibles en JSON estándar, como tipos de datos binarios y fechas.

## Composición de un Documento BSON

Un documento BSON está compuesto por pares de clave-valor. Cada par de clave-valor se almacena en un formato binario que incluye el tipo de datos del valor, seguido por la clave y el valor mismo.

### Ejemplo de Documento BSON

```json
{
    "_id": {"$oid": "507f1f77bcf86cd799439011"},
    "nombre": "Carlos Alcaraz",
    "pais": "España",
    "ranking": 1,
    "titulos_grand_slam": 3,
    "entrenador": {
        "nombre": "Juan Carlos Ferrero",
        "pais": "España"
    },
    "nacimiento": {"$date": "2003-05-05T00:00:00Z"},
    "activo": true
}
```

### Partes del Documento BSON

- **_id**: Identificador único generado automáticamente por MongoDB.
- **nombre**: Campo de tipo cadena.
- **pais**: Campo de tipo cadena.
- **ranking**: Campo de tipo entero.
- **titulos_grand_slam**: Campo de tipo entero.
- **entrenador**: Subdocumento que contiene información sobre el entrenador.
- **nacimiento**: Campo de tipo fecha.
- **activo**: Campo de tipo booleano.

## Tipos de Datos en BSON

BSON soporta una variedad de tipos de datos, incluyendo:

- **Cadena (String)**: Una secuencia de caracteres UTF-8.
- **Entero (Integer)**: Números enteros de 32 o 64 bits.
- **Booleano (Boolean)**: Valores verdadero o falso.
- **Fecha (Date)**: Fechas almacenadas como milisegundos desde la época de Unix.
- **Nulo (Null)**: Representa un valor nulo.
- **Array (Array)**: Una lista ordenada de valores.
- **Documento (Document)**: Un objeto anidado.
- **Binario (Binary)**: Datos binarios.
- **ObjetoId (ObjectId)**: Identificador único generado por MongoDB.
- **Decimal128 (Decimal128)**: Números de punto flotante de alta precisión.
- **JavaScript (JavaScript)**: Código JavaScript.
- **Símbolo (Symbol)**: Similar a las cadenas pero utilizados para propósitos especiales.
- **Regular Expression (Regexp)**: Expresiones regulares.

### Ejemplo de Tipos de Datos

```json
{
    "cadena": "Ejemplo de cadena",
    "entero": 42,
    "booleano": true,
    "fecha": {"$date": "2025-02-16T17:28:48Z"},
    "nulo": null,
    "array": [1, 2, 3],
    "documento": {
        "clave": "valor"
    },
    "binario": {"$binary": "SGVsbG8gd29ybGQ=", "$type": "00"},
    "objectId": {"$oid": "507f1f77bcf86cd799439011"},
    "decimal128": {"$numberDecimal": "123.45"},
    "javascript": {"$code": "function() { return true; }"},
    "symbol": {"$symbol": "miSimbolo"},
    "regexp": {"$regularExpression": {"pattern": "^abc", "options": "i"}}
}
```

## Operadores en BSON

### Operadores de Comparación

- **$eq**: Igual a.
- **$ne**: No igual a.
- **$gt**: Mayor que.
- **$gte**: Mayor o igual que.
- **$lt**: Menor que.
- **$lte**: Menor o igual que.
- **$in**: Coincide con cualquier valor en la matriz.
- **$nin**: No coincide con ningún valor en la matriz.

### Ejemplo de Operadores de Comparación

```javascript
db.jugadores.find({ ranking: { $gt: 2 } })
```

### Operadores Lógicos

- **$and**: Junta cláusulas con una lógica AND.
- **$or**: Junta cláusulas con una lógica OR.
- **$not**: Invierte el efecto de un operador de consulta.
- **$nor**: Junta cláusulas con una lógica NOR.

### Ejemplo de Operadores Lógicos

```javascript
db.jugadores.find({ $or: [{ pais: "España" }, { pais: "Serbia" }] })
```

### Operadores de Elementos

- **$exists**: Coincide si un campo existe.
- **$type**: Coincide si el campo es de un tipo específico.

### Ejemplo de Operadores de Elementos

```javascript
db.jugadores.find({ entrenador: { $exists: true } })
```

### Operadores de Evaluación

- **$regex**: Coincide con expresión regular.
- **$mod**: Realiza una operación de módulo y compara el resultado.
- **$text**: Realiza una búsqueda de texto.
- **$where**: Consulta usando código JavaScript.

### Ejemplo de Operadores de Evaluación

```javascript
db.jugadores.find({ nombre: { $regex: "^Carlos" } })
```



## Instalación de MongoDB Atlas y Configuración en VSCode

Sigue estos pasos para configurar un clúster de MongoDB Atlas y conectarte a él desde VSCode.

### Paso 1: Crear una Cuenta en MongoDB Atlas

1. Ve a [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) y regístrate.
2. Crea un nuevo proyecto y un clúster.

### Paso 2: Configurar el Clúster

1. En la sección "Security", añade un nuevo usuario de base de datos con un nombre de usuario y contraseña.
2. En la sección "Network Access", añade tu dirección IP para permitir el acceso.

### Paso 3: Conectar al Clúster

1. En la sección "Clusters", haz clic en "Connect" y selecciona "Connect Your Application".
2. Copia la cadena de conexión proporcionada. Se verá algo así:
    ```
    mongodb+srv://<username>:<password>@cluster0.mongodb.net/myFirstDatabase?retryWrites=true&w=majority
    ```

### Paso 4: Configurar VSCode

1. Instala el plugin [MongoDB for VS Code](https://marketplace.visualstudio.com/items?itemName=mongodb.mongodb-vscode).
2. Abre VSCode y ve a la vista de MongoDB en la barra lateral izquierda.
3. Haz clic en "Add Connection" y pega la cadena de conexión copiada anteriormente.
4. Guarda la conexión y debería aparecer en la lista de conexiones.

## Crear una base de datos

Para crear una base de datos en MongoDB, simplemente cambiamos a la base de datos que deseamos crear con el comando `use`.

### Ejemplo:
```shell
use mi_base_de_datos
```

## Crear una colección

Para crear una colección en una base de datos, utilizamos el comando `createCollection()`.

### Ejemplo:
```shell
db.createCollection("mi_coleccion")
```

### Sintaxis:
```shell
db.createCollection("<nombre_coleccion>")
```

- `<nombre_coleccion>`: Nombre de la colección que se creará.

## Crear (Create)

Para insertar un documento en una colección utilizamos el comando `insertOne()` o `insertMany()`.

### Ejemplo con `insertOne()`:
```shell
db.mi_coleccion.insertOne({
    nombre: "Juan Pérez",
    edad: 30,
    ocupacion: "Desarrollador"
})
```

### Sintaxis:
```shell
db.<nombre_coleccion>.insertOne({<documento>})
```

- `<nombre_coleccion>`: Nombre de la colección donde se insertará el documento.
- `<documento>`: Documento BSON que se insertará.

### Ejemplo con `insertMany()`:
```shell
db.mi_coleccion.insertMany([
    {
        nombre: "Ana Gómez",
        edad: 25,
        ocupacion: "Diseñadora"
    },
    {
        nombre: "Luis Torres",
        edad: 35,
        ocupacion: "Gerente"
    }
])
```

### Sintaxis:
```shell
db.<nombre_coleccion>.insertMany([{<documento1>}, {<documento2>}, ...])
```

- `<nombre_coleccion>`: Nombre de la colección donde se insertarán los documentos.
- `<documento>`: Documentos BSON que se insertarán.

## Leer (Read)

Para leer documentos de una colección utilizamos el comando `find()`.

### Ejemplo para leer todos los documentos:
```shell
db.mi_coleccion.find()
```

### Ejemplo para leer documentos con un criterio:
```shell
db.mi_coleccion.find({ nombre: "Juan Pérez" })
```

### Sintaxis:
```shell
db.<nombre_coleccion>.find({<criterio>})
```

- `<nombre_coleccion>`: Nombre de la colección de la cual se leerán los documentos.
- `<criterio>`: Criterio de búsqueda para filtrar los documentos (puede estar vacío para leer todos los documentos).

### Operadores de búsqueda

#### Operador `$gt` (mayor que):
```shell
db.mi_coleccion.find({ edad: { $gt: 30 } })
```
Encuentra documentos donde la edad sea mayor que 30.

#### Operador `$lt` (menor que):
```shell
db.mi_coleccion.find({ edad: { $lt: 30 } })
```
Encuentra documentos donde la edad sea menor que 30.

#### Operador `$in` (dentro de un conjunto):
```shell
db.mi_coleccion.find({ nombre: { $in: ["Juan Pérez", "Ana Gómez"] } })
```
Encuentra documentos donde el nombre esté dentro del conjunto especificado.

#### Operador `$or` (o):
```shell
db.mi_coleccion.find({ $or: [{ nombre: "Juan Pérez" }, { edad: { $lt: 30 } }] })
```
Encuentra documentos que cumplan al menos una de las condiciones especificadas.

## Actualizar (Update)

Para actualizar documentos en una colección utilizamos el comando `updateOne()`, `updateMany()` o `replaceOne()`.

### Ejemplo con `updateOne()`:
```shell
db.mi_coleccion.updateOne(
    { nombre: "Juan Pérez" },
    { $set: { edad: 31 } }
)
```

### Sintaxis:
```shell
db.<nombre_coleccion>.updateOne({<criterio>}, {<actualizacion>})
```

- `<nombre_coleccion>`: Nombre de la colección donde se actualizarán los documentos.
- `<criterio>`: Criterio de búsqueda para seleccionar los documentos a actualizar.
- `<actualizacion>`: Documento que define los cambios a realizar. Utiliza operadores como `$set`, `$inc`, etc.

### Ejemplo con `updateMany()`:
```shell
db.mi_coleccion.updateMany(
    { ocupacion: "Desarrollador" },
    { $set: { ocupacion: "Ingeniero de Software" } }
)
```

### Sintaxis:
```shell
db.<nombre_coleccion>.updateMany({<criterio>}, {<actualizacion>})
```

- `<nombre_coleccion>`: Nombre de la colección donde se actualizarán los documentos.
- `<criterio>`: Criterio de búsqueda para seleccionar los documentos a actualizar.
- `<actualizacion>`: Documento que define los cambios a realizar.

### Ejemplo con `replaceOne()`:
```shell
db.mi_coleccion.replaceOne(
    { nombre: "Luis Torres" },
    {
        nombre: "Luis Torres",
        edad: 36,
        ocupacion: "Director"
    }
)
```

### Sintaxis:
```shell
db.<nombre_coleccion>.replaceOne({<criterio>}, {<nuevo_documento>})
```

- `<nombre_coleccion>`: Nombre de la colección donde se reemplazará el documento.
- `<criterio>`: Criterio de búsqueda para seleccionar el documento a reemplazar.
- `<nuevo_documento>`: Nuevo documento que reemplazará el documento existente.

### Operadores de actualización

#### Operador `$set` (establecer un valor):
```shell
db.mi_coleccion.updateOne(
    { nombre: "Juan Pérez" },
    { $set: { edad: 31 } }
)
```
Establece el valor del campo `edad` a 31 en el documento que cumple el criterio.

#### Operador `$inc` (incrementar):
```shell
db.mi_coleccion.updateOne(
    { nombre: "Juan Pérez" },
    { $inc: { edad: 1 } }
)
```
Incrementa el valor del campo `edad` en 1 en el documento que cumple el criterio.

#### Operador `$unset` (eliminar un campo):
```shell
db.mi_coleccion.updateOne(
    { nombre: "Juan Pérez" },
    { $unset: { ocupacion: "" } }
)
```
Elimina el campo `ocupacion` del documento que cumple el criterio.

## Eliminar (Delete)

Para eliminar documentos de una colección utilizamos el comando `deleteOne()` o `deleteMany()`.

### Ejemplo con `deleteOne()`:
```shell
db.mi_coleccion.deleteOne({ nombre: "Juan Pérez" })
```

### Sintaxis:
```shell
db.<nombre_coleccion>.deleteOne({<criterio>})
```

- `<nombre_coleccion>`: Nombre de la colección de la cual se eliminarán los documentos.
- `<criterio>`: Criterio de búsqueda para seleccionar los documentos a eliminar.

### Ejemplo con `deleteMany()`:
```shell
db.mi_coleccion.deleteMany({ ocupacion: "Diseñadora" })
```

### Sintaxis:
```shell
db.<nombre_coleccion>.deleteMany({<criterio>})
```

- `<nombre_coleccion>`: Nombre de la colección de la cual se eliminarán los documentos.
- `<criterio>`: Criterio de búsqueda para seleccionar los documentos a eliminar.

## Usando MongoDB Playground en VSCode

MongoDB Playground es una característica de MongoDB para escribir, ejecutar y depurar operaciones en MongoDB directamente desde Visual Studio Code.

### Crear una base de datos y una colección

1. Abre Visual Studio Code.
2. Instala la extensión de MongoDB.
3. Crea un nuevo archivo de Playground (`.mongodb`).
4. Escribe el siguiente código en el archivo de Playground:

```javascript
// Crear una base de datos
use('mi_base_de_datos');

// Crear una colección
db.createCollection('mi_coleccion');

// Insertar documentos
db.mi_coleccion.insertMany([
    {
        nombre: "Ana Gómez",
        edad: 25,
        ocupacion: "Diseñadora"
    },
    {
        nombre: "Luis Torres",
        edad: 35,
        ocupacion: "Gerente"
    }
]);

// Leer documentos
db.mi_coleccion.find();

// Actualizar documentos
db.mi_coleccion.updateOne(
    { nombre: "Luis Torres" },
    { $set: { edad: 36 } }
);

// Eliminar documentos
db.mi_coleccion.deleteOne({ nombre: "Ana Gómez" });
```

5. Ejecuta el Playground presionando `Ctrl+Shift+P` y seleccionando `MongoDB: Run Selected Playground`.

