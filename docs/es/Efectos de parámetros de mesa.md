# Efectos de parámetros "effects" del modelo de mesa

Los **efectos de parámetros** se refieren a cómo al presionar un botón en la mesa, se produce una respuesta en otro parámetro.

El campo `effect` se encuentra como un arreglo en el archivo de configuración del modelo de la mesa.

## Ejemplo

```json
{
	"input":"KeyboardInput",
	"dataType":"BYTE",
	"index":36,
	"type":"point",
	"output":[-2.6,-13.3],
	"paramID":"CAT_KEY_PINK1",
	"weight":1.0,
	"effects":[
	{
		"paramID":"CAT_KEY_PINK1_FADE",
		"effectType":"sawtooth",
		"period":0.3,
		"peak":0.38,
		"trigger":"up"
	}
	]
}
```

En el fragmento anterior:

Cuando la tecla J del teclado se libera (índice `36` en KeyboardInput), el parámetro con ID `"CAT_KEY_PINK1_FADE"` en el modelo disminuirá de `0.38` a `0` en un período de `0.3` segundos. (Esta explicación es solo para fines ilustrativos; para el efecto de desvanecimiento de la luz en el teclado, utiliza directamente AutoFade).

* El campo `"effectType"` establece el estilo de cambio para el parámetro `"CAT_KEY_PINK1_FADE"` en el modelo.

* El campo `"trigger"` determina el tipo de activación.

* El campo `"effects"` es una matriz en la que se pueden insertar múltiples efectos en un mapeo. Por ejemplo: `"effects": [{ },{ },{ }]`

## Campo "trigger"

Indica cuándo se activa el efecto, con solo dos valores posibles: `"down"` significa que se activa al presionar el botón, y `"up"` significa que se activa al soltarlo.

## Campo "effectType"

