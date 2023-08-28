# Archivo de configuración de la mesa
El **archivo de configuración de la mesa** se coloca junto al **modelo de mesa de CatTuber** y se utiliza para configurar efectos y mapeos.

Este archivo de configuración está en formato JSON y se puede abrir con cualquier editor de texto. El formato JSON no es complicado; puedes inferir las relaciones lógicas a partir del contenido JSON. Puedes consultar el contenido de otros elementos dentro del archivo o el contenido de otros archivos JSON. Asegúrate de no usar signos de puntuación en chino y de no omitir comas ni agregar comas de más (debe haber comas entre elementos del mismo nivel; el último elemento de un nivel no lleva coma al final). Si es necesario, utiliza un validador de formato JSON.

## Campo "Version" (obligatorio)
Indica cómo el software debe leer el archivo de configuración. Actualmente, solo se admite el valor `2`.

## Campo "AutoFade" (opcional, recomendado)

Se debe utilizar junto con la etiqueta `"tag"` (consulte el texto siguiente). Al configurar este campo, los efectos de iluminación de las teclas pueden desvanecerse lentamente después de soltarlas.

```json
"AutoFade":
{
	"period":0.3,
	"opacity":0.38
}
```
El ejemplo anterior indica que, para las teclas con la etiqueta especificada, el valor del parámetro de la tecla cambiará de 1 a 0.38 cuando se suelte,  y luego, disminuirá a 0 en 0.3 segundos.

## Campo "OutputMap" (obligatorio)
El campo `"OutputMap"` es una matriz bidimensional donde la primera dimensión representa el **número de mano** y la segunda dimensión representa los diversos **mapeos en esa mano**.

En CatTuber, los números de mano comienzan desde la mano derecha del personaje. Por ejemplo, "OutputMap": [[A, B], [C, D]] indica que en la mano derecha hay dos mapeos, A y B, y en la mano izquierda hay dos mapeos, C y D.

Para permitir que los lectores se familiaricen rápidamente, aquí hay dos ejemplos de mapeos comunes.

### Ejemplo de mapeo de una tecla del teclado:
```json
{
	"input":"KeyboardInput",
	"dataType":"BYTE",
	"index":36,
	"type":"point",
	"output":[13,-6.5],
	"paramID":"CAT_KEY_J",
	"weight":1.0,
	"tag":"autoFade"
}
```
Este mapeo significa que cuando se presiona la tecla J en el teclado, se activará el parámetro con el `ID` de `"CAT_KEY_J"` en la mesa, y la mano se posicionará en las coordenadas `(X=13, Y=-6.5)`.

El `"index"` de `36` corresponde al índice de la tecla J en los datos de "KeyboardInput" y se puede consultar el índice de cada tecla a través del programa de [**búsqueda de teclas**](../../tools/KeyIndexQuery.exe) en este repositorio.

El `"weight"` indica el peso. Cuando se presionan múltiples teclas al mismo tiempo, la posición real de la mano es el promedio ponderado de las coordenadas de las manos en estos varios mapeos.

La etiqueta `"tag":"autoFade"` indica que esta tecla se ajusta al efecto `"AutoFade"` mencionado anteriormente. Sin esta etiqueta, en el momento en que se levanta la mano, el valor del parámetro de la tecla se establecerá directamente en 0.

### Ejemplo de mapeo de un rango del ratón
```json
{
	"input":"MousePos_AppRelated",
	"dataType":"float",
	"index":[0,1],
	"type":"area",
	"output":[[-30.0,4.8],[-22.4,3.0],[-30,-30.0],[-18.1,-30.0]],
	"paramID":["CAT_RX","CAT_RY"],
	"weight":1000.0,
	"mode":1,
	"tag":"mouse"
}
```
Este mapeo significa que cuando se mueve el ratón, la posición X e Y del modelo de la mano y del ratón se moverán dentro de un rango definido por cuatro puntos: arriba a la izquierda `(-30.0, 4.8)`, arriba a la derecha `(-22.4, 3.0)`, abajo a la izquierda `(-30, -30.0)` y abajo a la derecha `(-18.1, -30.0)`. Los valores de los parámetros `"CAT_RX"` y `"CAT_RY"` en la mesa también cambiarán (cuando se usa el ratón, estos dos parámetros no tienen uso debido a que no han sido modelados; pero en futuras versiones del software, estos dos parámetros podrán usarse para el joystick de los mandos).

# Contenido avanzado
A continuación, se presentan algunos contenidos avanzados que permiten lograr efectos específicos. Estos contenidos no son obligatorios en el archivo de configuración. Si aún no estás familiarizado o estás comenzando con la creación de modelos para CatTuber, puedes leer estos contenidos después de haber creado y importado exitosamente un modelo de mesa.

[Efectos de parámetros "effects"](Efectos%20de%20parámetros%20de%20mesa.md).
