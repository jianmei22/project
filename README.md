## jQuery API及用法总结

[1.选择器](#1)

[1.1基本选择](#1.1)

[1.2层级选择](#1.2)

[1.3属性选择](#1.3)

[1.4基本筛选](#1.4)

[1.内容筛选](#1.5)

<a id = '1'>
### 选择器 

<a id = '1.1'>
#### 基本选择器 
1. \* 通用选择器

2. .class 类选择器，一个元素可以有多个类(chrome使用原生js函数getElementByClassName()实现)

利用类选择器改变元素的样式
```js
<div class="demo"></div>

<script type="text/javascript">
	$('.demo').css({
		border: '3px solid red',
	})
</script>
```

3. element元素选择器，DOM节点的标签名(调用函数getElementByTagName()实现)

利用元素选择器查找文档中的元素,添加css样式
```js
<script type="text/javascript">
	$('div').css({
		color: 'skyblue',
	})
</script>
```
4. id选择器，具有唯一性,在一个文件中只能使用一次（原生js调用getElementById()函数)

查找id元素添加样式
```js
<div id="demo">demo3</div>

<script type="text/javascript">
	$('#demo').css({
		border: '3px solid skyblue',
	})		
</script>
```
***
<a id = '1.2'>
#### 层级选择器
1. 子选择器(选择父元素的子元素)

```js
<div>
	<p></p>
</div>
<script type="text/javascript">
$('div>p').css({
	border: '3px solid skyblue',
})			
</script>		
```
2. 群组选择器（选择可以匹配的所有元素）

选择.demo和#demo,___以逗号为间隔隔开___
```js
<div class="demo">demo2</div>
<div id="demo">demo3</div>

<script type="text/javascript">
$('.demo, #demo').css({
	border: '2px solid red',
})			
</script>

```
3. 后代选择器（选择元素的下一个元素）

注意：会选择该元素下所有匹配合适的元素

此例中所有的p均会被加上border样式
```js
<div>
	<p>demo</p>
	<p>demo</p>
	<p>demo</p>
</div>

<script type="text/javascript">
$('div p').css({
	border: '1px solid skyblue',
})			
</script>
```
 4. 前缀选择器

此例中选择只有div下面类名为demo的元素
```js
<div class="demo">demo1</div>
<div class="demo">demo2</div>
<div id="demo">demo3</div>

<script type="text/javascript">
	$('div.demo').css({
		color: 'red',
	})		
</script>
```
5. next选择器（只选择到紧跟其后的同级元素）

注意：元素之间的关系必须是同级即兄弟元素，不能为父子关系

此例中选择的是仅紧跟着p标签的第一个span标签，故会改变1的样式
```js
<p></p>
<span>1</span>
<span>2/span>
<span>3</span>
<script type="text/javascript">
    $('p+span').css({
    	border: '2px solid blue',
    })			
</script>
```
6. nextAll选择器（选择到跟随其后的所有同级元素）

同第五个next选择器，只不过选择的范围不同

此例中会选择p标签之后的所有span标签，改变样式
```js
<p></p>
<span>1</span>
<span>2/span>
<span>3</span>

$('p~span').css({
    	border: '2px solid blue',
    })
```
***
<a id = '1.3'>
#### 属性选择器

1. [attribute]

$('div[title]')
查找所有属性名为title的元素

此例三个div均会被添加border样式

```js
<div title = "demo"></div>
<div title = "demo"></div>
<div title = ""></div>

$('div[title = demo]').css({
	border: '5px solid skyblue',
})
```

2. [attribute = value],属性名 = 属性值

 $('div[title = demo]') 
 
查找title的属性值为demo的所有元素并设置样式

此例加边框样式的只有第一个第二个div

```js
<div title = "demo"></div>
<div title = "demo"></div>
<div title = ""></div>

$('div[title = demo]').css({
	border: '5px solid skyblue',
})
```

3. [attribute|='value']

跟[attribute = value]基本类似，均是选择属性名等于该属性值的所有元素

4. [attribute^='value']^=以value开头的所有元素

div[title^=demo]
查找title属性是以demo开头的元素

此例三个div中只有前两个div会被选择改变样式

```js
<div title = "demo"></div>
<div title = "demodemo"></div>
<div title = "de"></div>

$('div[title = demo]').css({
	border: '5px solid skyblue',
})
```

5. [attribute$='value']$=以value结尾的所有元素

div[title$=demo]

查找title属性是以demo结尾的元素

此例三个div中前三个div会被选择改变样式

```js
<div title = "demo"></div>
<div title = "demo demo"></div>
<div title = "demodemo"></div>
<div title = "de"></div>

$('div[title $= demo]').css({
	border: '5px solid skyblue',
})
```

6. [attribute!='value']

这个选择器等同于 :not([attr=value]) 即非

div[title!=demo]

原生dom提供querySelectorAll()提高查询的性能

此例中选择title不等于demo的元素，即第一个和第三个

```js
<div title = "demo"></div>
<div title = "demodemo"></div>
<div title = "de"></div>

$('div[title != demo]').css({
	border: '5px solid skyblue',
})
```

7. [attribute*='value']
只要属性名中的一部分包含了value这个属性值，均会被选择到

div[title*=demo]

此例中第一个和第二个div均包含demo，所以选择第一二个div元素

```js
<div title = "demo"></div>
<div title = "demodemo"></div>
<div title = "de"></div>

$('div[title*=demo]').html('jianmei');
```

8. [attribute~='value']
div[title~=demo]即title属性中有用空格分隔后的值等于demo

此例中第一个和第三个中都含有demo，且第二个有空格，故选择的是第一个和第三个

__注意：__若此例中使用div[title=demo]，则选择的只有第一个

```js
<div title = "demo"></div>
<div title = "de demo"></div>
<div title = "demodemo"></div>
<div title = "de"></div>

$('div[title~=demo]').html('jianmei');
```
***
<a id = '1.4'>
### 基本筛选选择器

1. :eq(index) index 匹配元素的索引值，从0开始

eq = equal平等的，即是等于index的值

此例中选择的是index等于0的div

```js
<div class="demo">demo1</div>
<div class="demo">demo2</div>
<div id="demo">demo3</div>
$('div:eq(0)').css({
	color: 'red',
})
```
2. :gt(index) 

gt = great than 即是大于index的值

此例中第二个和第三个div会被选择，选择的是index大于0的元素

```js
<div class="demo">demo1</div>
<div class="demo">demo2</div>
<div id="demo">demo3</div>
$('div:gt(0)').css({
	color: 'red',
})
```

3. :lt(index) 

lt = less than 即是小于index的值

此例中第一个和第二个div会被选择，选择的是index小于0的元素

```js
<div class="demo">demo1</div>
<div class="demo">demo2</div>
<div id="demo">demo3</div>
$('div:lt(2)').css({
	color: 'red',
})
```

4. :odd选择__index为奇数__的元素,并不是按照视觉可见的顺序

此例中选择的是第二个和第四个div，index分别为1，3

```js
		<div class="demo">demo1</div>
		<div class="demo">demo2</div>
		<div id="demo">demo3</div>
		<div class="demodemo">demo4</div>

			$('div:odd').css({
				color: 'red',
			})
```

5.:even 选择__index为偶数__的元素,并不是按照视觉可见的顺序

此例中选择的是第一个和第三个div，index分别为0，2

```js
		<div class="demo">demo1</div>
		<div class="demo">demo2</div>
		<div id="demo">demo3</div>
		<div class="demodemo">demo4</div>

			$('div:even').css({
				color: 'red',
			})
```

6. :first相当于:eq(0),为了更好的性能，一般使用.filter(':first')

此时的顺序是视觉上可见的顺序

此例中仅选择第一个div

```js
		<div class="demo">demo1</div>
		<div class="demo">demo2</div>
		
			$('div:first').html('jianmei');
```

7. :last，为了更好的性能，一般使用.filter(':last')

此例中仅选择最后一个div

```js
		<div class="demo">demo1</div>
		<div class="demo">demo2</div>
		
			$('div:last').html('jianmei');
```

8. :header 选择所有的标题元素，为了更好的性能，一般使用.filter(':header')

此例中的h1和h2均会被选择，改变样式

```js
		<h1>jianmei</h1>
		<h2>jianmei</h2>
		
			$(':header').css({
				background: 'skyblue',
			})
```

9. :not() 用于过滤的选择器，但是通常会构建非常复杂的选择器，所以大多数情况下使用.not()方法

这里只写.not(selector)方法

此例中选择的是index不是奇数的div，所以选择的是第一个和第三个div

```js
		<div class="demo">demo1</div>
		<div class="demo">demo2</div>
		<div id="demo">demo3</div>
		<div class="demodemo">demo4</div>
		
			$('div').not(':odd').css({
				border: '2px solid skyblue',
			})

```

10. :lang('language') 选择指定语言的所有元素

__注意__：此例中只有第一个和第二个span元素均会被选中，:lang会选中含有language或者第一个符合的language的元素，并不是只要含有language的元素都会被选择

```js
		<span lang = "en">1</span>
		<span lang = "en-mei">2</span>
		<span lang = "mei-en">3</span>
		
			$('span:lang(en)').css({
				border: '2px solid red',
			})
```

11. :root 选择的根元素永远都是html

此例中会向每一个p中添加一个html
```js
			<p>demo</p>
			<p>demo</p>
			<p>demo</p>
			
			$('<b></b>').html($(':root')[0].nodeName).appendTo('p');
```

12. :target 匹配ID和标识符相匹配的元素

例如：给定url : http://example.com/#foo

`$('p:target');`

将选择 `<p id = 'foo'>`的元素

13. :animated选择所有正在执行动画效果的元素

为了更好的使用效果，首先使用纯CSS选择器选择元素，然后使用.filter(":animated")
```bash

学到属性和效果的时候再返回来写animated, 第168行

```
<a id = '1.5'>
### 内容筛选选择器
***
1. :parent()选择所有包含子元素或者文本的父级元素

为了获得更好的性能，首先使用纯css选择器选择元素，然后使用.filter(':parent')


2. :has()

`$('div:has(p)')`选择一个div，这个div内至少含有一个p标签

此处选择的是
```js
		<div><p></p></div>
		<div></div>
			$('div:has(p)').css({
				border: '2px solid skyblue',
			})
```






