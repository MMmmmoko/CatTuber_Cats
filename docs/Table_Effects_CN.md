
# 桌子模型的参数特效"effects"

参数特效是指桌子上的一个按键触发后，另一个参数对此按键的响应。

"effect"字段是加在桌子模型配置文件里的映射之内的一个数组。

## 示例

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

上段内容表示:

键盘上J键抬起时（KeyboardInput内索引为36），模型中参数ID为"CAT_KEY_PINK1_FADE"的参数将在0.3秒的时间里从0.38降到0。(此处仅作说明，键盘上光效的渐隐效果请直接使用AutoFade)

其中"effectType"决定CAT_KEY_PINK1_FADE参数的变化样式。"trigger"决定触发方式。

**"effects"是个数组，一个映射中可以插入多个特效。如"effects":[{ },{ },{ }]**

## "trigger"

触发时机，只有两个值可选。"down"表示在按键按下时触发，"up"表示在按键抬起时触发。

## "effectType"

| 特效名 | 特效效果 |
| :--- | :--- |
| [pulse](#pulse) | 大概这个样子___/\\_____ |
| [pulse_add](#pulse_add) | 如上述，但是重复触发的时候数值会叠加 |
| [sawtooth](#sawtooth) | 大概这个样子___\|\\_____ |
| [sawtooth_add](#sawtooth_add) | 如上述，但是重复触发的时候数值会叠加 |
| [incremental](#incremental) | 整数递增，每次触发时特效参数值+1，超过极值时会归零 |
| [random_integer](#random_integer) | 每次触发时，特效参数会变成范围内随机整数 |
| [random_range](#random_range) | 每次触发时，特效参数会变成范围内随机值  |

##

### pulse

pulse特效在触发时，特效参数的值会从0经过"period"数值的一半的时间到达"peak"值，然后再经过"period"数值的一半的时间回到零。（"period"单位为秒）

\_\_\_/\\\_\_\_\_

示例
```json
{
	"paramID":"CAT_EFFECT",
	"effectType":"pulse",
	"period":0.3,
	"peak":0.38,
	"trigger":"up"
}
```
上述示例的pulse在触发时，CAT_EFFECT参数数值会从0经过0.15秒到达0.38，随后经过0.15秒回到0。


##
### pulse_add
单次pulse_add特效在触发时，与[pulse](#pulse)一样，特效参数的值会从0经过"period"数值的一半的时间到达"peak"值，然后再经过"period"数值的一半的时间回到零。（"period"单位为秒）
\_\_\_/\\\_\_\_\_
被多次触发时，特效参数的值是不同时刻触发的[pulse](#pulse)特效在此时刻的数值的叠加。

F(t)=f(t+t0)+f(t+t1)+f(t+t2)+...

示例
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
sawtooth特效在触发时，特效参数的值会突变成"peak"值，经过"period"数值的秒数，从"peak"值降到零。

\_\_\_|\\_\_\_

示例
```json
{
	"paramID":"CAT_EFFECT",
	"effectType":"sawtooth",
	"period":0.3,
	"peak":0.38,
	"trigger":"up"
}
```
上述示例的sawtooth在触发时，CAT_EFFECT参数数值会从0变为0.38，然后用0.15秒的时间回到0。

##
### sawtooth_add
单次sawtooth_add特效在触发时，与[sawtooth](#sawtooth)类似，特效参数的值会从0增加"peak"值，经过"period"数值的秒数，从"peak"值降到零。

\_\_\_|\\_\_\_

被多次触发时，特效参数的值是不同时刻触发的[sawtooth](#sawtooth)特效在此时刻的数值的叠加。

F(t)=f(t+t0)+f(t+t1)+f(t+t2)+...

示例
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

incremental特效初始值为0，每次触发时数值+1，数值最大可到"peak"值，此时触发数值会变为0。

示例
```json
{
	"paramID":"CAT_EFFECT",
	"effectType":"incremental",
	"peak":5,
	"trigger":"down"
}
```
CAT_EFFECT参数初始值为0，在每次触发时，CAT_EFFECT参数数值将在1，2，3，4，5，0之间依次变化。

提示：想要无限递增的话，把"peak"设置为足够大的值就行，但请设置为小于2,147,483,647的数字。

可以将"peak"设置为1，来实现一个开关。

##
### random_integer

random_integer中使用"period"、"peak"来标识范围，

random_integer初始值为0，每次触发时数值变为[period,peak]范围内的随机整数。

示例
```json
{
	"paramID":"CAT_KEY_X",
	"effectType":"random_integer",
	"period":2,
	"peak":5,
	"trigger":"down"
}
```
在示例里，CAT_KEY_X参数初始值为0，在触发时将在2、3、4、5里随机取值。比如4。


##

### random_range

random_range中使用"period"、"peak"来标识范围，

random_range初始值为0，每次触发时数值变为[period,peak]范围内的随机数。

示例
```json
{
	"paramID":"CAT_KEY_X",
	"effectType":"incremental",
	"period":2,
	"peak":5,
	"trigger":"random_range"
}
```

在示例里，CAT_KEY_X参数初始值为0，在触发时将在[2,5]里随机取值。比如3.65421。
