## jQuery
### 选择器 
* `find()` 在子类中查找
* `parent()`父类中查找
* `next()` `nextAll()` `prev()`  `siblings()`同级操作
* `filter()` 过滤掉

	``` javascript
		var langs = $('ul.lang li'); 
	langs.filter(function () {
	    return this.innerHTML.indexOf('S') === 0; // 返回S开头的节点
	}); 
	
	``` 

* map()方法把一个jQuery对象包含的若干DOM节点转化为其他对象：

``` javascript
var langs = $('ul.lang li'); // 拿到JavaScript, Python, Swift, Scheme和Haskell
var arr = langs.map(function () {
    return this.innerHTML;
}).get(); // 用get()拿到包含string的Array：['JavaScript', 'Python', 'Swift', 'Scheme', 'Haskell']

```

* first()、last()和slice()方法可以返回一个新的jQuery对象
``` javascript
var langs = $('ul.lang li'); // 拿到JavaScript, Python, Swift, Scheme和Haskell
var js = langs.first(); // JavaScript，相当于$('ul.lang li:first-child')
var haskell = langs.last(); // Haskell, 相当于$('ul.lang li:last-child')
var sub = langs.slice(2, 4); // Swift, Scheme, 参数和数组的slice()方法一致
```

### 基本过滤器
* `:not(selector)` 排除
* `:even` 偶数
* `:odd` 奇数
* `:eq(index)` 等于
* `:gt()` 大于 `:lt()` 小于
* `:header` h1~h6
* `:animated` 动画
* `:focus` 焦点
	
### 内容过滤器
* `：contains(text)` 包含文本
* `:empty` 没有子元素和文本
* `:has(selector)`
* `:parent`
* 可见性
	* `:hidden` 不可见
	* `:visible` 可见

## DOM操作
* `text()``html()`获取文本和原始html,jQuery的方法会作用在每个节点上。

	``` javascript
	j1.html('<span style="color: red">JavaScript</span>');
	j2.text('JavaScript & ECMAScript');
	```

* `css('name', 'value')`修改css
* `class`

	``` javascript
	div.hasClass('highlight'); // false， class是否包含highlight
	div.addClass('highlight'); // 添加highlight这个class
	div.removeClass('highlight'); // 删除highlight这个class
	```

* `show()`和`hide()`//不删除dom
* `width()` `height()`
* `attr()`和`removeAttr()`方法用于操作DOM节点的属性：
	* attr()和prop()对于属性checked处理有所不同：
	
	``` javascript
	var radio = $('#test-radio');
	radio.attr('checked'); // 'checked'
	radio.prop('checked'); // true
	radio.is(':checked'); 
	```
* jQuery对象统一提供`val()`方法获取和设置对应的value属性
* append() 添加dom到最后
	* 添加节点`ul.append('<li><span>Haskell</span></li>');`
* prepend()	添加dom到最前
* 同级节点可以用after()或者before()方法。
	> 以上dom操作会删除原来位置的dom
* remove()
* detach() //删除DOM但会保留jqurey中的配置
* `empty()` 清空节点
* `clone`
* `replaceWith()` 替换
* `wrap()`包裹节点
* 切换样式 toggle(); toggleClasss();

## 事件
### 鼠标事件
* `click`:
* `dblclick`: 双击
* `mouseenter` 鼠标进入
* `mouseleave ` 鼠标移出
* `mousemove` 鼠标移动
* `hover` 鼠标进入和退出

### 键盘
* `keydown`
* `keyup`
* `keypress` 

### 其它 
* `focus` 获得焦点
* `blur` 失去焦点
* `change` 内容变化
* `submit` 提交
* `ready` 页面载入
	* 简化写法，页面载入后调用
	
		``` javascript
		$(function(){
		...
		});
	```

### 参数
* 所有方法都会传入event参数
	* `event.pageX`  `event.pageY`
	* `event.stopPropagation()` 停止事件冒泡
	* `event.preventDefault()` 屏蔽默认行为
	* 在函数中返回flase相当于同时调用上面两个方法
	* `event.target` //获取触发事件的元素
	* `event.which` //1，2，3鼠标左中右
* `off(‘'click'’,func)` 移除所有绑定的函数
* `one()` 执行一次的函数回调
* `trigger('myClick',[参数])` //调用自定义方法
* 调用无参数的方法可以触发事件
	* `input.change()`相当于`input.trigger('change')`，它是trigger()方法的简写。

* 浏览器安全限制
	* 某些方法只用用户触发才有效，如`window.open()`

		``` javascript
		//可以执行
		button1.click(function () {
		    popupTestWindow();
		});
		//不立刻执行的方法会被拦截
		button2.click(function () {
		    // 不立刻执行popupTestWindow()，100毫秒后执行:
		    setTimeout(popupTestWindow, 100);
		});
				
		```
		
## 动画
> slow 0.6s fast0.2s  normal 0.4s

* `hide` `show` 
* `slideUp` `slideDown``slideToggle('slow')` //上下逐渐消失
* fadeOut('slow')  fadeIn('slow')  fadeToggle('slow')//渐隐渐现
* animate() 自定义动画，

	``` javascript
	div.animate({
	    opacity: 0.25,
	    width: '256px',
	    height: '256px'
	    left: '+=50px' //当前位置累计500px
	}, 3000，fun); //3秒到设定值 执行完调用的方法
	
	```
	
* `stop(clearQueue,gotoEnd)` //是否情况动画队列，是否跳到末状态
* `is(:animated)` //是否处于动画状态
* `delay(1000)`延迟

## ajax
* `ajax(url, settings)`
	* settings 对象
		* async：是否异步执行AJAX请求，默认为true，千万不要指定为false；
		* method：发送的Method，缺省为'GET'，可指定为'POST'、'PUT'等；
		* contentType：发送POST请求的格式，默认值为'application/x-www-form-urlencoded; charset=UTF-8'，也可以指定为text/plain、application/json；
		* data：发送的数据，可以是字符串、数组或object。如果是GET请求，data将被转换成query附加到URL上，如果是POST请求，根据contentType把data序列化成合适的格式；
		* headers：发送的额外的HTTP头，必须是一个object；
		* dataType：接收的数据格式，可以指定为'html'、'xml'、'json'、'text'等，缺省情况下根据响应的Content-Type猜测。

	``` javascript
	var jqxhr = $.ajax('/api/categories', {
	    dataType: 'json'
	}).done(function (data) {
	    ajaxLog('成功, 收到的数据: ' + JSON.stringify(data));
	}).fail(function (xhr, status) {
	    ajaxLog('失败: ' + xhr.status + ', 原因: ' + status);
	}).always(function () {
	    ajaxLog('请求完成: 无论成功或失败都会调用');
	});
	
	```

* get
		
	``` javascript
	var jqxhr = $.get('/path/to/resource', {
    name: 'Bob Lee',
    check: 1
	});
	
	```
	
	* 第二个参数如果是object，jQuery自动把它变成query string然后加到URL后面，实际的URL是：`/path/to/resource?name=Bob%20Lee&check=1`

* post
* getJSON //返回的数据直接被解析

## 插件
1. 给`$.fn`绑定函数，实现插件的代码逻辑；
2. 插件函数最后要`return this;`以支持链式调用；
3. 插件函数要有默认值，绑定在`$.fn.<pluginName>.defaults`上；
4. 用户在调用时可传入设定值以便覆盖默认值。