### jquery核心

#### jquery对象

1、jquery()

返回匹配的元素集合，无论是通过在dom的基础上传递参数还说创建一个html字符串

例：查找所有的div下的p元素，并为它们加上边框

```js
		<p>one</p>
		<div>
			<p>two</p>
		</div>
		<p>three</p>
		<script type="text/javascript">
			$("div > p").css({
				"border": "1px solid gray",
			});
		</script>
```
2、jquery.noConflict()

放弃jquery控制$变量

例：将$引用的对象映射回原始的对象

```js
			jQuery.noConflict();
			jQuery("div p").hide();
			$("content").style.display = "none";
```
3、jquery提供一种方法来执行0个或者多个对象的回调函数
```js
			$(function () {
				$.when({
					tetsing: 123
				}).done({
					function(x){
						alert(x.testing);
					}
				});
			})
```
#### 实用工具
1、jquery.contains()检查一个dom元素是另一个dom元素的后代

如果第二个参数所提供的dom元素是第一个参数dom元素的后裔，那么$.contains()返回true，无论是直接的子元素或者是后代元素，否则返回false
```js
			$(function () {
				$.contains(document.documentElement, document.body); //true
				$.contains(document.body, document.documentElement);//false
			})
```
2、jquery.each()

遍历数组元素

```js
			$(function () {
				$.each([52, 97], function (index, value) {
					alert(index + ":" + value);
				});
			})
```
3、 jQuery.extend()

遍历数组元素，并修改第一个对象

```js
			$(function () {
				var object1 = {
					apple: 0,
					banana: {
						weight: 52,
						price: 100,
					},
					cherry: 97,
				};
				var object2 = {
					banana:{
						price: 200,
					},
					durian: 100,
				};
				// object2合并到object1中
				$.extend(object1, object2);
				var printObj = typeof JSON != "undefined" ? JSON.stringify : function(obj) {
					var arr = [];
					$.each(obj, function(key, val) {
						var next = key + ":";
						next += $.isPlainBoject(val) ? printObj(val) : val;
						arr.push(next);
					});
					return "{" + arr.join(",") + "}";
				};
				$(".log").append(printObj(object1));
			});
```
运行结果：{"apple":0,"banana":{"price":200},"cherry":97,"durian":100}

4、jquery.globalEval()在全局上下文下执行一些js代码

```js
			function test() {
				jQuery.globalEval("var newVar = true;")
			}
			test();
```
5、jquery.grep()

查找满足过滤函数的数组元素，原始数组不受影响

```js
			var arr = [1,2,3,4,5,6,7,8,8,9,3,45,56,65,47,76,75];
			$("div").text(arr.join(", "));
			arr = jQuery.grep(arr, function (n, i) {
				return (n != 5 && i > 4);
			});
			$("p").text(arr.join(", "));
			arr = jQuery.grep(arr, function (a) {
				return a != 9;
			});
			$("span").text(arr.join(", "));
```
6、jquery.inArray()

在数组中查找指定值并返回它的索引（如果没有找到，则返回-1）

```js
			$(function () {
				var arr = [4, "peter", 8, "john"];
				var $spans = $("span");
				$spans.eq(0).text(jQuery.inArray("john", arr));
				$spans.eq(1).text(jQuery.inArray(4, arr));
				$spans.eq(2).text(jQuery.inArray("kali", arr));
				$spans.eq(3).text(jQuery.inArray("tom", arr, 2));
			})
```
输出显示3 0 -1 -1

7、isArray() 确定的参数是一个数组

例：查找参数是否为数组

```js
		是数组吗？<b></b>
		
			// 在"+"加号前面加冒号是为了将后面的判断结果变成字符串
			$("b").append("" + $.isArray([]));
```
输出结果为：true

8、jquery.isEmptyObject()

检查对象是否为空（不包含任何属性）

```js
			$(function () {
				function fun(html) {
					document.body.innerHTML += "<br>" + html;
				}
				fun($.isEmptyObject({}));  //true
				fun($.isEmptyObject({
					foo: "bar" //false
				}));
			});
```
9、jquery.isPlainObject()

测试对象是否是纯粹的对象（通过“{}”或者“new Object"创建的)

```js
			console.log(jQuery.isPlainObject({}));  //true
			console.log(jQuery.isPlainObject("test"));  //false
```
10、jquery.makeArray()

转换一个类似数组的对象成为真正的js数组

```js
		<div>first</div>
		<div>second</div>
		<div>third</div>
		<div>fourth</div>
		
			var elems = $("div");
			var arr = jQuery.makeArray(elems);
			// 颠倒数组中元素的顺序
			arr.reverse();
			$(arr).appendTo(document.body);
```

11、jquery.map()

将一个数组中的所有元素转换到另一个数组中

```js
		<div></div>
		<p></p>
		<span></span>
		
			var arr = ["a", "b", "c", "d", "e"];
			// join()把数组中所有的元素转换成一个字符串
			$("div").text(arr.join(", "));
			arr = jQuery.map(arr, function (n, i) {
				return (n.toUpperCase() + i);
			});
			$("p").text(arr.join(", "));
			arr = jQuery.map(arr ,function (a) {
				return a + a;
			});
			$("span").text(arr.join(", "));
```
12、jquery.merge()

合并两个数组内容到第一个数组

