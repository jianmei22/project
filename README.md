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
### 操作

#### 拷贝
```bash
.clone 创建一个匹配的元素集合的深度拷贝副本

.clone()方法深度复制所有匹配的元素集合，包括所有匹配元素，元素的下级元素，文字节点

当和插入方法联合使用的时候，.clone()对于复制页面上的元素很方便

__注意__:当使用clone的时候，在将它插入到文档之前，我们可以修改克隆后的元素或者元素内容

```
复制所有的b元素然后将他们插入到所有的段落中
```js
		<b>hello</b>
		<p>have a good day</p>
		
			// prependTo是将元素插入到前面
			// $('b').clone().prependTo('p');
			// appendTo是将元素插入到后面,就是添加的意思
			$('b').clone().appendTo('p');
```		
#### DOM插入、包裹

1. .wrap()

在集合中匹配的每一个元素周围包裹一个html结构

在所有的p外面包裹一层div，此例中会有两个div

```js
		<p>have a good day</p>
		<p>have a nice day</p>
		
		//在p外面包裹一个class为demo的div
			$('p').wrap("<div class = 'demo'></div>")
```
2. wrapAll()

在集合中所有匹配元素的外面包裹一个html元素，此例中只有一个包裹在两个p元素怒外面的div，div的数量只有一个

```js
		<p>have a good day</p>
		<p>have a nice day</p>
		
			// 与wrap不同的是wrap是在匹配符合的每一个元素外面都要加一个div
			// 而wrapAll只在所有匹配的元素外面加一层div		
			$('p').wrapAll("<div class = 'demo'></div>")
```

3. wrapInner()

在匹配元素里的内容外包一层结构

选择所有的段落，包裹每一个匹配元素的内容

__注意__:wrap和wrapInner都是包裹每一个匹配的元素

__但是不同的是wrap是在选择的每一个元素外包裹一层，但是wrapInner是在选择的每个元素的内容外包裹一层__

```js
		<p>have a good day</p>
		<p>have a nice day</p>
		
		//包裹的是内容have a good day
			$('p').wrapInner("<div class = 'demo'></div>")
```
####DOM插入，内部插入

1. append()

在每个匹配元素里面的末尾处插入参数内容
```js
		// 在div内插入p
			$('div').append($('b'));
```

2. appendTo()

将匹配的元素插入到目标元素的最后面

```js
		<b>hello</b>
		<div class="demo"></div>
		
		// 将p插入到div内
			$('b').appendTo($('.demo'));
```
3. html()

获取集合中第一个匹配元素的html内容或者设置每一个匹配元素的html内容

```js
		<div class="demo">123</div>
		<div class="demo">123</div>
		<div class="demo">123</div>
		
			// 如果添加的是空的字符串,则代表清空div内的内容
			// $('.demo').html('');
			// 向div内添加内容
			$('.demo').html('jianmei');
```
4.prepend()

将参数内容插入到每个匹配元素的前面（元素内部）

```js
		<b>hello</b>
		<div class="demo">123</div>
		
			// 在div内插入b
			// b元素的内容会放在原本div内容的前面,跟append是相反的
			$('.demo').prepend($('b'));
```
5. prependTo()

将所有元素插入到目标前面（元素内）

```js
		<b>hello</b>
		<div class="demo">123</div>
		
			// 将b插入到div内
			$('b').prependTo($('.demo'));
```
6. text()

得到匹配元素集合中每个元素的文本内容，包括他们的后代，或者设置匹配元素集合中每一个元素的文本内容为指定的文本内容

```js
		<p>have a good day</p>
		<p>have a nice day</p>
		
			// 在段落p中添加文本
			$('p').text('jianmeinew text');
```
### DOM插入、外部插入

1、after()

在匹配元素集合中的每个元素后面插入参数所指定的内容，作为其兄弟节点

```js
		<div class="demo">123</div>
		<div class="demo">123</div>
		
			// 在demo类之后插入p标签
			// $('.demo').after('<p>jianmei</p>')
			// 在demo类后插入所有的p
			$('.demo').after($('p'));
```
2、 before和after的理论是一样的，根据参数的设定，在匹配的元素前面插入内容，外部插入

```js
			// 在demo类之前插入p标签
			$('.demo').before('<p>jianmei</p>')
```
3、 insertAfter和after是一样的功能，主要是插入内容和目标的位置不同，

```js
			//将p插入到demo类之后
			$('p').insertAfter('.demo');
```
4、 同理可知insertBefore的原理

```js
			// 将p插入demo类之前
			$('p').insertBefore('.demo');
```

#### DOM移除

1、 detach(),从DOM中去掉所有匹配的元素

