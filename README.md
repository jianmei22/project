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

### 内容筛选
***
1. :parent选择所有包含子元素或者文本的父级元素

为了获得更好的性能，首先使用纯css选择器选择元素，然后使用.filter(':parent')

__注意__:parent涉及的子元素包含文本节点

此例中选择的是第一个和第二个div，因为只有第三个是没有子元素和文本节点的
```js
		<div><p></p></div>
		<div> </div>
		<div></div>
		
			$('div:parent').css({
				border: '3px solid skyblue',
			})
```

2. empty:和parent相反，选择没有包含子元素的元素

此例中选择的是第三个div，因为只有第三个是没有子元素和文本节点的
```js
		<div><p></p></div>
		<div> </div>
		<div></div>
		
			$('div:empty').css({
				border: '3px solid skyblue',
			})
```

3. :has()

`$('div:has(p)')`选择一个div，这个div内至少含有一个p标签

此处选择的是第一个div，只有第一个div内含有p标签
```js
		<div><p></p></div>
		<div></div>
		
			$('div:has(p)').css({
				border: '2px solid skyblue',
			})
```

4. :contains(text)text区分大小写，选择所有包含指定文本的元素

`$('div:has(mei)')` 查找所有含有mei的div

```js
		<div>jian mei</div>
		<div>mei</div>
		
			$('div:contains(mei)').css({
				border: '2px solid skyblue'
			})
```

***
### 可见性筛选

1. :hidden 选择所有隐藏的元素

元素可以被认为是隐藏的几种情况：

* css的display值为none
* type = "hidden"
* 元素的高度和宽度显式设置为0

元素visibility:hidden和opcity:0被认为是可见的，因为他们仍然占据文档空间，

使用:hidden()查询不能充分利用原生DOM提供的querySelectorAll()方法来提高性能。为了在现代浏览器上获得更佳的性能，请使用.filter(":hidden")代替

此例中div本来是隐藏的，选择的是有隐藏元素的div，并在3s之后显示
```js
		<div style="display: none;">hidden</div>
		
			// :hidden
			$('div:hidden').show(3000);
			```
1. :visible 选择所有可见的元素

跟hidden用法相反
```js
			<p>demo</p>
			<p>demo</p>
			<p>demo</p>
			
			$('p:visible').click(function() {
				$(this).css({
					background: 'skyblue',
				})
			})
```
***
### 子元素筛选选择器

1. :first-child 选择所有父级元素下的第一个子元素 

此例中仅div下面的第一个p改变样式
```js
		<div>
			<p>demo</p>
			<p>demo</p>
			<p>demo</p>
		</div>
		
			$('div p:first-child').css({
				'text-decoration': 'underline',
			})
```

2. first-of-type 选择所有相同的元素名称的第一个兄弟元素

_注意_：此例中跟first-child不一样的地方是，first-child只选择直系的第一个，如果第一个不是，则不选择，first-of-type选择的是只要包含有就选择包含的第一个兄弟元素，此处选择的是div内包含的p标签的第一个
```js
		<div>
			<a href=""></a>
			<p>demo</p>
			<p>demo</p>
			<p>demo</p>
		</div>
		
			$('div p:first-of-type').css({
				background: 'red',
			})
```

3. :last-child 选择所有父级元素下的第一个子元素 

此例中仅div下面的最后一个p改变样式
```js
		<div>
			<p>demo</p>
			<p>demo</p>
			<p>demo</p>
		</div>
		
			$('div p:last-child').css({
				'text-decoration': 'underline',
			})
```

4. last-of-type 选择所有相同的元素名称的最后一个兄弟元素

原理同上：first-of-type，
```js
		<div>
			<a href=""></a>
			<p>demo</p>
			<p>demo</p>
			<p>demo</p>
		</div>
		
			$('div p:last-of-type').css({
				background: 'red',
			})
```

5. :nth-child(index/even/odd/equation) 

index：匹配的索引值，从1开始，可以是even（偶数） odd（奇数）2n

__注意__：和eq()不一样的地方是，eq()的索引是从0开始的 

```js
		<div>
			<button></button>
			<button></button>
		</div>
		<div>
			<button></button>
		</div>
		
	$('div:nth-child(2)').click(function () {
				$(this).css({
					border: '2px solid skyblue',
				});
			});
```

6. :only-child 如果某元素是其父元素的唯一一个子元素，就会被选择，如果父元素还有其他元素，就不会被选择