例：合并两个数组，修改第一个参数的内容

$.merge([0,1,2],[2,3,4])

结果：[0,1,2,2,3,4]

```js
			var first = ['a', 'b', 'c'];
			var second = ['d', 'e', 'f'];
			console.log($.merge($.merge([],first), second));
```
得到的结果：["a","b","c","d","e","f"] 

13、jquery.now()返回一个数字，表示当前时间

是表达式(new Date).getTime()返回数值的一个简写

```
			$(function () {
				document.body.innerHTML = $.now();
			})
			```
14、jquery.parseHTML()

将字符串解析到一个dom节点的数组中

例：使用一个html字符创建一个数组的dom节点，并将它插入到一个div

```js
			$(document).ready(function () {
				var $log = $(".log");
					str = "<b>name:</b> mei",
					html = $.parseHTML(str),
					nodeNames = [];
				// 添加已经解析的html
				$log.append(html);
				// 集合已经解析的html的节点名称
				$.each(html, function (i, elem) {
					nodeNames[i] = "<li>" + elem.nodeName + "</li>";
				});
				// 插入节点名
				$log.append("<h3>nodeNames:</h3>");
				$("<ol></ol>").append(nodeNames.join("")).appendTo($log);
			})
```

```bash
输出结果：content:
name: mei
nodeNames:
1.B
2.#text
```
15、jquery.parseJSON()

接受一个标准格式的json字符串 并返回解析后的js值

```js
			var obj = jQuery.parseJSON('{
				"name": "mei"
			}');
			alert(obj.name) === "mei";
```
弹出 true

16、proxy()
接受一个函数，然后返回一个新函数，并且这个新函数始终保持了特定的上下文语境

例：通过调用参数为“context，function name"的jquery.proxy()方法，强制修改函数的上下文语境，并且在第一次点击事件执行之后，解除绑定

```js
		<p><button class="test">test</button></p>
		<p class="log"></p>
		
			var obj = {
				name: "mei",
				test: function () {
					$(".log").append(this.name);
					$(".test").off("click", obj.test);
				}
			};
			// 接收了一个click函数,又接收了一个新的proxy函数
			$(".test").on("click", jQuery.proxy(obj, "test"));
```
17、jquery.trim()

去掉字符串起始和结尾的空格

例：删除在开始和在字符串的末尾的两个空格
```js
		<pre class="original"></pre>
		<pre class="trimmed"></pre>
		
			var str = "     meimeimei    ";
			$(".original").html("original(原始): " + str + "");
			$(".trimmed").html("trimmed（去掉空格后）: " + $.trim(str) + "");
```
18、jquery.type()

确定js对象的类型

例：判断该参数是否是一个正则表达式

```js
		这是一个正则表达式？<b></b>
		
			$(function () {
				$("b").append("" + jQuery.type(/test/));
			});
```
返回输出：这是一个正则表达式？regexp

19、jquery.unique()

排序一个dom元素的数组，恰当的出去重复项，请注意，这仅适用于dom元素数组，而

\____不能处理字符串或者数字数组__

```js
			// $(function() {
			// 	//unique() 必须获取一个原始数据
			// 	var divs = $("div").get();
			// 	// 添加三个div块元素
			// 	// concat方法用于连接两个或者多个字符串
			// 	divs = divs.concat($(".dup").get());
			// 	$("div:eq(1)").text("重排序后有 " + divs.length + " 个元素");
			// 	divs = jQuery.unique(divs);
			// 	$("div:eq(2)").text("重排序后有 " + divs.length + " 个元素").css("color", "red");
			// })
```

#### dom元素方法
1、.get()
通过检索匹配jquery对象得到对应的dom元素

例：如果指定了index参数，get会获取单个元素

```js
		<div>document中又6个div块</div>
		<div></div>
		<div class="dup"></div>
		
			console.log($("div").get(2));
```
输出得到的是第三个div

例：点击元素，显示标签名

```js
			div {
				width: 200px;
				height: 50px;
				border: 2px solid salmon;
			}
			input{
				margin: 8px;
				border: 2px solid #90EE90;
			}
			
		<span> </span>
		<div><input type="text"></div>
		
			$("*", document.body).click(function (e) {
				// 阻止冒泡事件
				e.stopPropagation();
				var dom = $(this).get(0);
				$("span").text("" + dom.tagName);
			})
```
2、 index() 从匹配的元素中搜索给定元素的索引值，从0开始

例：返回class为foo的索引值

```js
		<div class = "bar"></div>
		<div class = "foo"></div>
		<div class = "nav"></div>
		<p></p>
		
			$(function () {
				var $foo = $(".foo");
				$("p").html('index:' + $("div").index($foo));
			})
```
输出结果为：index:1

3、.size() 
```bash
__.size()已经被废弃了，用.length__
```
返回jquery对象匹配的dom元素的数量

例：统计div的个数，点击时添加一个div
```js
		<span></span>
		<div></div>
		
			$(document.body).click(function () {
				$(this).append($("<div>"));
				var n = $("div").length;
				$('span').text("there are " + n + " divs, click to add more");
			}).click();
```
4、 toArray()

返回一个包含jquery对象集合中的所有dom元素的数组

例：选择文档中所有的div，并且返回一个dom元素数组，然后利用浏览器内置的reverse方法反转整个数组

```js

```