detach和remove方法一样，除了deach保存所有jquery数据和被移走的元素相关联

当需要移走一个数据，不久又将该元素插入DOM时，常用此方法。
```js
		<p>hello</p>
		<p>you</p>
		<button>meimei</button>
		
			// 删除DOM中所有段落
			$('p').click(function () {
				$(this).toggleClass('.off');
			});
			var p;
			$('button').click(function () {
				if(p) {
					p.appendTo('body');
					p = null;
					}else {
						p = $('p').detach();
					}
			});
```
2、 remove() 将匹配元素集合从DOM中删除（同时删除的还有元素上的事件以及jquery数据）

可以移除任何想要移除的元素

将所有的段落从DOM

```JS
			// 将所有段落从DOM中删除
			$('button').click(function () {
				$('p').remove();
			})
```

3、 empty() 从DOM中移除集合中匹配元素的所有子节点

这个方法不仅移除子元素和后代元素，同时移除元素里的文本
```js
		<p>hello</p>
		<p>you</p>
		<button>meimei</button>
		
		$('button').click(function () {
			$('p').empty();
		});
```
4、 unwrap() 将匹配元素集合的父级元素删除，保留自身（和兄弟元素，如果存在）在原来的位置

在每个段落外层加上一个div或者删除div

点击按钮添加或者删除样式

```js
		<p>hello</p>
		<p>you</p>
		<button>meimei</button>
		
			// 点击按钮给p的父级元素为demo样式的进行添加和删除操作
			var pTags = $('p');
			// 给button绑定事件
			$('button').click(function () {
				// 判断p的父级元素是否有demo样式
				// 若有则删除
				if(pTags.parent().is('.demo')) {
					pTags.unwrap();
				}
				// 若没有则包裹一个demo样式的div
				else{
					pTags.wrap('<div class = "demo"></div>');
				}
			});
```

DOM替换
1、 replaceAll()

用集合的匹配元素替换每个目标元素

.replaceAll(target)

```js
			// 将所有的p替换成demo
			$('button').click(function () {
				$('<div class = "demo">div</div>').replaceAll($('p'));
			})
```
2、 replaceAll()

用提供的内容替换集合中所有匹配的元素并且返回被删除元素的集合

.replaceWith()可以从dom中移除内容，也可以在这个地方插入新的内容

```js
			// 点击按钮的时候,用div替换按钮
			$('button').click(function () {
				// 用div替换当前的button
				$(this).replaceWith("<div class = 'demo'>" + $(this).text() + "</div>");
			})
```
### 事件

#### 浏览器事件

1、 .resize()

为js的resize事件绑定一个处理函数，或者触发元素上的该事件

例：当窗口大小改变时（改变后），查看窗口的宽度。

```js
			$(window).resize(function () {
				$('body').prepend('<div>' + $(window).width() + '</div>');
			})
```
2、 .scroll()

为js的scroll事件绑定一个处理函数，或者触发元素上的该事件

例：在页面滚动的时候触发一系列动作

```js
			$('p').clone().appendTo(document.body);
			$('p').clone().appendTo(document.body);
			$('p').clone().appendTo(document.body);
			$('p').clone().appendTo(document.body);
			$('p').clone().appendTo(document.body);
			$(window).scroll(function () {
				$('span').css({
					'display':'inline'
				}).fadeOut('slow');
			})
```

3、 文档加载(holdReady())

暂停或恢复，延迟就绪事件，直到已加载加载

```js
			$.holdReady(true);
			$.getScript(''),function () {
				$.holdReady(false);
			};
```
3、 ready()

当dom准备就绪的时候，指定一个函数来执行

例子：显示当dom加载的信息

```js
			$(document).ready(function () {
				$('p').text("the dom is")
			})
```

```js
			//当dom准备好了之后,就会绑定一个函数
			$(document).ready(function () {
				// 给button绑定一个函数,点击button,切换p的上滑与下滑 状态
				$('button').click(function () {
					$('p').slideToggle();
				});
			})
```
4、unload()

为js的unload事件绑定一个处理函数

例子：当离开页面时显示一个提示框

```js
			$(window).unload(function () {
				return "bye now";
			});
```
#### 事件绑定

1、 bind()

为一个元素绑定一个事件处理程序

bind的基本用法：在p上绑定一个点击事件

`
			$('p').bind('click', function () {
				alert('user clicked');
			})
			`
			
例子：为段落标签绑定单击事件

