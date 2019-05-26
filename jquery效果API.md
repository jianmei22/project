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