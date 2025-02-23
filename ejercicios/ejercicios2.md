# Ejercicio 1: Agrupación básica

Crea una base de datos llamada youtube.

Crea una colección llamada youtubers.

Inserta los siguientes documentos de ejemplo:

```json
db.youtubers.insertMany([
  { "nombre": "AuronPlay", "pais": "España", "suscriptores": 29000000, "videos": 1100 },
  { "nombre": "Yuya", "pais": "México", "suscriptores": 25000000, "videos": 700 },
  { "nombre": "ElRubiusOMG", "pais": "España", "suscriptores": 40000000, "videos": 900 },
  { "nombre": "Luisito Comunica", "pais": "México", "suscriptores": 38000000, "videos": 500 },
  { "nombre": "HolaSoyGerman", "pais": "Chile", "suscriptores": 42000000, "videos": 140 }
]);
```

Calcula el total de videos por país.

# Ejercicio 2: Filtrar y agrupar

Calcula el promedio de suscriptores por país para youtubers con más de 1000 suscriptores.

# Ejercicio 3: Ordenar resultados

Calcula el total de suscriptores por país y ordénalos de mayor a menor.

# Ejercicio 4: Calcular ingresos estimados

Asumiendo que cada suscriptor genera 0.01 por video, calcula los ingresos estimados por país.

# Ejercicio 5: Filtrar, agrupar y proyectar

Calcula el promedio de videos por país para youtubers con más de 50 videos.

# Ejercicio 6: Calcular métricas combinadas

Calcula el total de suscriptores y videos por país y ordénalos por el total de suscriptores de mayor a menor.

# Ejercicio 7: Proyectar y calcular ingresos individuales

Calcula los ingresos para cada youtuber (suscriptores * videos * 0.01) y encuentra aquellos con ingresos mayores a $500.

# Ejercicio 8: Agregación compleja

Para youtubers con más de 1000 suscriptores, calcula el total de suscriptores y el promedio de videos por país, además del youtuber con más suscriptores en cada país. Ordena los resultados por el total de suscriptores de mayor a menor.