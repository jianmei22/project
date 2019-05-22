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