| Nombre del efecto | Efecto |
| :--- | :--- |
| [pulse](#pulse) | Más o menos así: \_\_\_\/\\\_\_\_ |
| [pulse_add](#pulse_add) | Similar a lo anterior, pero el valor se acumula en activaciones repetidas |
| [sawtooth](#sawtooth) | Más o menos así: \_\_\_\|\\\_\_\_ |
| [sawtooth_add](#sawtooth_add) | Similar a lo anterior, pero el valor se acumula en activaciones repetidas |
| [incremental](#incremental) | Incrementa en números enteros. En cada activación, el valor del parámetro del efecto aumenta en 1, se reinicia al llegar al valor máximo |
| [random_integer](#random_integer) | En cada activación, el parámetro del efecto se convierte en un número entero aleatorio dentro de un rango especificado |
| [random_range](#random_range) | En cada activación, el parámetro del efecto se convierte en un número aleatorio dentro de un rango especificado  |

##
### pulse

Cuando se activa el efecto `"pulse"`, el valor del parámetro del efecto aumentará desde 0 hasta el valor `"peak"` en la mitad del tiempo especificado por `"period"`, luego regresará a `0` en la otra mitad del tiempo. (`"period"` está en segundos)

\_\_\_/\\\_\_\_

Ejemplo:
```json
{
	"paramID":"CAT_EFFECT",
	"effectType":"pulse",
	"period":0.3,
	"peak":0.38,
	"trigger":"up"
}
```
En el ejemplo anterior, cuando se activa el efecto `pulso`, el valor del parámetro `CAT_EFFECT` aumentará de `0` a `0.38` en `0.15` segundos, luego volverá a `0` en `0.15` segundos.

##
### pulse_add
Cuando se activa el efecto `"pulse_add"`, al igual que con [`"pulse"`](#pulse), el valor del parámetro del efecto aumentará desde `0` hasta el valor `"peak"` en la mitad del tiempo especificado por `"period"`, luego regresará a `0` en la otra mitad del tiempo. (`"period"` está en segundos)

\_\_\_/\\\_\_\_

Cuando se activa múltiples veces, el valor del parámetro del efecto es la suma acumulada de los valores de los efectos [`"pulse"`](#pulse) en los momentos individuales en que se activaron.

$$
F(t) = f(t + t_0) + f(t + t_1) + f(t + t_2) + …
$$

Ejemplo:
```json
{
	"paramID":"CAT_EFFECT",
	"effectType":"pulse_add",
	"period":4,
	"peak":1,
	"trigger":"up"
}
```

##
### sawtooth
Cuando se activa el efecto `"sawtooth"`, el valor del parámetro del efecto cambia abruptamente de `0` al valor `"peak"`, luego regresará gradualmente a `0` en el tiempo especificado por `"period"` (en segundos).

\_\_\_|\\_\_\_

Ejemplo:
```json
{
	"paramID":"CAT_EFFECT",
	"effectType":"sawtooth",
	"period":0.3,
	"peak":0.38,
	"trigger":"up"
}
```
En el ejemplo anterior, cuando se activa el efecto `diente de sierra`, el valor del parámetro `CAT_EFFECT` cambiará de `0` a `0.38`, luego volverá a `0` en `0.15` segundos.

##
### sawtooth_add
单次sawtooth_add特效在触发时，与[sawtooth](#sawtooth)类似，特效参数的值会从0增加"peak"值，经过"period"数值的秒数，从"peak"值降到零。

Cuando se activa el efecto `"sawtooth_add"`, al igual que con [`"sawtooth"`](#sawtooth), el valor del parámetro del efecto cambia abruptamente de `0` al valor `"peak"`, luego regresará gradualmente a `0` en el tiempo especificado por `"period"` (en segundos).

\_\_\_|\\_\_\_

Cuando se activa múltiples veces, el valor del parámetro del efecto es la suma acumulada de los valores de los efectos [`"sawtooth"`](#sawtooth) en los momentos individuales en que se activaron.

$$
F(t) = f(t + t_0) + f(t + t_1) + f(t + t_2) + …
$$

Ejemplo:
```json
{
	"paramID":"CAT_EFFECT",
	"effectType":"sawtooth_add",
	"period":4,
	"peak":1,
	"trigger":"up"
}
```

##
### incremental
El efecto `"incremental"` tiene un valor inicial de 0 y cada vez que se activa, el valor se aumenta en 1 hasta alcanzar el valor `"peak"`, y en ese momento, el valor se reinicia a 0.

Ejemplo:
```json
{
	"paramID":"CAT_EFFECT",
	"effectType":"incremental",
	"peak":5,
	"trigger":"down"
}
```

En el ejemplo anterior, el parámetro `CAT_EFFECT` tiene un valor inicial de 0. Cada vez que se activa, el valor de `CAT_EFFECT` cambiará sucesivamente entre `1`, `2`, `3`, `4`, `5` y `0`.

Consejo: Si deseas un incremento infinito, puedes configurar `"peak"` con un valor lo suficientemente grande, pero asegúrate de que sea menor que `2,147,483,647`.

También puedes configurar `"peak"` en `1` para lograr un efecto de interruptor.

##
### random_integer
En el efecto `"random_integer"`, se utilizan `"period"` y `"peak"` para definir un rango.

El efecto `"random_integer"` comienza en `0` y en cada activación, el valor se convierte en un número entero aleatorio dentro del rango `[period, peak]`.

Ejemplo:
```json
{
	"paramID":"CAT_KEY_X",
	"effectType":"random_integer",
	"period":2,
	"peak":5,
	"trigger":"down"
}
```
En el ejemplo anterior, el parámetro `CAT_KEY_X` comienza en `0` y en cada activación tomará un valor aleatorio entre `2`, `3`, `4` y `5`. Por ejemplo, podría ser `4`.

##
### random_range

En el efecto `"random_range"`, se utiliza `"period"` y `"peak"` para definir un rango.

El efecto `"random_range"` comienza en `0` y en cada activación, el valor se convierte en un número aleatorio dentro del rango `[period, peak]`.

Ejemplo:
```json
{
	"paramID":"CAT_KEY_X",
	"effectType":"incremental",
	"period":2,
	"peak":5,
	"trigger":"random_range"
}
```
En el ejemplo anterior, el parámetro `CAT_KEY_X` comienza en `0` y en cada activación tomará un valor aleatorio dentro de `[2, 5]`. Por ejemplo, podría ser `3.65421`.