## jQuery API及用法总结

### 选择器
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

3. [attribute^='value']^=以value开头的所有元素

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

4. [attribute|='value']

跟[attribute = value]基本类似，均是选择属性名等于该属性值的所有元素

5. [attribute!='value']

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

6. [attribute*='value']
只要属性名中的一部分包含了value这个属性值，均会被选择到

div[title*=demo]

此例中第一个和第二个div均包含demo，所以选择第一二个div元素

```js
<div title = "demo"></div>
<div title = "demodemo"></div>
<div title = "de"></div>

$('div[title*=demo]').html('jianmei');
```













