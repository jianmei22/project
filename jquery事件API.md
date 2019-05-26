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