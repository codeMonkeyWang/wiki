## javascript&HTML5
### 基本语法
* string
	* indexOf(“word”) //检索某个字符串
* undefined //未赋值
* var tempArr = [1,2,3,4];
* 对象 

``` javascript
var fido = {
	name: "Fido",
	weight: 40
}

fido.age = 5; //增加属性
delete fido.age //删除属性
```

* new

``` javascript
function User(name, uri) {	this.name = name;	this.uri = uri;	this.display = function() {		console.log(this.name);	}}

var someuser = new User('byvoid', 'http://www.byvoid.com');
``` 

* 定时器 setInterval
	* clearInterval //取消定时器
### UI
* alert("test"); //提示框

### DOM
* getElementById("test");
* document.querySelector("div>p"); //使用选择器来获取元素
	*  `document.querySelectorAll("");`
* test.innerHTML();
* createElement("li"); //创建一个li
	* head.appendChild(newScriptElement);
	* head.replaceChild(newScriptElement, oldScriptElement);
* window.onload = init; //页面加载完调用方法
* `var controlLinks = document.querySelectorAll("a.control");`

### 数学
* Math.random(); //0~1的随机数
* Math.floor(1.23); //去除小数

### 地理定位
* degreesToDecimal(degrees,minutes,seconds) //度分秒转换为小数
* getCurrentPosition()
	* Position
		* coords //经纬度
			* latitude //纬度
			* longitude//经度
			* accuracy//精确度
		* timestamp //创建时间
* watchPosition()
* clearWatch()

### 网络
### JSON
* `JSON.parse(responseText);`
* `JSON.stringify("string");` //生成json
* jsonP

### canvas

``` javascript
	var canvas = document.getElementById("myCanvas");
	var context = canvas.getContext("2d");
```

### Video
* `video.canPlayType("video/mp4") != ""` //“” maybe probably
	* 只有当类型中包含codec 参数时浏览器才会有比maybe更大的信心

### 本地存储
* `localStorage.setItem();`
* `localStorage.getItem();`

### 线程
* 线程无法更新DOM
* worker.terminate();//终止线程 可以从内部调用close()终止

``` javascript
var worker = new Worker("worker.js");
worker.postMessage("ping");

worker.onmessage = function(event) {
	var message = "Worker " + " says " + event.data;
	document.getElementById("output").innerHTML = message;
}
worker.onerror = function(error) {
	document.getElementById("output").innerHTML =
		"There was an error in " + error.filename + 
		" at line number " + error.lineno +
		": " + error.message;
};

```

* `worker.js`

``` javascript
onmessage = pingpong;

function pingpong(event) {
	if (event.data == "ping") {
		postMessage("pong");
	}
	else {
		// intentionally make an error!
		1/x;
	}
}

```

* 子线程也可以再创建子线程
* 子线程中可以使用`importScripts()`来利用JSONP
* 线程可以使用XMLHttpReques和本地存储

## 其它主题
* Modernizr 提供统一的接口来检测浏览器的支持。
	* `if(Modernizr.geoLocation)...`
	* `if(Modernizr.localstorage)...`
	* if(Modernizr.video)...