```js
		<p>ppp </p>
		<span></span>
		
			// 点击p将鼠标点击的位置写入span中
			// 鼠标移入和移出时改变class样式
			$('p').bind('click', function (event) {
				$('span').text('clicked:' + event.pageX + ',' +  event.pageY);
			})
			$('p').bind('mouseenter mouseleave', function (event) {
				$(this).toggleClass('demo');
			})
```

2、 delegate()

为所有匹配选择器的元素绑定一个或多个事件处理函数，基于一个指定的根元素的子集，匹配的元素包括那些目前已经匹配到的元素，也包括那些今后可能匹配到的元素。

例子：点击添加另外一个段落，__请注意__,delegate()绑定所有段落的click事件，甚至是新的段落。

```js
			// delegate()
			// 给p点击一个点击事件,每点击一次,就在前一个的后面加一个样式一样的p
			$('body').delegate('p', 'click', function () {
				$(this).after('<p>new paragraph</p>')
			});
```

3、 off()

移除一个事件处理函数

例子：移除click事件

```js
		<p>ppp </p>
		<p>移除之后</p>
		<button>移除</button>
		
			// ready(),当dom准备好了的时候,就加载背景颜色
			$(document).ready(function () {
				$('p').on('click', function () {
					$(this).css('background-color', 'pink');
				});
				// 点击button移除click事件之后,就没有事件被绑定
				$('button').click(function () {
					$('p').off('click');
				});
			})
```
4. one()

为元素的事件添加处理函数,处理函数在每个元素上每种事件类型最多执行一次

one()和on()是相同的,不同之处在于,对于给定的元素和事件类型,处理程序在第一次触发事件之后会被立即解除绑定

例子:点击任何一个段落,段落的字体大小只会改变一次

```js
			// 这里是one,所以这个事件只执行一次,点击效果只一次有效,如果是on绑定事件,正常状态可以点击多次实现效果
			$(document).ready(function () {
				$('p').one('click', function () {
					$(this).animate({
						fontSize: "+=6px"});
				});
			});
```

5. trigger()

trigger()和triggerHandle()不同的是:trigger会触发默认事件

根据绑定到匹配元素的给定的事件类型执行所有的处理程序和行为

```js
		<input type="text" value="文本">
		<button type="button">选中</button>
		
			// 点击button选中input框的文本
			$('input').ready(function () {
				$('button').click(function () {
					$('input').trigger('select');
				})
			})
```

6. triggerHandle()与trigger方法类似,不同的是trigger会触发事件的默认行为,例如表单的提交.

#### 表单事件

1. blur()

当元素失去焦点的时候发生blur事件,该方法通常和focus一起使用

```js
			// 当input失去焦点弹出一个提示框
			$(document).ready(function () {
				$('input').blur(function () {
					alert('失去了焦点');
				})
			})
```
2. focus()方法和blur()方法用法差不多

```js
			// 获取焦点的时候,显示提示字
			$(document).ready(function () {
				$('input').focus(function () {
					$('span').css({
						'display':'inline',
					}).fadeOut(2000);
				})
			})
```
3. change() 当元素的值改变时发生change事件(仅适用于表单字段)

当输入框的值发生改变的时候,按下enter键或者在点击输入框外部,会弹出一个提示框

```js
			$(document).ready(function () {
				$('input').change(function () {
					alert('文本已经被修改');
				})
			})
```
4. select()

为js的select事件绑定一个处理函数

例子:当输入框的文本被选中的时候,在div内显示文本
```js
			$(document).ready(function () {
				$('input').select(function () {
					$('div').text('select').show().fadeOut(2000)
				})
			})
```

5. submit()

当提交表单时,会发生submit事件,该方法只适用于form元素

```js
		<form action="505-事件冒泡.html" method="post">
			<input type="text">
			<input type="text">
			<input type="submit" value="提交"/>
		</form>
		
			$(document).ready(function () {
				$('form').submit(function () {
					alert('提交');
				});
			});
```

#### 键盘事件
1. keydown()和keyup()

与keydown事件相关的事件顺序
```bash
* keydown 键被按下的过程
* keypress 键被按下
* keyup 键被松开
```
例子:按下键盘输入的时候会改变输入框的颜色()
```js
			$(document).ready(function () {
				$('input').keydown(function () {
					$('input').css({
						'background-color':'red',
					});
				});
				$('input').keyup(function () {
					$('input').css({
						'background-color':'green',
					})
				})
			});
```
2. keypress()

例子:计算在input字段内按键次数

```js
			var i = 0;
			$(document).ready(function () {
				$('input').keypress(function () {
					$('span').text(i += 1);
				})
			})
```
####鼠标事件
1. click()单次点击 dblclick()双击