此例中，只有第二个div内有唯一一个button，所以选择的是第二个，在第二个button内添加文本：alone
```js
		<div>
			<button></button>
			<button></button>
		</div>
		<div>
			<button></button>
		</div>
		
			$('div button:only-child').text('alone').css({
				border: '2px solid skyblue',
			}
```
7. ：nth-of-type() 同一个父元素下面标签名字相同的子元素中的第n个

index是从1开始的，可以是字符串even或者odd或者是方程式:nth-of-type(even), :nth-of-type(4n)

此例中选择的是第一个div内的button兄弟元素的第二个
```js
		<div>
			<button></button>
			<button></button>
		</div>
		<div>
			<button></button>
		</div>
		
			$('div button:nth-of-type(1)').text('alone').css({
				border: '2px solid skyblue',
			}
```
***
### 表单选择器

1. :button 选择所有按钮元素和类型为按钮的元素

此例中两个元素均被选择且添加move样式
```js
    <input type="button" value="Input Button"/>
    <button>Button</button>
	
			$(':button').addClass('move');
	
```
2. :checkbox 查询不能充分利用原生DOM提供的querySelectorAll() 方法来提高性能，建议使用[type="checkbox"]代替

```js
    <input type="checkbox" />
	
			$(':checkbox').wrap("<span style='background-color:red'>");
			----------------------------------------------------------
			//最好这样写
			$('[type = checkbox]').wrap("<span style='background-color:red'>");
```

3. :checked 匹配所有勾选的元素

此例中选择了第三个处于选中状态的input
```js
    <input type="checkbox" />
    <input type="checkbox" />
    <input type="checkbox" checked />
	
			$('input:checked').wrap("<span style='background-color:red'>");
			```
4. :disabled 匹配所有禁用的元素

此例中选择第一个input
```js
    <input type="checkbox" disabled/>
    <input type="checkbox" />
	
			$('input:disabled').wrap("<span style='background-color:red'>");
```

5. enabled 匹配所有可用的元素，和disabled用法相反

此例中选择第二个input
```js
    <input type="checkbox" disabled/>
    <input type="checkbox" />
	
			$('input:enabled').wrap("<span style='background-color:red'>");
```

6. :focus 选择当前获取焦点的元素

此例中选择的是当前获取焦点的input,且该input的类型为text，再设置样式
```js
    <input type="text" />
	
			$('input[type = text]').focus(function () {
				$(this).css({
					background:'red',
				})
			})
```

总结：:file :image :input : password :radio :reset :select :submit :text 

均是选择所有类型为该属性的元素用法同上。
### 属性/css

#### 属性
1. .attr()

attr()设置普通属性，prop()设置特有属性

获取或者设置匹配的元素集合中的第一个元素的属性的值

如果需要获取或者设置每个单独元素的属性值，需要依靠.each() .map()方式循环

此例中同时给img添加alt和title属性

```js
		<img src="../img/4.jpg" alt="" id="photo">
		
			$('#photo').attr({
				alt: 'jianemi',
				title: 'meimei',
			})
```

2. prop()

获取或者设置匹配的元素集中第一个元素的属性值

.prop()方法只获得第一个匹配元素的属性值

禁止页面上所有的复选框

```js
		<input type="checkbox" checked>
		<input type="checkbox">
		<input type="checkbox">
		
			$("input[type='checkbox']").prop({
				disabled: true,
			})
```
3.removeAttr()

为匹配的元素集合中的每一个元素中移除一个属性(attribute)

removeAttr()使用的是原生的js方法

ie 8，9，11中使用removeAttr()删除一个内联onclick事件处理程序不会达到预期的效果，为了避免潜在的问题，使用.prop()代替

点击按钮,添加或者删除按钮后面input元素的title属性，此例使用立即执行函数

```js
		<button>enable</button>
		<input type="text" title="hello">
		<div id="log"></div>
		
			(function () {
				var inputTitle = $("input").attr("title");
				$("button").click(function () {
					var input = $(this).next();
					if(input.attr("title") == inputTitle) {
						input.removeAttr("title")
					}else{
						input.attr("title", inputTitle);
					}
					$("#log").html("input title is now" + input.attr("title"));
				});
			})();
```

4. .removeprop

为集合中匹配的元素删除一个属性(property)

__注意__：此方法不可以用来删除原生的属性，例如：cheackede disabled selected

此例中设置一个div的数字属性，然后将其删除

