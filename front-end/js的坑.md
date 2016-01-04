## js的坑
* 坚持使用`===`替代`==`
* `NaN`与其它值都不等 `NaN === NaN; // false`
	* 唯一能判断NaN的方法是通过isNaN()函数：    
		`isNaN(NaN); // true`
	* 注意浮点数比较 `1 / 3 === (1 - 2 / 3); // false`
* 启用严格模式`'use strict';` 	
* ES新增多行字符串\`...\`（markdown一致）
### 数组
* 要取得Array的长度，直接访问`length`属性
	* 请注意，直接给Array的length赋一个新的值会导致Array大小的变化：      
	
  ``` javascript
  	var arr = [1, 2, 3];
	arr.length; // 3
	arr.length = 6;
	arr; // arr变为[1, 2, 3, undefined, undefined, undefined]
  ```
  
	* 请注意，如果通过索引赋值时，索引超过了范围，同样会引起Array大小的变化：

	``` javascript
		var arr = [1, 2, 3];
		arr[5] = 'x';
		arr; // arr变为[1, 2, 3, undefined, undefined, 'x']
	```
* slice()就是对应String的substring()版本
	* 如果不给slice()传递任何参数，它就会从头到尾截取所有元素。利用这一点，我们可以很容易地复制一个Array：
	`var aCopy = arr.slice();`
	
### 对象
* ` delete xiaoming.age;` // 删除age属性
* 如果我们要检测xiaoming是否拥有某一属性，可以用in操作符：
	* `'name' in xiaoming; // true`
* 排除继承的属性`xiaoming.hasOwnProperty('name'); // true`

### 函数
* `arguments `用于接收函数传入的所有参数，类似于array
* `rest` 函数额外的参数数组(ES6)
* 
``` javascript
function foo() {
    var x = 'Hello, ' + y;
    alert(x); //hello, undefined
    var y = 'Bob'; //变量声明会被默认提升到函数顶部，但赋值动作不会变位置。
}
```

* let 定义变量（ES6），块级作用域
	* var 作用域为函数
* const 定义常量（ES6），块级作用域


* 名字空间,用来减少冲突

``` javascript
// 唯一的全局变量MYAPP:
var MYAPP = {};

// 其他变量:
MYAPP.name = 'myapp';
MYAPP.version = 1.0;

// 其他函数:
MYAPP.foo = function () {
    return 'foo';
};
```
* 可以用函数本身的apply方法，它接收两个参数，第一个参数就是需要绑定的this变量，第二个参数是Array，表示函数本身的参数。
	* `getAge.apply(xiaoming, []); // 25, this指向xiaoming, 参数为空`

### 高阶函数
* `map` 将一个函数应用到所有对象
	* 把array转换成String
	
	``` javascript
	var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
	arr.map(String);
	```
* reduce	
	* `[x1, x2, x3, x4].reduce(f) === f(f(f(x1, x2), x3), x4)`

	``` javascript
		//求数组的和
		var arr = [1, 3, 5, 7, 9];
		arr.reduce(function (x, y) {
		    return x + y;
		});
	```
* filter() 根据返回值删除某些元素
* sort() 排序算法，返回`-1``0``1`来排序

### 闭包
* 返回闭包时牢记的一点就是：返回函数不要引用任何循环变量，或者后续会发生变化的变量。

``` javascript
function count() {
    var arr = [];
    for (var i=1; i<=3; i++) {
        arr.push(function () {
            return i * i;
        });
    }
    return arr;
}

var results = count();
var f1 = results[0]; //16
var f2 = results[1]; //16
var f3 = results[2]; //16
```

### 箭头函数

``` javascript
var obj = {
    birth: 1990,
    getAge: function (year) {
        var b = this.birth; // 1990
        var fn = (y) => y - this.birth; // this.birth仍是1990
        return fn.call({birth:2000}, year);
    }
};
obj.getAge(2015); // 25
```


### generator
* yield

