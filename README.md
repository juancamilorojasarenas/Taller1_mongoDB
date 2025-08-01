NOMBRES DE LOS INTEGRANTES: CONNIE TATIANA CARRILLO BOHORQUEZ,KEVIN SANTIAGO RIVERO RUEDA, JUAN CAMILO ROJAS ARENAS.
# Taller1_mongoDB
INVESTIGACIÓN QUE SE LLEVO A CABO EN BASE A LAS PREGUNTAS MENCIONADAS.

# 1. ¿Qué es una base de datos NoSQL?

- La base de datos NoSQL nos ofrece una perspectiva diferente a la relacional ya que esta diseñada para grandes volumenes de datos,en esta no se utliza tablas,y además nos permite realizar un tipo de escalado horizontal,para asi poder tener mayor flexibilidad y rendimiento,y por ultimo y no menos importante también se maneja el modelo clave valor,donde a través de la clave recuperamos el valor o dato.

## ¿Qué es MongoDB?
- MongoDB es un una base de datos NoSQL que sus datos se almacenan en JSON haciendo que sea muchisimo mas acessible y comprensible para apps modernas o servicios multiplataformas,lo que quiere decir que a nosotros como desarrolladores se nos facilita y agiliza el trabajo,por su manera de ser tipo documental y inspirada en el modelo clave/valor,creando asi un esquemas más libre y con código abierto.

## ¿Qué diferencia hay entre una base de datos relacional (como MySQL) y una base de datos documental como MongoDB?
- Básicamente se diferencian en muchos aspectos entre esos por ejemplo su estructura primordialmente en MYSQL utlizamos tablas,filas y columnas mientras que en Mongo DB utilzamos únicamente documentos Json en colecciones,otro aspecto a considerar es el hecho de que en MySQL se utiliza un escalamiento vertical por otro lado en MongoDB se utliza horizontal igualmente en Mongo DB como ya lo mencione hay mayor flexibilidad y no tanta rigidez en comparación a MYSQL.

## ¿Qué son documentos y colecciones en MongoDB?
- Los documentos para simplificarlos guardan la información completa  sobre una entidad ya sea un cliente,pedido,pizza,etc. y la colección son como tablas pero para documento allí puedo agrupar documentos similares.

# 2.DISEÑO DE LA PROPUESTA

## Colecciones que tendrían:

- Pedido
- Producto
- Usuario
- Inventario
- Ingredientes
- Combos
- Tipo_producto

## ¿Qué información tendría un documento de pedido? ¿Y un producto?

### La informacion que tendria un documento de pedido, seria:

- ID del pedido
- ID del usuario (referencia al documento del cliente)
- Lista de productos (con información de personalización si aplica)
- Tipo de pedido (para recoger o en el lugar)
- Es_domicilio (booleano que indica si es a domicilio)
- Fecha y hora del pedido
- Estado del pedido (preparando, listo, entregado, cancelado, etc.)
- Total del pedido
- Método de pago

### La informacion que tendria un documento de producto, seria:

- ID del producto
- Nombre del producto
- Lista de ingredientes (cada uno con nombre y cantidad)
- Descripción del producto
- ID del tipo de producto (referencia a la colección "Tipo_producto")
- Precio base del producto
- Tamaños disponibles (si aplica, como personal, mediana, familiar)
- Personalizable (booleano que indica si acepta adiciones)

## ¿Qué iría dentro del documento y qué se referenciaría?

- Los ingredientes básicos del producto irían dentro del documento de producto como una lista.
- El tipo de producto (pizza, bebida, postre, etc.) se referenciaría desde la colección "Tipo_producto".
- Los productos dentro de un pedido irían incrustados como una lista de objetos que incluyen el ID del producto, cantidad, tamaño (si aplica) y adiciones personalizadas.
- El cliente se referenciaría mediante su ID (como si fuera una llave foránea).
- En la colección "Combos", se referenciarían los productos que forman parte del combo por su ID, pero también se podría incluir la cantidad de cada uno dentro del mismo documento.
- Las adiciones (extras como tocineta, queso extra, etc.) se incluirían dentro del producto del pedido, ya que son específicas de cada pedido.

## ¿Qué campos serían listas, objetos u otros documentos incrustados?

- Los ingredientes serían una lista de objetos dentro del documento de producto.
- La lista de productos dentro del pedido sería una lista de objetos, incluyendo sus personalizaciones.
- Las adiciones en un pedido serían una lista de objetos dentro del producto del pedido.
- Los productos en un combo serían una lista que contiene objetos con ID y cantidad.
- En el documento del usuario, podrían incluirse como lista algunos campos como direcciones frecuentes o historial de pedidos (en caso de querer consultar los últimos pedidos sin necesidad de otra búsqueda).
- El campo de tamaños disponibles en los productos sería una lista de valores (por ejemplo: personal, mediana, familiar).
- Los campos como estado del pedido y método de pago serían valores simples (texto o booleanos).

# 3.

## Crear ejemplos de documentos JSON

<img width="318" height="423" alt="image" src="https://github.com/user-attachments/assets/b4b14a52-de0a-439b-8dd9-a6038797780a" />

<img width="318" height="423" alt="image" src="https://github.com/user-attachments/assets/3ac22715-6b12-472f-85ce-c7cb1a7cb859" />

<img width="397" height="527" alt="image" src="https://github.com/user-attachments/assets/1f558cb1-4f09-4986-a207-f8857292db89" />


# 4.

### Reflexión grupal

- Lo más difícil:

El mayor reto fue imaginar cómo estructurar la información sin apoyarnos en las tradicionales claves foráneas ni en la separación por tablas. En bases de datos relacionales, estamos acostumbrados a dividir todo en entidades específicas y luego conectarlas con relaciones. Sin embargo, en una base de datos orientada a documentos como MongoDB, esa lógica cambia completamente: ahora los datos relacionados se anidan o duplican, lo que al principio resulta confuso y requiere un cambio de mentalidad.

- Lo mejor del enfoque con documentos:

Lo que más nos gustó fue la simplicidad con la que se puede acceder a toda la información relacionada con un pedido en un solo documento. Por ejemplo, no hay que hacer múltiples consultas ni unir tablas para saber qué pidió el cliente, cuándo, con qué adiciones y cuánto costó. Todo está encapsulado en un mismo bloque, lo que facilita tanto el desarrollo como la lectura de los datos.

- Dudas que surgieron:

Nos surgieron varias preguntas al pensar en cómo mantener la consistencia de los datos. Una de las principales fue sobre cómo manejar los clientes que hacen muchos pedidos: ¿es correcto repetir su información en cada documento? ¿No genera eso redundancia y posibles errores si cambia su número o nombre? También nos preguntamos cómo actualizar datos repetidos en varios documentos sin tener relaciones directas. Estos aspectos nos dejaron claro que, aunque es un enfoque muy práctico, también exige criterios distintos para organizar y mantener los datos correctamente.
