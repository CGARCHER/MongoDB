# Ejercicio "Tienda de Ropa"

## Enunciado

Vamos a crear una base de datos llamada "tienda". La base de datos tendrá una colección llamada "productos".

## Ejercicio

1. Crear la base de datos "tienda" y la colección "productos"

2. Insertar documentos en la colección "productos" (uno a uno):

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

3. Eliminar todos los documentos de la colección "productos".

4. Volver a crear los mismos documentos, insertándolos todos a la vez.

5. Actualizar todos los documentos con un precio inferior a 25 para que tengan un precio un 10% más caro.

6. Reemplazar cada documento que sea para hombre con la misma estructura, pero añadiendo una propiedad nueva: "paraMujer": false.

7. Reemplazar cada documento que sea para mujer con la misma estructura, pero añadiendo una propiedad nueva: "paraHombre": false.

8. Actualizar cada documento, filtrando por su referencia. Las propiedades "tipo" deben cambiar de "camisa" a "chaqueta" y la "talla" debe ser igual a "M".
