# Documentos Embebidos en MongoDB

Los documentos embebidos en MongoDB son una forma de estructurar datos en los que se almacenan documentos dentro de otros documentos. Esta técnica permite agrupar datos relacionados en una sola estructura, lo que facilita el acceso y la manipulación de la información.

### Ejemplo de Documento Embebido

En el siguiente ejemplo, cada profesor tiene una asignatura embebida dentro de su documento:

```json
{
  "nombre": "José Luis",
  "apellidos": "Suárez Manrique",
  "especialidad": "Biología",
  "esTitular": true,
  "esAsociado": false,
  "edad": 51,
  "asignatura": {
    "id": "A0001",
    "nombre": "Biología molecular",
    "creditos": 6
  }
}
```

## Ejercicios

### Datos de Ejemplo

```json
[
  {
    "nombre": "José Luis",
    "apellidos": "Suárez Manrique",
    "especialidad": "Biología",
    "esTitular": true,
    "esAsociado": false,
    "edad": 51,
    "asignatura": {
      "id": "A0001",
      "nombre": "Biología molecular",
      "creditos": 6
    }
  },
  {
    "nombre": "Antonio",
    "apellidos": "López Pérez",
    "especialidad": ["Matemáticas", "Física"],
    "esTitular": false,
    "esAsociado": true,
    "edad": 39,
    "asignatura": {
      "id": "A0002",
      "nombre": "Termodinámica",
      "creditos": 9
    }
  },
  {
    "nombre": "María",
    "apellidos": "Munguía Arteche",
    "especialidad": ["Física", "Química"],
    "esTitular": true,
    "esAsociado": false,
    "edad": 55,
    "asignatura": {
      "id": "A0002",
      "nombre": "Termodinámica",
      "creditos": 9
    }
  }
]
```

### 1. Obtener todos los profesores que tienen la asignatura con el id `A0002`

Para obtener todos los profesores que tienen la asignatura con el id `A0002`, podemos utilizar la siguiente consulta en MongoDB:

```javascript
db.profesores.find({ "asignatura.id": "A0002" });
```

Respuesta:
```json
[
  {
    "nombre": "Antonio",
    "apellidos": "López Pérez",
    "especialidad": ["Matemáticas", "Física"],
    "esTitular": false,
    "esAsociado": true,
    "edad": 39,
    "asignatura": {
      "id": "A0002",
      "nombre": "Termodinámica",
      "creditos": 9
    }
  },
  {
    "nombre": "María",
    "apellidos": "Munguía Arteche",
    "especialidad": ["Física", "Química"],
    "esTitular": true,
    "esAsociado": false,
    "edad": 55,
    "asignatura": {
      "id": "A0002",
      "nombre": "Termodinámica",
      "creditos": 9
    }
  }
]
```

Explicación:
La consulta `find` se usa para buscar documentos en una colección que coincidan con un criterio específico. Aquí, estamos buscando profesores cuya asignatura tenga el id `A0002`.

### 2. Obtener todos los profesores que imparten la asignatura "Termodinámica"

Para obtener todos los profesores que imparten la asignatura "Termodinámica", utilizamos la siguiente consulta en MongoDB:

```javascript
db.profesores.find({ "asignatura.nombre": "Termodinámica" });
```

Respuesta:
```json
[
  {
    "nombre": "Antonio",
    "apellidos": "López Pérez",
    "especialidad": ["Matemáticas", "Física"],
    "esTitular": false,
    "esAsociado": true,
    "edad": 39,
    "asignatura": {
      "id": "A0002",
      "nombre": "Termodinámica",
      "creditos": 9
    }
  },
  {
    "nombre": "María",
    "apellidos": "Munguía Arteche",
    "especialidad": ["Física", "Química"],
    "esTitular": true,
    "esAsociado": false,
    "edad": 55,
    "asignatura": {
      "id": "A0002",
      "nombre": "Termodinámica",
      "creditos": 9
    }
  }
]
```

Explicación:
Esta consulta es similar a la anterior, pero en lugar de buscar por el id de la asignatura, buscamos por el nombre de la asignatura. Estamos buscando profesores cuya asignatura tenga el nombre `Termodinámica`.

### 3. Obtener todos los profesores que tienen asignaturas con más de 6 créditos

Para obtener todos los profesores que tienen asignaturas con más de 6 créditos, utilizamos la siguiente consulta en MongoDB:

```javascript
db.profesores.find({ "asignatura.creditos": { $gt: 6 } });
```

Respuesta:
```json
[
  {
    "nombre": "Antonio",
    "apellidos": "López Pérez",
    "especialidad": ["Matemáticas", "Física"],
    "esTitular": false,
    "esAsociado": true,
    "edad": 39,
    "asignatura": {
      "id": "A0002",
      "nombre": "Termodinámica",
      "creditos": 9
    }
  },
  {
    "nombre": "María",
    "apellidos": "Munguía Arteche",
    "especialidad": ["Física", "Química"],
    "esTitular": true,
    "esAsociado": false,
    "edad": 55,
    "asignatura": {
      "id": "A0002",
      "nombre": "Termodinámica",
      "creditos": 9
    }
  }
]
```

Explicación:
En esta consulta, utilizamos el operador `$gt` (mayor que) para encontrar profesores cuyas asignaturas tengan más de 6 créditos.

### 4. Obtener todos los profesores que tienen asignaturas con más de 6 créditos y son mayores de 40 años

Para obtener todos los profesores que tienen asignaturas con más de 6 créditos y son mayores de 40 años, utilizamos la siguiente consulta en MongoDB:

```javascript
db.profesores.find({ "asignatura.creditos": { $gt: 6 }, "edad": { $gt: 40 } });
```

Respuesta:
```json
[
  {
    "nombre": "María",
    "apellidos": "Munguía Arteche",
    "especialidad": ["Física", "Química"],
    "esTitular": true,
    "esAsociado": false,
    "edad": 55,
    "asignatura": {
      "id": "A0002",
      "nombre": "Termodinámica",
      "creditos": 9
    }
  }
]
```

Explicación:
En esta consulta, combinamos dos criterios utilizando una coma (que actúa como un `AND` en MongoDB). Buscamos profesores cuyas asignaturas tengan más de 6 créditos y cuya edad sea mayor que 40 años.

## Conclusión

Esta documentación explica cómo realizar consultas sobre un conjunto de datos de profesores y sus asignaturas utilizando MongoDB. Las consultas específicas permiten filtrar los datos según criterios como el id de la asignatura, el nombre de la asignatura, el número de créditos y la edad del profesor.