para是直接定义在全局对象上面的，即定义在window上面的，所以可以访问window.para来访问，直接访问para
```js
		<div id="log"></div>
		
			para = $("#log");
			para
				.prop('code', 1234)
				.append('code is:', String(para.prop('code')),'.')
				.removeProp('code')
				// 这个时候已经将prop添加的字符串删除
				.append('now code is:', String(para.prop('code')),'.')
```

5. val()

获取匹配的元素集合中第一个元素的当前值，这个方法不接受任何参数

.val方法主要用于获取表单元素的值，如input select和textarea，当在一个空集合上调用的时候，返回值为undefined

例：取得文本框的值

```js
		<input type="text" value="text">
		<p></p>
		
			// 取得文本框的值
			$("input").keyup(function () {
				// 获取当前的value值
				var value = $(this).val();
				// 向p中添加获取的value值
				$("p").text(value);
			}).keyup();
```

val()允许你传递一个元素值的数组，当使用在包含像input select option等jquery对象时很有用

例：点击按钮时，在文本框显示按钮值

```js
		<button>feed </button>
		<button>the </button>
		<button>input </button>
		<button type="reset">reset</button>
		<input type="text" value="click a button" lang="en">
		
			$("button").click(function () {
				// 获取button的text文本
				var text = $(this).text();
				// 将获取到的文本添加到value
				$("input[lang = 'en']").val(text);
			})
			// 点击重置按钮
			$("button[type = reset]").click(function () {
				$("input[lang = 'en']").val('click a button');
			})
```
### CSS

1. addClass() 为每个匹配的元素添加指定的一个或者多个样式类名

对所有匹配的元素添加多个样式类名 用空格隔开

$("p").addClass('css1 css2')

通常和removeClass一起使用

$("p").removeClass('css1 css2').addClass('css3')

```js
		<p>jianmei</p>
		<p>meimei</p>
		<p>jianjian</p>
		
			// 给第二个p添加elem样式
			$("p:nth(1)").addClass("elem");
```
2. css 获取匹配元素集合中的第一个元素的样式属性的计算值或设置每一个匹配元素的一个或者多个css属性

```js
		<p>jianmei</p>
		<p>meimei</p>
		<p>jianjian</p>
		
			// 点击元素,获取它的背景颜色
			$("p").click(function () {
				var color = $(this).css("background-color");
				$("input").val(color);
			})
```

设置样式，每点击一次div 会改变样式或者恢复样式

```js
		<div id="log"></div>
		
			// 增加div的宽度
			// 定义count,用于计算次数
			var count = 0;
			$("#log").click(function () {
				// 每点击一次,count+1
				count ++;
				if(count % 2 == 0){
					$(this).css({
						width: '300px',
					})
				}else{
					$(this).css({
						width: '400px',
					})
				}
			})
```

3. hasClass()

确定任何一个匹配的元素是否有被分配给定的样式（类）


```js
		<button>feed </button>
		<button class="elem">the </button>
		<button>input </button>
		
		    $("input").hasClass("elem").toString();
```

4. removeClass()

移除集合中每个匹配元素中一个或者多个样式

从匹配的元素中移除elem类

```js
		<button>feed </button>
		<button class="elem">the </button>
		<button>input </button>
	
			$("button").removeClass('elem');
			//如果removeClass()后面跟的是(),则代表移出当前元素的所有样式类
```

5. toggleClass()

为匹配的元素集合中的每一个元素添加或者删除一个或多个样式类(class),取决于这个样式类是否存在或者参数的值。

如果存在就删除，如果不存在就添加

```js
		<p>jianmei</p>
		<p class="elem">meimei</p>
		<p>jianjian</p>
		
			$("p").click(function () {
			$(this).toggleClass('elem');
		})
```
### 尺寸

1. .height()

获取匹配元素集合中的第一个元素的当前计算高度值或者设置每一个匹配元素的高度值

__注意__: height中的高度只包括元素本身的高度和宽度

.css('height') 和.height()之间的区别就是后者返回一个没有单位的数值，前者是返回一个带有完整单位的字符串，当一个元素的高度需要计算的时候通常使用.height()
```js
		<p>jianmei</p>
		<p class="elem">meimei</p>
		<p>jianjian</p>
		
			// 点击p的时候增加p的长度,并且改变颜色
			$("p").click(function () {
				$(this).width(300)
					   .css({
						   cursor: "auto",
						   background: '#90EE90',
					   })
			})
```

2. width和height用法一致

