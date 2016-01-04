## ECMAScript 6

### let和const
* let
	* let 只在代码块中有效，和主流语言保持一致
	* let不存在变量提升，如果let在一个方法下面的代码行定义，就不可用。
	* let不允许重复声明（var语句重复声明语句是合法且无害的）
	* 实际上使得获得广泛应用的立即执行匿名函数（IIFE）不再必要了。
	
	```java
		// IIFE写法		(function () {			var tmp = ...;			...		}());		// 块级作用域写法		{			let tmp = ...;			...
		}
		
	```
	
	``` javascript
		function f() { console.log('I am outside!'); }		(function () {			if(false) {			// 重复声明一次函数f			function f() { console.log('I am inside!'); }			}			f();		}());
	
	```
	> 上面代码在ES5中运行，会得到“I am inside!”，但是在ES6中运行，会得到“I am outside!”。这是因为ES5存在函数提升，不管会不会进入if代码块，函数声明都会提升到当前作用域的顶部，得到执行；而ES6支持块级作用域，不管会不会进入if代码块，其内部声明的函数皆不会影响到作用域的外部。


	>需要注意的是，如果在严格模式下，函数只能在顶层作用域和函数内声明，其他情况（比如if代码块、循环代码块）的声明都会报错。

* const命令
	* 用来声明常量

	
### 解构赋值

```javascript

let [,,third] = ["foo", "bar", "baz"];
let [head, ...tail] = [1, 2, 3, 4];
let [x, , y] = [1, 2, 3];
//解构赋值允许指定默认值。
[x, y='b'] = ['a'] // x='a', y='b'
[x, y='b'] = ['a', undefined] // x='a', y='b'

//对于Set结构，也可以使用数组的解构赋值。
[a, b, c] = new Set(["a", "b", "c"])
//事实上，只要某种数据结构具有Iterator接口，都可以采用数组形式的解构赋值。
function* fibs() {var a = 0;var b = 1;while (true) {yield a;[a, b] = [b, a + b];}}var [first, second, third, fourth, fifth, sixth] = fibs();sixth // 5
```

> 注意，ES6内部使用严格相等运算符（===），判断一个位置是否有值。所以，如果一个数组成员不严格等于undefined，默认值是不会生效的。

``` javascript
//如果要将一个已经声明的变量用于解构赋值，必须非常小心。
var x;{x} = {x:1};// SyntaxError: syntax error

//为JavaScript引擎会将{x} 理解成一个代码块，从而发生语法错误。
//只有不将大括号写在行首，避免JavaScript将其解释为代码块，才能解决这个问题。

// 正确的写法({x} = {x:1});
//字符串
const [a, b, c, d, e] = 'hello';
//获取length
let {length : len} = 'hello';
```

* 不能使用圆括号的情况
	
``` javascript
	//变量声明语句中，模式不能带有圆括号。
	var [(a)] = [1];	var { x: (c) } = {};	var { o: ({ p: p }) } = { o: { p: 2 } };
	//函数参数中，模式不能带有圆括号。
	function f([(z)]) { return z; }	//不能将整个模式，或嵌套模式中的一层，放在圆括号之中。
	({ p: a }) = { p: 42 };	([a]) = [5];
```

* 可以使用圆括号

``` javascript
//可以使用圆括号的情况只有一种：赋值语句的非模式部分，可以使用圆括号。
[(b)] = [3]; // 正确({ p: (d) } = {}); // 正确[(parseInt.prop)] = [3]; // 正确
```

## 字符的扩展
* includes()：返回布尔值，表示是否找到了参数字符串。
* startsWith()：返回布尔值，表示参数字符串是否在源字符串的头部。
* endsWith()：返回布尔值，表示参数字符串是否在源字符串的尾部。

``` javascript
var s = "Hello world!";

//这三个方法都支持第二个参数，表示开始搜索的位置。
s.startsWith("world", 6) // true
s.endsWith("Hello", 5) // true
s.includes("Hello", 6) // false

```

> 使用第二个参数 n 时，endsWith 的行为与其他两个方法有所不同。它针对前 n 个字符，而其他两个方法针对从第 n 个位置直到字符串结束。

* repeat()返回一个新字符串，表示将原字符串重复 n 次。
### 模板字符串

``` javascript
$("#result").append(`
  There are <b>${basket.count}</b> items
   in your basket, <em>${basket.onSale}</em>
  are on sale!
