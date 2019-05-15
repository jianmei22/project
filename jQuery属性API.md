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








