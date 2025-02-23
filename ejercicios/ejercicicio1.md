## Ejercicios CRUD

### Ejercicio 1
Crear la base de datos "tienda" y la colección "productos".

### Ejercicio 2
Insertar documentos en la colección "productos" (uno a uno):

```json
{
  "referencia": "P0001",
  "tipo": "camisa",
  "paraHombre": true,
  "talla": "XS",
  "precio": 20.99
}
```

```json
{
  "referencia": "P0002",
  "tipo": "camisa",
  "paraHombre": true,
  "talla": "XL",
  "precio": 30.25
}
```

```json
{
  "referencia": "P0003",
  "tipo": "pantalon",
  "paraMujer": true,
  "talla": "L",
  "precio": 28.99
}
```

### Ejercicio 3
Eliminar todos los documentos de la colección "productos".

### Ejercicio 4
Volver a crear los mismos documentos, insertándolos todos a la vez.

### Ejercicio 5
Actualizar todos los documentos con un precio inferior a 25 para que tengan un precio un 10% más caro.

### Ejercicio 6
Buscar todos los documentos que sean para hombre y agregar una propiedad nueva "enStock: true".

### Ejercicio 7
Eliminar un documento específico por referencia "P0002".

### Ejercicio 8
Actualizar cada documento. Las propiedades "tipo" deben cambiar de "camisa" a "chaqueta" y la "talla" debe ser igual a "M".