`);

//如果在模板字符串中需要使用反引号，则前面要用反斜杠转义。
var greeting = `\`Yo\` World!`;
```

* 标签模板 可以用来自定义字符串拼接规则

	``` javascript
	var total = 30;
	var msg = passthru`The total is ${total} (${total*1.05} with tax)`;
	
	function passthru(literals) {
	  var result = "";
	  var i = 0;
	
	  while (i < literals.length) {
	    result += literals[i++];
	    if (i < arguments.length) {
	      result += arguments[i];
	    }
	  }
	
	  return result;
	
	}
	```

	* “标签模板”的一个重要应用，就是过滤 HTML 字符串，防止用户输入恶意内容。
	* 标签模板的另一个应用，就是多语言转换（国际化处理）。

## 数值的扩展
ES6 提供了二进制和八进制数值的新的写法，分别用前缀 0b 和 0o 表示。

* Number.isFinite(), Number.isNaN()

``` javascript
//Number.isFinite()用来检查一个数值是否非无穷（infinity）。
Number.isFinite(15); // true
Number.isFinite(0.8); // true
Number.isFinite(NaN); // false
Number.isFinite(Infinity); // false
Number.isFinite(-Infinity); // false
Number.isFinite("foo"); // false
Number.isFinite("15"); // false
Number.isFinite(true); // false

//Number.isNaN() 用来检查一个值是否为 NaN。
Number.isNaN(NaN); // true
Number.isNaN(15); // false
Number.isNaN("15"); // false
Number.isNaN(true); // false
```

* Number.parseInt(), Number.parseFloat()
ES6 将全局方法 parseInt()和 parseFloat()，移植到 Number 对象上面，行为完全保持不变。
* Number.isInteger()和安全整数   
在 JavaScript 内部，整数和浮点数是同样的储存方法，所以 3 和 3.0 被视为同一个值。
	* Number.MAX_SAFE_INTEGER 和 Number.MIN_SAFE_INTEGER 这两个常量，用来表示数值范围的上下限。
	* Number.isSafeInteger()则是用来判断一个整数是否落在这个范围之内。

### Math对象的扩展
* Math.trunc 方法用于去除一个数的小数部分，返回整数部分。
* Math.sign 方法用来判断一个数到底是正数、负数、还是零。如果参数为正数，返回 +1；参数为负数，返回 -1；参数为 0，返回 0；参数为 NaN，返回 NaN。

``` javascript
Math.sign(-5) // -1
Math.sign(5) // +1
Math.sign(0) // +0
Math.sign(-) // -0
Math.sign(NaN) // NaN
```

## 数组的扩展
* Array.from     
任何有 length 属性的对象，都可以通过 Array.from 方法转为数组。

``` javascript
Array.from({ 0: "a", 1: "b", 2: "c", length: 3 });

//Array.from()还可以接受第二个参数，作用类似于数组的 map 方法，用来对每个元素进行处理。
Array.from(arrayLike, x => x * x);
// 等同于
Array.from(arrayLike).map(x => x * x);

Array.from([1, , 2, , 3], (n) => n || 0)
// [1, 0, 2, 0, 3]

//Array.from()可以避免 JavaScript 将大于\uFFFF的 Unicode 字符，算作两个字符的bug。
function countSymbols(string) {
  return Array.from(string).length;
}
```

* Array.of() 方法用于将一组值，转换为数组。

``` javascript
//这个方法的主要目的，是弥补数组构造函数 Array() 的不足。

Array.of(3, 11, 8) // [3,11,8]
Array.of(3) // [3]
Array.of(3).length // 1

Array() // []
Array(3) // [undefined, undefined, undefined]
Array(3,11,8) // [3, 11, 8]
```

* 数组推导

``` javascript
var a1 = [1, 2, 3, 4];
var a2 = [for (i of a1) i * 2];

a2 // [2, 4, 6, 8]


var years = [ 1954, 1974, 1990, 2006, 2010, 2014 ];

[for (year of years) if (year > 2000) year];
// [ 2006, 2010, 2014 ]

[for (year of years) if (year > 2000) if(year < 2010) year];
// [ 2006]

[for (year of years) if (year > 2000 && year < 2010) year];
// [ 2006]
```

## 对象的扩展
* Object.is() 
它与严格比较运算符（===）的行为基本一致，不同之处只有两个：一是 +0 不等于 -0，二是 NaN 等于自身。

``` javascript

+0 === -0 //true
NaN === NaN // false

Object.is(+0, -0) // false
Object.is(NaN, NaN) // true

```

* Object.assign()

Object.assign 方法用来将源对象（source）的所有可枚举属性，复制到目标对象（target）。它至少需要两个对象作为参数，第一个参数是目标对象，后面的参数都是源对象。只要有一个参数不是对象，就会抛出 TypeError 错误。

如果目标对象与源对象有同名属性，或多个源对象有同名属性，则后面的属性会覆盖前面的属性
``` javascript
var target = { a: 1, b: 1 };