``` javascript
	//返回每次返回比之前多1的数字
	var x = 1;
	while(true){
		yield x++;
	}

```

## 标准对象
### 包装对象

``` javascript
var n = new Number(123); // 123,生成了新的包装类型
var b = new Boolean(true); // true,生成了新的包装类型
var s = new String('str'); // 'str',生成了新的包装类型
```

* 不要使用new Number()、new Boolean()、new String()创建包装对象；
* 用parseInt()或parseFloat()来转换任意类型到number；
* 用String()来转换任意类型到string，或者直接调用某个对象的toString()方法；
* 判断Array要使用Array.isArray(arr)；
* 判断null请使用myVar === null；
* 判断某个全局变量是否存在用typeof window.myVar === 'undefined'；
* 函数内部判断某个变量是否存在用typeof myVar === 'undefined'。
* number 调用toString方法
	* `123..toString(); // '123', 注意是两个点！`

### Date

``` javascript
var now = new Date();
now; // Wed Jun 24 2015 19:49:22 GMT+0800 (CST)
now.getFullYear(); // 2015, 年份
now.getMonth(); // 5, 月份，注意月份范围是0~11，5表示六月
now.getDate(); // 24, 表示24号
now.getDay(); // 3, 表示星期三
now.getHours(); // 19, 24小时制
now.getMinutes(); // 49, 分钟
now.getSeconds(); // 22, 秒
now.getMilliseconds(); // 875, 毫秒数
now.getTime(); // 1435146562875, 以number形式表示的时间戳
```

* 创建指定日期    
	* `var d = new Date(2015, 5, 19, 20, 15, 30, 123);`
	
	*  ISO 8601格式
	
		``` javascript
			var d = Date.parse('2015-06-24T19:49:22.875+08:00');   
			var d = new Date(1435146562875);
		```
### RegExp
* 创建正则表达式

``` javascript
var re1 = /ABC\-001/;
var re2 = new RegExp('ABC\\-001');

re1; // /ABC\-001/
re2; // /ABC\-001/
```	

### JSON
* `JSON.stringify()`
* `JSON.parse()`

## 面向对象编程
* 按照约定要对象函数的首字母应该大写，这样`jslint`等工具可以检测出未写new的错误。
* 继承

``` javascript
function inherits(Child, Parent) {
    var F = function () {};
    F.prototype = Parent.prototype;
    Child.prototype = new F();
    Child.prototype.constructor = Child;
}
```

## 浏览器
* windows
	* window.innerWidth //净宽度
	* window.innerHeight 
* navigator //这些信息可以被修改
	* navigator.appName：浏览器名称；
	* navigator.appVersion：浏览器版本；
	* navigator.language：浏览器设置的语言；
	* navigator.platform：操作系统类型；
	* navigator.userAgent：浏览器设定的User-Agent字符串。
* screen 屏幕信息
* location URL信息

	``` javascript
	location.href; //http://www.example.com:8080/path/index.html?a=1&b=2#TOP
	location.protocol; // 'http'
	location.host; // 'www.example.com'
	location.port; // '8080'
	location.pathname; // '/path/index.html'
	location.search; // '?a=1&b=2'
	location.hash; // 'TOP'
	```
	
	* 要加载一个新页面，可以调用location.assign()。
	* 如果要重新加载当前页面，调用location.reload()
* document document对象就是整个DOM树的根节点。
	* Cookie    
	服务器在设置Cookie时可以使用httpOnly，设定了httpOnly的Cookie将不能被JavaScript读取。
* history	
	* JavaScript可以调用history对象的back()或forward ()
	* 这个对象属于历史遗留对象,任何情况，你都不应该使用history这个对象了。

### DOM
* 更新DOM
	* innerHTML `p.innerHTML = 'ABC <span style="color:red">RED</span> XYZ';`
	* textContent innerText

### AJAX
* ajax XMLHttpRequest
* jsonp 通过script标签请求
* CORS 使用XMLHttpRequest，要求服务器设置`Access-Control-Allow-Origin`

### Promise