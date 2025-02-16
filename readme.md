# Tutorial sobre Bases de Datos NoSQL y MongoDB

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