var source1 = { b: 2, c: 2 };
var source2 = { c: 3 };

Object.assign(target, source1, source2);
target // {a:1, b:2, c:3}
```

### Symbol
* 属性名属于 Symbol 类型，就都是独一无二的，可以保证不会与其他属性名产生冲突。
	* 相同参数的返回值不同
	* Symbol 类型的值可以转为字符串。

``` javascript
// 有参数的情况
var s1 = Symbol("foo");
var s2 = Symbol("foo");
s1 === s2 // false

//使用和定义必须使用方括号
let s = Symbol();
let obj = {
  [s]: function (arg) { ... }
};
obj[s](123);

//Symbol.for() 相同参数返回相同的值
var s1 = Symbol.for('foo');
var s2 = Symbol.for('foo');

s1 === s2 // true

//Symbol.keyFor 方法返回一个已登记的 Symbol 类型值的 key
var s1 = Symbol.for("foo");
Symbol.keyFor(s1) // "foo"

var s2 = Symbol("foo");
Symbol.keyFor(s2) // undefined
```

### Proxy
* Proxy 用于修改某些操作的默认行为，等同于在语言层面做出修改，所以属于一种“元编程”（meta programming），即对编程语言进行编程。

## 函数的扩展
### 参数允许设置默认值
* 指定了默认值以后，函数的 length 属性，将返回没有指定默认值的参数个数。也就是说，指定了默认值后，length 属性将失真。

``` javascript
(function(a){}).length // 1
(function(a = 5){}).length // 0
(function(a, b, c = 5){}).length // 2

//利用参数默认值，可以指定某一个参数不得省略，如果省略就抛出一个错误。

function throwIfMissing() {
  throw new Error('Missing parameter');
}

function foo(mustBeProvided = throwIfMissing()) {
  return mustBeProvided;
}

```

### rest参数
* 函数的 length 属性，不包括 rest 参数。

``` javascript
function add(...values) {
   let sum = 0;

   for (var val of values) {
      sum += val;
   }

   return sum;
}

add(2, 5, 3) // 10
```

* 扩展运算符

``` javascript
function push(array, ...items) {
  array.push(...items);
}

function add(x, y) {
  return x + y;
}

var numbers = [4, 38];
add(...numbers)


// ES5的写法
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
Array.prototype.push.apply(arr1, arr2);

// ES6的写法
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
arr1.push(...arr2);

//数组赋值
var a = [1];
var b = [2, 3, 4];
var c = [6, 7];
var d = [0, ...a, ...b, 5, ...c];

const [first, ...rest] = [1, 2, 3, 4, 5];
first // 1
rest  // [2, 3, 4, 5]

const [first, ...rest] = [];
first // undefined
rest  // []:

//字符串转数组
[..."hello"]
// [ "h", "e", "l", "l", "o" ]

//任何类似数组的对象，都可以用扩展运算符转为真正的数组。
var nodeList = document.querySelectorAll('div');
var array = [...nodeList];
```

### 箭头函数
* 由于大括号被解释为代码块，所以如果箭头函数直接返回一个对象，必须在对象外面加上括号。

``` javascript
var getTempItem = id => ({ id: id, name: "Temp" });

```

* 箭头函数有几个使用注意点。
	* 函数体内的 this 对象，绑定定义时所在的对象，而不是使用时所在的对象。
	* 不可以当作构造函数，也就是说，不可以使用 new 命令，否则会抛出一个错误。
	* 不可以使用 arguments 对象，该对象在函数体内不存在。

``` javascript
const pipeline = (...funcs) =>
  val => funcs.reduce((a, b) => b(a), val);

const plus1 = a => a + 1;
const mult2 = a => a * 2;
const addThenMult = pipeline(plus1, mult2);

addThenMult(5)
// 12
```
	
### 函数绑定
* 尾调用优化
* 尾递归

``` javascript
function factorial(n, total = 1) {
  if (n === 1) return total;
  return factorial(n - 1, n * total);
}

factorial(5) // 120
```
尾调用可以提高执行效率。

## set和map
* set中元素不能重复
* set 使用`===`比较，对象总是不相等。 唯一的例外是 NaN 等于自身（精确相等运算符认为 NaN 不等于自身）。

``` javascript
function dedupe(array) {
  return Array.from(new Set(array));
}