2.鼠标的相关事件
```js
			$(document).ready(function () {
				$('div').mousedown(function () {
					$(this).css({
						'border':'2px solid blue',
					});
				}).mouseout(function () {
					$(this).css({
						'border':'4px solid green',
					})
				}).mouseover(function () {
					$(this).css({
						'background':'pink',
					})
				}).mouseleave(function () {
					$(this).css({
						'background':'darkgrey',
					})
				}).mouseenter(function () {
					$(this).css({
						'background' :'red',
					})
				}).onmouseup(function () {
					$(this).css({
						'background' :'blue',
					})
				})
			})
```
3. mousemove()

```js
			// 获取鼠标移动的时候,鼠标在页面的位置
			$(document).ready(function () {
				$(document).mousemove(function (event) {
					$('span').text(event.pageX + ',' + event.pageY);
				});
			});
```
4. focusin()和focusout()

当元素或者在其内的任意元素,获得焦点时就会发生focusin事件

例: 当div元素或者其任意子元素获得焦点时,设置div元素的背景颜色
```js
			// focusin()和focusout
			$(document).ready(function () {
				$('nav.demo').focusin(function () {
					$(this).css({
						'background' : 'red',
					});
				});
				$('nav.demo').focusout(function () {
					$(this).css({
						'background' : '#90EE90',
					})
				})
			})
```

####事件对象

1、event.currentTarget

该属性是在事件冒泡阶段内的当前dom元素，通常等于this

```js
	$(document).ready(function () {
				$('button, div, p').click(function () {
					// 因为这里是三个等号,相当于判断,故输出的值hi一个布尔值,event.currentTarget等于this,所以返回true
					alert(event.currentTarget === this);
				});
			});
```
2、event.data()

包含当前执行的处理程序被绑定时传递到事件方法的可选数据

例：对每个p元素返回通过on方法传递的数据

这里还没懂

```js
			$(document).ready(function () {
				$('p').each(function (i) {
					$(this).on('click',{x:i},function (event) {
						// index从0开始的
						alert('num:' + $(this).index() + ',' + event.data.x);
					});
				});
			});
```
3、event.isDefaultPrevented()

检查指定的事件是否调用了preventDefault()

例子：防止链接打开url，并检查preventDefault是否被调用
```js
			$(document).ready(function () {
				$('nav').click(function(event) {
					event.preventDefault();
					// 如果被调用则会返回true
					alert('是否调用：'+ event.isDefaultPrevented());
				});
			});
```
4、 event.pageX和event.pageY

返回鼠标的位置，分别是相对于文档的左边缘和上边缘

例：获取鼠标的位置
```js
			$(document).ready(function () {
				$(document).mousemove(function (event) {
					$('nav').text("x:" + event.pageX  +"y:" + event.pageY);
				})
			})
```
5、 event.preventDefault()

阻止元素发生默认的行为：例如：当点击提交的时候阻止对表单的提交，阻止一下url的链接。

例子：防止链接打开url
```js
			$(document).ready(function () {
				$('a').click(function (event) {
					event.preventDefault();
				});
			});
```
5、event.which 返回指定事件上被按下的鼠标键或者按钮

例子：当你在以上输入框中输入内容时，div 中会陷入输入键的数字码。

```js
			$(document).ready(function () {
				$('input').keydown(function (event) {
					$('div').html('key:' + event.which);
				})
			})
```
### 效果

#### 基础
1、hide()和show()

隐藏被选的元素，与css3的display：none类似，隐藏的元素不会被完全显示，不影响布局

例子：点击按钮隐藏/显示所有的p元素

```js
		<p>隐藏/显示的段落</p>
		<button type="button" class = "btn1">隐藏</button>
		<button type="button" class = "btn2">显示</button>
		
			$(document).ready(function () {
				$('.btn1').click(function () {
					$('p').hide();
				});
				$('.btn2').click(function () {
					$('p').show();
				});
			})
```
2、 toggle()

toggle方法添加两个或者多个函数，以响应被选元素的click事件之间的切换

例子：点击p元素进行颜色切换

```js
		<button type="button" class="btn3">toggle</button>
		
			$('.btn3').click(function () {
				$('p').toggle(function () {
					$(this).css({
						'background':'red',
					});
				});
			})
```
#### 自定义

1、 animate()

该方法通过css样式将元素从一个状态改变为另外一个状态

__注意__:一般使用"+=" "-="创建相对动画

例子：通过改变元素的高度，对元素应用动画

```js
		<button type="button" class="btn4">增加高度</button>
		<button type="button" class="btn5">重置高度</button>
		<div></div>
		
			$(document).ready(function () {
				$('.btn4').click(function () {
					$('div').animate({
						'height': '300px',
					});
				});
				// 重置
				$('.btn5').click(function () {
					$('div').animate({
						'height': '150px',
					});
				});
			})
```
2、 delay()

