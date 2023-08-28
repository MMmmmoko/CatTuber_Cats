# ¿Qué es un "estándar de modelos"?
CatTuber tiene como objetivo lograr que los modelos de personajes, mesas y mouses sean independientes hasta cierto punto. Por ejemplo, si se crea un modelo de personaje según ciertas reglas, este personaje puede usarse directamente con otros modelos de mesas y mouses que sigan las mismas reglas. De esta manera, el modelo de personaje que hayas creado puede usarse directamente con mesas creadas por otras personas, o modelos de personajes diferentes pueden usar el modelo de mesa personalizado que hayas creado. Las "reglas" usadas para crear estos modelos se denominan **estándar de modelos**.

No existe un único **estándar de modelos** los usuarios pueden establecer sus propios estándares según sus necesidades, pero los modelos creados según estándares diferentes no pueden combinarse.

En la versión actual, los diferentes modelos bajo el mismo estándar deben cumplir con lo siguiente (para facilitar la lectura y comprensión, se usan nombres de parámetros en lugar de IDs de parámetros, consulta la documentación específica de creación de modelos para los IDs de parámetros):
1. El lienzo del modelo debe ser consistente o estar en una relación de múltiplos (para facilitar la colocación durante la modelación).
2. En cualquier parámetro de "ManoX" y "ManoY", las posiciones de las manos en diferentes modelos de personajes deben coincidir.
3. La forma de la máscara utilizada en el modelo de personaje para representar que el cuerpo está oculto por la mesa debe coincidir con la forma del modelo de mesa bajo el mismo estándar.
4. Para los parámetros de "PosiciónX" y "PosiciónY" de los modelos de objetos sostenidos en la mano (como ratones o bolígrafos), deben coincidir con los valores equivalentes de "ManoX" y "ManoY", respectivamente. Por ejemplo, si el valor de los parámetros XY de un modelo de ratón es [-30,30], el modelo debería representar que la **mano** sostiene el ratón cuando los parámetros XY de la **mano** son [-30,30].
5. Se deben seguir ciertas reglas de orden de dibujo. [Reglas de orden de capas usadas en los modelos oficiales de CatTuber.](Reglas%20de%20orden%20de%20capas%20en%20modelos%20oficiales%20de%20CatTuber)

Cuando una serie de modelos se crea siguiendo los requisitos anteriores, los modelos dentro de esa serie pueden ser intercambiables o compatibles entre sí. Si sigues el **estándar de modelos** oficial al crear tus propios modelos, tus modelos de personajes o mesas podrán utilizarse directamente con una variedad de modelos de mesas o personajes creados por otros siguiendo el estándar oficial.

### Establecer un nuevo estándar de modelos
A muchas personas les gustan las mesas poco inclinadas, y otras prefieren una vista completamente horizontal. ¡Establecer tu propio **estándar de modelos** según tus necesidades es perfectamente posible!

Solo necesitas crear modelos generales siguiendo los requisitos de parámetros proporcionados en los tutoriales y luego dividir el modelo en tres partes: personaje, objeto sostenido en la mano y mesa. Estos tres modelos se convertirán en la referencia para tu propio **estándar de modelos**.
