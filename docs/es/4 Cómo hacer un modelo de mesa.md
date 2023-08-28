# Cómo hacer un modelo de mesa

### Preparación de ilustraciones (¿esto también cuenta como ilustración?)
No recomendamos dibujar directamente el teclado sobre la mesa como versión final en el PSD. Puedes consultar el archivo PSD y el archivo cmo3 del modelo de mesa de demostración. Nuestro enfoque consiste en dibujar un borde de tecla, un efecto de luz de tecla y un resplandor de tecla (opcional, pero se recomienda agregar un resplandor luminoso al modelo que represente la tecla). Luego prepara varias capas de texto (es decir, patrones de tapa de tecla) en la misma posición, y después, en el editor Live2D, ensambla las en un teclado completo sin perspectiva. Agrega un deformador sobre el teclado y úsalo para colocar el teclado en la mesa con la posición, el tamaño y la perspectiva adecuados.

Si ya tienes preparado un modelo completo de mesa con teclado, puedes omitir este paso, ya que puedes ensamblarlo en el editor Live2D sin necesidad de proporcionar nuevos recursos.

### Preparación antes de modelar
Abre Live2D Cubism Editor e importa el archivo PSD del modelo de mesa.

Los parámetros por defecto proporcionados por el editor de Live2D para la mesa no son necesarios, elimina todos los parámetros. Puedes definir tus propios IDs de parámetros para la mesa. Si planeas crear un modelo de mesa con muchas teclas, puedes importar los ["parámetros de teclado completo de CatTuber"](../../models/CatTuber全键盘参数.csv) desde el repositorio al editor.

![Imagen 1](imgs/img3_1.png)

Si estás comenzando con un modelo de mesa con teclado completo existente (como el que se encuentra en esta biblioteca), simplemente abre una copia de ese modelo completo en el Live2D Cubism Editor.

Importa el modelo de personaje estándar dentro de este modelo de mesa (solo como referencia, no para salida).

### Ensamblaje de teclas
Elimina las demás teclas del modelo de teclado completo y organiza las teclas individuales en la disposición de un teclado plano mediante desplazamiento.

Si no tienes un deformador, aplica uno al teclado plano y crea un parámetro temporal en el deformador para guardar la forma inicial.

Muestra el modelo del personaje y ajusta el deformador usando el modelo del personaje como referencia para colocar el teclado en la mesa con la posición, tamaño y perspectiva adecuada.

Si no estás comenzando con un teclado completo, ajusta la opacidad de los efectos de luz y resplandor en los parámetros correspondientes.

Si estás comenzando con un teclado completo que ya tiene parámetros configurados, verifica de que todos los parámetros de las teclas están configurados correctamente en esta etapa.

### Exportación del modelo
Selecciona la opción de exportación "SDK for Native 4.0". **Asegúrate de que los nombres de los archivos de modelo y animación exportados desde el editor no contengan caracteres chinos ni caracteres de ancho completo.**

### Expresiones y animaciones
¿Un modelo de mesa no puede tener expresiones y animaciones?

En la versión actual, CatTuber no cuenta con un sistema completo de expresiones y animaciones, principalmente debido a que el sistema de eventos de CatTuber aún no está completamente desarrollado. Se espera poder controlar las expresiones y animaciones del modelo a través de este sistema de eventos, por ejemplo, como emitir un evento cuando se presiona una tecla con una frecuencia determinada, y que el modelo de mesa reciba este evento y desencadene una animación efecto visual.

Sin embargo, las animaciones en modo inactivo ("Idle") son compatibles. Puedes agregar animaciones a la categoría "Idle" a través de Live2D Cubism Viewer o editar el archivo `*.model3.json` manualmente.

### Creación del archivo de configuración
El archivo de configuración del modelo de mesa es crucial para vincular la mesa y el personaje. No solo determina cómo la mesa responderá a la entrada de teclas en términos de parámetros del modelo, sino también dónde deben colocarse las manos.

Para no entorpecer la lectura, por favor [consulta aquí la guía sobre el archivo de configuración de la mesa](Archivo%20de%20configuración%20de%20la%20mesa.md).

### Importación en CatTuber
1. Crea una nueva carpeta y dale el nombre de tu modelo (este nombre puede contener caracteres chinos y se mostrará en la interfaz de selección de modelos de CatTuber).
2. Coloca una imagen PNG de 256x256 llamada Cover.png en esta carpeta.
3. Crea una subcarpeta llamada "l2dmodel" dentro de esta carpeta y coloca en ella los archivos de modelo y animación exportados desde el editor. **Renombra el archivo** `*.model3.json` **a** `cat.model3.json`**. Asegúrate de que los nombres de los archivos de modelo y animación exportados desde el editor no contengan caracteres chinos ni otros caracteres de ancho completo.**
4. Coloca el contenido mencionado en la carpeta "Resources\Table" dentro de la carpeta de CatTuber.
5. Coloca un archivo de configuración con el mismo nombre al lado de la carpeta.

**Esta imagen es un ejemplo de la ruta del modelo de mesa; el modelo de mesa se encuentra en Resources\Table.**

![Imagen 2](imgs/img3_2.png)