对队列中的下一项执行的设置延迟

例子：隐藏再显示两个div，其中绿色的div在显示之前，有1秒的延迟

```js
		<button type="button" class="btn6">delay run</button>
		<div class="item1"></div>
		<div class="item2"></div>
		
	$(document).ready(function () {
				$('.btn6').click(function () {
					//slideUp(300),300毫秒后将div收起，800ms进入
					$('.item1').slideUp(300).fadeIn(800),
					$('.item2').slideUp(300).delay(1000).fadeIn(800);
				});
			});
```
3、dequeue()和queue() 
dequeue()方法从队列中移除下一个函数，然后执行函数，队列是一个或者多个等待运行的函数，通常和queue方法一起使用

queue()方法显示被选元素上要执行的函数队列

例：从队列中移除下一个函数，然后执行函数

注意：必须保证dequeue()方法在queue()添加的函数之内被调用，简单的说就是必须保证queue()函数内必须有dequeue()
```js
		<button type="button" class="btn7">run</button>
		<div class="item1"></div>
		
			$(document).ready(function () {
				$('.btn7').click(function () {
					var item1 = $('.item1');
					item1.animate({
						'height':'200',
						'width':'200',
					},'slow');
					//执行队列
					item1.queue(function () {
						//css改变可要可不要，但是dequeue()必须在queue()方法之内
						item1.css({
							'background' :' pink',
						});
						item1.dequeue();
					});
					item1.animate({
						'height':'100',
						'width':'100',
					},'slow');
				})
			})
```
4、 finish()

停止当前运行的动画，移除所有排队的动画，并为被选元素完成所有的动画

```js
		<button type="button" class="btn8">start</button>
		<button type="button" class="btn9">stop</button>
		<div class="item1"></div>
		
			$(document).ready(function () {
				$('.btn8').click(function () {
					$('.item1').animate({
						'height':'200'
					},2000);
					$('.item1').animate({
						'width':'200'
					},2000);
				});
				$('.btn9').click(function () {
					$('.item1').finish();
				});
			});
```
5、 stop()

被选元素停止当前正在运行的动画

原理和finish差不多，不同的是finish会停止当前执行的动画并完成整个动画的过程，而stop就相当于按了暂停键，停止当前动画，点击开始的时候会接着之前动画轨迹进行运动。

#### 渐变

1、 fadeIn 和 fadeOut

in是逐渐改变被选元素的不透明度，从隐藏到可见，即进入的过程

out是从可见到隐藏，即出去的过程

```js
		<button type="button" class="btn10">淡入</button>
		<button type="button" class="btn11">淡出</button>
		<br>
		<div class="item2"></div>
		
			$('.btn10').click(function () {
				$('.item2').fadeIn(1000);
			});
			$('.btn11').click(function () {
				$('.item2').fadeOut(1000);
			})
```
2、 fadeToggle()

可以在fadeIn和fedeOut之间切换，如果元素已经淡出，则元素会被添加上淡出的效果，反之一样。
```js
		<button type="button" class="btn12">淡入/淡出</button>
		<div class="item1"></div>
		
			// 点击按钮,会自动判断当前元素的淡入淡出状态
			$(document).ready(function () {
				$('.btn12').click(function () {
					$('.item1').fadeToggle(3000);
				})
			})
```
3、fadeTo()

允许渐变为给定的不透明度（0，1）

```js
		<button type="button" class="btn13">颜色变淡</button>
		<br>
		<div class="item2"></div>
		<div class="item1"></div>
		
			$(document).ready(function () {
				$('.btn13').click(function () {
					$('.item1').fadeTo('1000', 0.45);
					$('.item2').fadeTo('2000', 0.15);
				})
			})
```

#### 滑动

1、 slideDown()和slideUp()

down:以滑动的方式显示被选元素，放出展示

up:以滑动的方式隐藏被选元素，收起隐藏

```js
		<button type="button" class="btn14">隐藏</button>
		<button type="button" class="btn15">显示</button>
		<br>
		<div class="item1"></div>
		
			$(document).ready(function () {
				$('.btn14').click(function () {
					$('.item1').slideUp(2000);
				});
				$('.btn15').click(function () {
					$('.item1').slideDown(2000);
				});
			})
```
2、slideToggle()

在被选元素上进行slideUp和slideDown之间进行切换

```js
		<button type="button" class="btn16">隐藏/显示</button>
		
			$(document).ready(function () {
				$('.btn16').click(function () {
					$('.item1').slideToggle(1000);
				});
			});
```