3. innerHeight()

__注意__: innerHeight()返回的高度包括当前元素本身的高度 + padding的高度


```js
		<p>jianmei</p>
		<p>jianjian</p>
		<p>jianjian</p>
		
			// 每点击一次,innerHeight就会改变并改变颜色
			var count = 0;
			$("p").click(function () {
				count ++;
				if(count % 2 == 1) {
					$(this).innerHeight(50).addClass('elem');
				}
				else {
					$(this).innerHeight(30).addClass();
				}
				})
```
4. innerWidth和innerHeight用法一致

5.outerHeight()

获取或者设置匹配的元素集合中第一个元素的当前计算外部高度

outerHeight的高度包括：本身的高度 + padding + border + (margin)

当outerHeight(true)时，包括margin，margin是可选的


```js
		<p>jianmei</p>
		<p>jianjian</p>
		<p>jianjian</p>
		
			var oheight = 60;
			$("p").click(function() {
				$(this).outerHeight(oheight).addClass('elem');
				// 每点击一次就减少4
				oheight -= 4;
			})
			
			var oheight = 60;
			$("p").one('click', function() {
				$(this).outerHeight(oheight).addClass('elem');
				// 只有点击一次的效果
				oheight -= 4;
			})
```
### 位置

1. .offset()

在匹配的元素集合中，获取的第一个元素的当前坐标，或者设置每一个元素的坐标，坐标相对于文档

点击查看当前元素的位置

```js
		<p>jianjian</p>
		<div id="log"></div>
		
			$('#log', document.body).click(function (e) {
				var offset = $(this).offset();
				// 阻止事件冒泡
				e.stopPropagation();
				$('p').text(offset.left + ', ' + offset.top);
			});	
```

2. .position()

和offset的区别在于position是i相对于父级元素的位移，如果要取得这个新的元素的位置，那么使用offset更合适

```js
		<p>jianjian</p>
		<div id="log"></div>
		
			$('#log').click(function (e) {
				var position = 
				$('p').text(position.left + ', ' + position.top);
			})
```
3. offsetParent()

取得离指定元素最近的含有定位信息的祖先元素，含有定位信息的元素指的是：

css的position属性是relative absolute 或者fixed元素

```js
		<ul>
			<li>22
				<ul>
					<li style="position: relative;">1</li>
					<li class="elem">2</li>
					<li>3</li>
				</ul>
			</li>
		</ul>
		
			$('li.elem').offsetParent().css('background-color', 'red');
```

4. scrollLeft()

获取匹配的元素集合中第一个元素的当前水平滚动条的位置或者设置每个匹配元素的水平滚动条位置

获取div的scrollLeft

此例中可知当前div水平滚动条的距离
```js
		<div id="log"></div>
		
			$('#log').text('scrollLeft:' + $(this).scrollLeft());
```
5. scrollTop()

获取匹配的元素集合中第一个元素的当前垂直滚动条的位置或者设置每个匹配元素的垂直滚动条位置

此例中可知当前div垂直滚动条的距离
```js
		<div id="log"></div>
		
			$('#log').text('scrollTop:' + $(this).scrollTop());
```

### 数据

1. .data()

在匹配元素上存储任意相关数据或返回匹配的元素集合中的第一个元素的给定名称的数据存储的值

.data(obj) 一个用于更新数据的键/值对

.data()方法允许我们再dom元素上绑定任意类型的数据，避免了循环引用的内存的泄露风险

从div元素存储然后找回一个值

此例中可以将#log内存储的数据分别提取到span中
```js
		<div id="log">
			the value is 
			<span></span>
			and
			<span></span>
		</div>
		
			$('#log').data('test', {
				first: 16,
				last: 'jianmei',
			});
			//将test的first内容添加到#log上
			$('span:first').text($('#log').data('test').first);
			$('span:last').text($('#log').data('test').last);
```
2. .removeData()

在元素上移除绑定的数据

.removeData([name]),要移除的存储数据名

.removeData([list]),一个数组或者空间分隔的字符串命名要删除的数据块

```js
		<div id="log">
			the value is 
			<span></span>
			and
			<span></span>
		</div>
		
			$('#log').data('test1', {
				first: 16,
			});
			$('#log').data('test2', {
				last: 'jianmei',
			});
			$('span:first').text($('#log').data('test1').first);
			//移除绑定在#log上的test1数据
			$('#log').removeData('test2');
			$('span:last').text($('#log').data('test2').last);
```