dedupe([1,1,2,3]) // [1, 2, 3]
```
### weakSet
* WeakSet 的成员只能是对象，而不能是其他类型的值。
* WeakSet 中的对象都是弱引用，即垃圾回收机制不考虑 WeakSet 对该对象的引用    

> WeakSet 的一个用处，是储存 DOM 节点，而不用担心这些节点从文档移除时，会引发内存泄漏。

### map

```javascript
let map = new Map();

map.set(NaN, 123);
map.get(NaN) // 123

map.set(-0, 123);
map.get(+0) // 123

//set可以使用链式写法
let map = new Map()
  .set(1, 'a')
  .set(2, 'b')
  .set(3, 'c');

```

### WeakMap
* eakMap 结构与 Map 结构基本类似，唯一的区别是它只接受对象作为键名（null 除外）

> WeakMap 的设计目的在于，键名是对象的弱引用（垃圾回收机制不将该引用考虑在内），所以其所对应的对象可能会被自动回收。当对象被回收后，WeakMap 自动移除对应的键值对。典型应用是，一个对应 DOM 元素的 WeakMap 结构，当某个 DOM 元素被清除，其所对应的 WeakMap 记录就会自动被移除。基本上，WeakMap 的专用场合就是，它的键所对应的对象，可能会在将来消失。WeakMap 结构有助于防止内存泄漏。

## Iterator 和 for...of 循环
* 默认的 Iterator 接口部署在数据结构的 Symbol.iterator 属性
* 对于类似数组的对象（存在数值键名和 length 属性），部署 Iterator 接口，有一个简便方法，就是Symbol.iterator方法直接引用数值的 Iterator 接口。

 ```js
 NodeList.prototype[Symbol.iterator] =      
 							Array.prototype[Symbol.iterator];
 ```

## Generator 函数
*

``` js
function* f() {
  for(var i=0; true; i++) {
    var reset = yield i;
    if(reset) { i = -1; }
  }
}

var g = f();

g.next() // { value: 0, done: false }
g.next() // { value: 1, done: false }
g.next(true) // { value: 0, done: false }
```

* 可以在 Generator 函数运行的不同阶段，从外部向内部注入不同的值，从而调整函数行为。

```js
function* foo(x) {
  var y = 2 * (yield (x + 1));
  var z = yield (y / 3);
  return (x + y + z);
}

var it = foo(5);

it.next()
// { value:6, done:false }
it.next(12)
// { value:8, done:false }
it.next(13)
// { value:42, done:true }

```
> 注意，由于 next 方法的参数表示上一个 yield 语句的返回值，所以第一次使用 next 方法时，不能带有参数。V8 引擎直接忽略第一次使用 next 方法时的参数，只有从第二次使用 next 方法开始，参数才是有效的。


```js
//斐波那契数列
function* fibonacci() {
  let [prev, curr] = [0, 1];
  for (;;) {
    [prev, curr] = [curr, prev + curr];
    yield curr;
  }
}

for (let n of fibonacci()) {
  if (n > 1000) break;
  console.log(n);
}
```

* 如果 yield 命令后面跟的是一个遍历器，需要在 yield 命令后面加上星号，表明它返回的是一个遍历器。这被称为 yield*语句。

```js
let delegatedIterator = (function* () {
  yield 'Hello!';
  yield 'Bye!';
}());

let delegatingIterator = (function* () {
  yield 'Greetings!';
  yield* delegatedIterator;
  yield 'Ok, bye.';
}());

for(let value of delegatingIterator) {
  console.log(value);
}
// "Greetings!
// "Hello!"
// "Bye!"
// "Ok, bye."
```

* 遍历二叉树

```js

// 下面是二叉树的构造函数，
// 三个参数分别是左树、当前节点和右树
function Tree(left, label, right) {
  this.left = left;
  this.label = label;
  this.right = right;
}

// 下面是中序（inorder）遍历函数。
// 由于返回的是一个遍历器，所以要用generator函数。
// 函数体内采用递归算法，所以左树和右树要用yield*遍历
function* inorder(t) {
  if (t) {
    yield* inorder(t.left);
    yield t.label;
    yield* inorder(t.right);
  }
}

// 下面生成二叉树
function make(array) {
  // 判断是否为叶节点
  if (array.length == 1) return new Tree(null, array[0], null);
  return new Tree(make(array[0]), array[1], make(array[2]));
}
let tree = make([[['a'], 'b', ['c']], 'd', [['e'], 'f', ['g']]]);

// 遍历二叉树
var result = [];
for (let node of inorder(tree)) {
  result.push(node);
}

result
// ['a', 'b', 'c', 'd', 'e', 'f', 'g']
```

### Generator 函数推导
```js
let generator = function* () {
  for (let i = 0; i < 6; i++) {
    yield i;
  }
}

