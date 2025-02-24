# Agrupaciones en MongoDB

Las agrupaciones en MongoDB se realizan utilizando el framework de agregación. Este framework proporciona una forma de procesar datos de documentos y devolver resultados computados. Utiliza un pipeline de etapas, donde cada etapa transforma los documentos de entrada y pasa los resultados a la siguiente etapa.

### Sintaxis Básica

La sintaxis básica para una operación de agregación en MongoDB es:

```javascript
db.coleccion.aggregate([
  { $etapa1: { ... } },
  { $etapa2: { ... } },
  ...
]);
```

Cada etapa en el pipeline es un documento que especifica la operación de agregación que se realizará.

## Etapas Comunes en el Pipeline

### $match

La etapa `$match` se utiliza para filtrar los documentos que pasan a la siguiente etapa según un criterio específico.

### $group

La etapa `$group` se utiliza para agrupar documentos por un campo específico y realizar operaciones de agregación, como sumar, promediar, contar, etc.

### $project

La etapa `$project` se utiliza para incluir, excluir o agregar campos a los documentos de salida. Permite transformar y remodelar los documentos.

### $sort

La etapa `$sort` se utiliza para ordenar los documentos de salida según un campo específico.

### $limit

La etapa `$limit` se utiliza para limitar el número de documentos en la salida.

### $skip

La etapa `$skip` se utiliza para omitir un número específico de documentos en la salida.

## Operadores de Agregación Básicos

### $sum

El operador `$sum` se utiliza para sumar valores. Puede sumar valores numéricos de documentos o contar el número de documentos si se usa con el valor `1`.

### $avg

El operador `$avg` se utiliza para calcular el promedio de valores numéricos.

### $multiply

El operador `$multiply$` se utiliza para multiplicar valores numéricos.

### Ejemplos de Uso de Operadores

- **$sum**: Sumar el total de ventas.
- **$avg**: Calcular el precio promedio de los artículos.
- **$multiply**: Calcular el total de ventas multiplicando el precio por la cantidad.

## Ejemplos Prácticos

### Datos de Ejemplo

Usaremos la siguiente colección de datos de ventas para nuestros ejemplos:

```json
[
  { "item": "camiseta", "precio": 10, "cantidad": 5, "categoria": "ropa" },
  { "item": "pantalones", "precio": 20, "cantidad": 10, "categoria": "ropa" },
  { "item": "calcetines", "precio": 5, "cantidad": 20, "categoria": "ropa" },
  { "item": "zapatos", "precio": 50, "cantidad": 2, "categoria": "calzado" },
  { "item": "sombrero", "precio": 15, "cantidad": 1, "categoria": "accesorios" }
]
```

### 1. Agrupar por Categoría y Calcular el Total de Ventas

Para agrupar los artículos por categoría y calcular el total de ventas (precio * cantidad) para cada categoría, utilizamos la siguiente consulta:

```javascript
db.ventas.aggregate([
  {
    $group: {
      _id: "$categoria",
      totalVentas: { $sum: { $multiply: ["$precio", "$cantidad"] } }
    }
  }
]);
```

Resultado:
```json
[
  { "_id": "ropa", "totalVentas": 300 },
  { "_id": "calzado", "totalVentas": 100 },
  { "_id": "accesorios", "totalVentas": 15 }
]
```

### 2. Calcular el Precio Promedio de los Artículos por Categoría

Para calcular el precio promedio de los artículos en cada categoría, utilizamos la siguiente consulta:

```javascript
db.ventas.aggregate([
  {
    $group: {
      _id: "$categoria",
      precioPromedio: { $avg: "$precio" }
    }
  }
]);
```

Resultado:
```json
[
  { "_id": "ropa", "precioPromedio": 11.666666666666666 },
  { "_id": "calzado", "precioPromedio": 50 },
  { "_id": "accesorios", "precioPromedio": 15 }
]
```

### 3. Contar el Número de Artículos en Cada Categoría

Para contar el número de artículos en cada categoría, utilizamos la siguiente consulta:

```javascript
db.ventas.aggregate([
  {
    $group: {
      _id: "$categoria",
      totalArticulos: { $sum: 1 }
    }
  }
]);
```

Resultado:
```json
[
  { "_id": "ropa", "totalArticulos": 3 },
  { "_id": "calzado", "totalArticulos": 1 },
  { "_id": "accesorios", "totalArticulos": 1 }
]
```

### 4. Filtrar y Agrupar: Obtener Categorías con Total de Ventas Mayor a 50

Para obtener categorías con un total de ventas mayor a 50, utilizamos la siguiente consulta:

```javascript
db.ventas.aggregate([
  {
    $group: {
      _id: "$categoria",
      totalVentas: { $sum: { $multiply: ["$precio", "$cantidad"] } }
    }
  },
  {
    $match: {
      totalVentas: { $gt: 50 }
    }
  }
]);
```

Resultado:
```json
[
  { "_id": "ropa", "totalVentas": 300 },
  { "_id": "calzado", "totalVentas": 100 }
]
```

### 5. Ejemplo Completo: Agrupar, Proyectar y Ordenar

Para obtener categorías con un total de ventas mayor a 50, proyectar solo el nombre de la categoría y el total de ventas con un cálculo adicional del IVA (impuesto al valor agregado) y ordenar los resultados por total de ventas en orden descendente, utilizamos la siguiente consulta:

```javascript
db.ventas.aggregate([
  {
    $group: {
      _id: "$categoria",
      totalVentas: { $sum: { $multiply: ["$precio", "$cantidad"] } }
    }
  },
  {
    $match: {
      totalVentas: { $gt: 50 }
    }
  },
  {
    $project: {
      _id: 0,
      categoria: "$_id",
      totalVentas: 1,
      totalVentasConIVA: { $multiply: ["$totalVentas", 1.21] } // Añadir un 21% de IVA
    }
  },
  {
    $sort: {
      totalVentas: -1
    }
  }
]);
```

Resultado:
```json
[
  { "categoria": "ropa", "totalVentas": 300, "totalVentasConIVA": 363 },
  { "categoria": "calzado", "totalVentas": 100, "totalVentasConIVA": 121 }
]
```

## Conclusión

Esta documentación explica cómo realizar agrupaciones en MongoDB utilizando el framework de agregación. Las consultas de ejemplo demuestran cómo agrupar documentos, calcular el total de ventas, el precio promedio, contar artículos, filtrar resultados, proyectar campos, ordenar, limitar y omitir resultados según criterios específicos. Al igual que Rafa Nadal y Roger Federer en el tenis, dominar las agrupaciones en MongoDB requiere práctica y precisión.
