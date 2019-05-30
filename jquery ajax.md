### Ajax

#### 全局ajax事件处理程序

1、ajaxComplete()

是ajax请求完成时运行的函数

例：ajax请求完成后显示 completed 的指示

```js
			$(document).reday(function() {
				$(document).ajaxComplete(function(event, request, settings) {
					$('.item1').append('completed');
				});
			});
```
2、ajaxError()

例：当ajax请求失败时，触发一个警告框

```js
			$(document).reday(function() {
				$(document).ajaxError(function() {
					alert('error');
				});
			});
```
3.ajaxSend()
在ajax请求发送之前绑定一个要执行的函数

```js
			// 当ajax请求即将发送前显示一个信息
			$(document).ajaxSend(function (event, request, settings) {
			$('.log').append('<li>' + settings.url + '</li>');	
			});
```
4、ajaxStart()在ajax请求刚开始的时候执行一个处理函数

```js
			// 当ajax请求开始发送时显示一个信息(没有一个ajax请求时已经激活的)
			$(document).ajaxStart(function () {
				$('.log').show();
			})
			```
5、ajaxStop()
```js
			// 在ajax请求完成时执行一个处理函数
			// 在ajax请求停止后隐藏加载信息
			$(document).ajaxStop(function () {
				$('.log').hide();
			})
```
6、ajaxSuccess()

```js
			// 绑定一个函数当ajax请求完成时执行
			
			// 当ajax请求成功之后,显示一个信息
			$(document).ajaxSuccess(function (event, request, settings) {
				$('.log').append('<li>' + settings.url + '</li>');
			});
```
#### 辅助函数
1、jquery.param()

创建一个数组，一个普通的对象，或者一个jquery对象的序列化表示·形式，用于url查询字符串或者ajax请求，如果传递一个jquery对象传递，应该包含输入元素

例子：序列号一个value对象

```js
			var params = {
				width:1680,
				height:1050
			};
			var str = jQuery.param(params);
			$('.log').text(str);
```
2、serialize()

将用作提交的表单元素的值编译成字符串

例子：序列化表单
```js
		<div class="log"></div>
		<form action="">
			第一个名称：<input type="text" name="fn" value="jian">
			最后一个名称：<input type="text" name="ln" value="mei">
		</form>
		<button type="button">序列化列表</button>
		
			$(document).ready(function () {
				$('button').click(function () {
					$('div').text($('form').serialize());
				});
			})
			//得到的是：fn=jian&ln=mei
```

3、serializeArray()

将用作提交的表单元素的值编译成拥有name和value对象组成的数组

例子:序列化表单

```js
		<form action="">
			第一个名称：<input type="text" name="fn" value="jian">
			最后一个名称：<input type="text" name="ln" value="mei">
		</form>
		<button>序列化表单值</button>
		<div class="log"></div>
		
			$(document).ready(function() {
				$('button').click(function() {
					x = $("form").serializeArray();
					$.each(x, function(i, field) {
						$(".log").append(filed.name + ":" + field.value + " ");
					});
				});
			});
```
#### 底层接口

jquery.ajax()

执行一个异步的http（ajax）的请求

例子：载入并执行一个js文件

```js
			$.ajax({
				method: "GET",
				url: "index.js",
				dataType: "script",
			});
```
例子：保存数据到服务器，成功时显示信息

```js
			$.ajax({
				method: "POST",
				url: "some.php",
				data: {
					name: "mary",
					location: "weston",
				}
			}).done(function(msg) {
				alert('data saved' + msg);
			});
```
例子：装入一个html网页最新版本
```js
			$.ajax({
				url: "index.html",
				cache: false
			}).done(function (html) {
				$(".log").append(html);
			})
```
jquery.ajaxSetup()

为以后要用到的ajax请求设置默认的值

例子：设置ajax请求默认地址为”/xmlhttp/",禁止触发全局ajax事件，用post代替默认get方法，其后的ajax请求不再设置任何选项参数
```js
			$.ajaxSetup({
				url: "/xmlhttp",
				global: false,
				type: "POST"
			});
			$.ajax({
				data: myData
			});
```

#### 快捷方法

1、jquery.get()

使用一个http get请求从服务器加载数据

例：请求test.php页面，但是忽略返回结果

$.get("test.php");

例：请求test.php页面，并且发送url参数（虽然仍然忽视返回的结果）

$.get("test.php",{
	name: "john",
	time: "2pm"
})

2、jquery.getJSON()

使用一个http get请求从服务器加载json编码的数据

这是一个ajax函数的缩写，相当于：

```js
			$.ajax({
				dataType: "json",
				url: url,
				data: data,
				success: success
			});
```
例子：获取json数据

```js
			$(document).ready(function () {
				$("button").click(function () {
					$.getJSON("demo_ajax_json.js", function (result){
						$.each(result, function (i, field) {
							$("div").append(field + " ");
						});
					});
				});
			});
```
3、jquery.post()

使用一个http post请求从服务器加载数据

这也是ajax函数的简写形式，相当于

```js
			$.ajax({
				dataType: "POST",
				url: url,
				data: data,
				success: success
			});
```
使用方式跟get类似

4、jquery.getScript()

使用一个http get请求从服务器加载并执行一个js文件

这是ajax的一个简写形式，相当于：

```js
			$.ajax({
				url: url,
				dataType: "script",
				success: success
			});
```
5、.load() 

从服务器载入数据并且将返回的html代码并插入至匹配的元素中

例：在一个有序列表中，加载主页的页脚导航

```js
		<b>project</b>
		<ol class="new-project"></ol>
		
			$('new-project').load("/resouces/load.html .project li")
```