let squared = ( for (n of generator()) n * n );
// 等同于
// let squared = Array.from(generator()).map(n => n * n);

console.log(...squared);
// 0 1 4 9 16 25
```

* 惰性求值，节省内存

```js
//传统方法
let bigArray = new Array(100000);
for (let i = 0; i < 100000; i++) {
  bigArray[i] = i;
}
let first = bigArray.map(n => n * n)[0];
console.log(first);

//Generator 方法
let bigGenerator = function* () {
  for (let i = 0; i < 100000; i++) {
    yield i;
  }
}
let squared = ( for (n of bigGenerator()) n * n );
console.log(squared.next());

```

* 实现状态机

```js
//传统方法
var ticking = true;
var clock = function() {
  if (ticking)
    console.log('Tick!');
  else
    console.log('Tock!');
  ticking = !ticking;
}

//Generator
var clock = function*(_) {
  while (true) {
    yield _;
    console.log('Tick!');
    yield _;
    console.log('Tock!');
  }
};

```

## Promise 对象
* Promise.race()
	* Promise.race方法同样是将多个Promise实例，包装成一个新的Promise实例。
	* `var p = Promise.race([p1,p2,p3]);`
	
		> 只要p1、p2、p3之中有一个实例率先改变状态，p的状态就跟着改变。那个率先改变的Promise实例的返回值，就传递给p的返回值。

* 有时需要将现有对象转为Promise对象，Promise.resolve方法就起到这个作用。
	* 如果Promise.resolve方法的参数，不是具有then方法的对象（又称thenable对象），则返回一个新的Promise对象，且它的状态为fulfilled。
	
		```js
		var p = Promise.resolve('Hello');
		
		//p状态为fulfilled，回调函数会立即执行
		p.then(function (s){
		  console.log(s)
		});
		```
* Promise.reject(reason)方法也会返回一个新的Promise实例，该实例的状态为rejected。

### async函数
* async函数就是将Generator函数的星号（*）替换成async，将yield替换成await

## Class 和model
```javascript
//ES5 写法
function Point(x,y){
  this.x = x;
  this.y = y;
}

Point.prototype.toString = function () {
  return '('+this.x+', '+this.y+')';
}

//定义类
class Point {

  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

//前面不需要加上function这个保留字，  
toString() {
    return '('+this.x+', '+this.y+')';
  }

}

```

* 定义“类”的方法的时候，前面不需要加上function这个保留字，直接把函数定义放进去了就可以了。
* 除了constructor方法以外，类的方法都定义在类的prototype属性上面。
* class不存在变量提升
* 类和模块的内部，默认就是严格模式，所以不需要使用use strict指定运行模式。

### Class的继承
* `class ColorPoint extends Point {}`
* `super`关键字，它指代父类的实例（即父类的this对象）
	* 子类必须在constructor方法中调用super方法，否则新建实例时会报错。
	* 另一个需要注意的地方是，在子类的构造函数中，只有调用super之后，才可以使用this关键字，否则会报错。

``` js

class ColorPoint extends Point {

  constructor(x, y, color) {
    super(x, y); // 等同于parent.constructor(x, y)
    this.color = color;
  }

  toString() {
    return this.color + ' ' + super.toString(); // 等同于parent.toString()
  }

}
```

* Object.getPrototypeOf()方法可以用来从子类上获取父类。
	* `Object.getPrototypeOf(ColorPoint) === Point`

* set和get方法

```js

class MyClass {
  get prop() {
    return 'getter';
  }
  set prop(value) {
    console.log('setter: '+value);
  }
}

let inst = new MyClass();

inst.prop = 123;
// setter: 123

inst.prop
// 'getter'
```	

* 如果某个方法之前加上星号（*），就表示该方法是一个Generator函数。

### Module

* export命令，import命令
	* 导出

		```js
		
		// circle.js
		
		export function area(radius) {
		  return Math.PI * radius * radius;
		}
		
		export function circumference(radius) {
		  return 2 * Math.PI * radius;
		}
		```

	* 导入
	
		```js
		// main.js
		module circle from 'circle';
		//import { area, circumference } from 'circle';
		
		console.log("圆面积：" + area(4));
		console.log("圆周长：" + circumference(14));		```
		
* export default命令

export default命令用于指定模块的默认输出。显然，一个模块只能有一个默认输出，因此export deault命令只能使用一次。所以，import命令后面才不用加大括号，因为只可能对应一个方法。


	```js
	import crc32 from 'crc32';
	// 对应的输出
	export default function crc32(){}
	
	import { crc32 } from 'crc32';
	// 对应的输出
	export function crc32(){};
	```	
	
### 模块的继承