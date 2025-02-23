# Consultas de Arrays en MongoDB

Esta guía proporciona ejemplos de consultas para buscar en arrays dentro de documentos en MongoDB. Se mostrarán cómo obtener profesores que imparten ciertas materias y cómo contar el número de profesores para una materia específica.

## Introducción

MongoDB es una base de datos NoSQL orientada a documentos que utiliza JSON (BSON) como formato de almacenamiento de datos. Una de las características poderosas de MongoDB es su capacidad para manejar arrays y documentos anidados, lo que permite modelar datos complejos de manera eficiente. Las consultas en arrays son una característica esencial que permite buscar documentos basados en los elementos dentro de un array.

## Comandos Principales

Para trabajar con arrays en MongoDB, es importante conocer algunos de los operadores y comandos principales que se utilizan en las consultas:

- `$all`: Selecciona los documentos donde el valor de un campo (array) contiene todos los elementos especificados.
- `$elemMatch`: Selecciona los documentos si al menos un elemento del array cumple con los criterios especificados.
- `$size`: Selecciona los documentos donde el array tiene un tamaño específico.
- `$in`: Selecciona los documentos donde el valor de un campo está en el array especificado.

## Colección de Profesores

La colección de `profesores` contiene documentos con información sobre los profesores y las materias que imparten. A continuación se muestra un ejemplo de la estructura de esta colección:

```json
[
    {
        "_id": 1,
        "nombre": "Juan Pérez",
        "materias": ["Matemáticas", "Física"]
    },
    {
        "_id": 2,
        "nombre": "María García",
        "materias": ["Química", "Biología"]
    },
    {
        "_id": 3,
        "nombre": "Carlos Sánchez",
        "materias": ["Matemáticas", "Química"]
    },
    {
        "_id": 4,
        "nombre": "Lucía Fernández",
        "materias": ["Física"]
    },
    {
        "_id": 5,
        "nombre": "Ana Martínez",
        "materias": ["Biología"]
    },
    {
        "_id": 6,
        "nombre": "Pedro López",
        "materias": ["Matemáticas", "Física", "Química"],
        "detallesMaterias": [
            { "nombre": "Matemáticas", "nivel": "Avanzado" },
            { "nombre": "Física", "nivel": "Intermedio" },
            { "nombre": "Química", "nivel": "Básico" }
        ]
    }
]
```

## Ejercicios

### Obtener todos los profesores que imparten exactamente Matemáticas y Física

Para obtener todos los profesores que imparten exactamente Matemáticas y Física, se puede utilizar una consulta que verifique que el array contenga exactamente esos dos elementos:

```javascript
db.profesores.find({
    materias: ["Matemáticas", "Física"]
});
```

### Obtener todos los profesores que imparten Matemáticas y Física

Para obtener todos los profesores que imparten tanto Matemáticas como Física, se puede utilizar el operador `$all`:

```javascript
db.profesores.find({
    materias: { $all: ["Matemáticas", "Física"] }
});
```

### Obtener todos los profesores que imparten Química

Para obtener todos los profesores que imparten Química, se puede utilizar una consulta simple:

```javascript
db.profesores.find({
    materias: "Química"
});
```

### Número total de profesores que imparten Biología

Para contar el número total de profesores que imparten Biología, se puede utilizar el método `countDocuments`:

```javascript
db.profesores.countDocuments({
    materias: "Biología"
});
```

### Obtener solo 1 profesor que imparta Física

Para obtener solo un profesor que imparta Física, se puede utilizar el método `findOne`:

```javascript
db.profesores.findOne({
    materias: "Física"
});
```

También se puede utilizar el método `find` con `limit` para obtener solo un profesor que imparta Física:

```javascript
db.profesores.find({
    materias: "Física"
}).limit(1);
```

### Uso de `$elemMatch`

Para obtener todos los profesores que imparten una materia que tiene un campo específico (por ejemplo, un array de objetos con detalles de la materia), se puede utilizar `$elemMatch`:

```javascript
db.profesores.find({
    detallesMaterias: { 
        $elemMatch: { 
            nombre: "Matemáticas", 
            nivel: "Avanzado" 
        } 
    }
});
```

### Uso de `$size`

Para obtener todos los profesores que imparten exactamente dos materias, se puede utilizar `$size`:

```javascript
db.profesores.find({
    materias: { $size: 2 }
});
```

### Uso de `$in` para buscar dos materias

Para obtener todos los profesores que imparten cualquier dos materias de un conjunto de materias especificadas (por ejemplo, Matemáticas o Física), se puede utilizar `$in`:

```javascript
db.profesores.find({
    materias: { $in: ["Matemáticas", "Física"] }
});
```

## Conclusión

Las consultas en arrays en MongoDB permiten realizar búsquedas complejas y específicas dentro de documentos. Esta guía proporciona ejemplos básicos pero esenciales para trabajar con arrays en MongoDB y obtener información relevante sobre los profesores y las materias que imparten.