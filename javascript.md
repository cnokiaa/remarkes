# JavaScript (ES6)

### 变量声明
* ES5:	var、function
* ES6:	let、const、import、class

##### let
let 声明了一个块级域的局部变量，并且可以给它一个初始化值。(不存在变量提升)

let声明的变量作用域包含定义它的块以及任何包含的子块中。

let与var非常像。它们之间主要的区别在于一个var变量的作用域是整个封闭函数。

#### const

const 声明创建一个只读的常量。这不意味着常量指向的值不可变，而是变量标识符的值只能赋值一次。(不存在变量提升)

可以在全局作用域或者函数内声明常量，常量需要被初始化。

当用class 创建对象时，constructor是一个用来创建和初始化的对象的特殊方法。

子类必须在constructor方法中调用super方法，否则新建实例时会报错。
******
### 数据类型
undefined、null、boolean、string、number、object、symbol

##### Symbol
表示独一无二的值。

Symbol函数前不能使用new命令，否则会报错。因为生成的Symbol是一个原始类型的值，不是对象。

也就是说，由于Symbol值不是对象，所以不能添加属性。基本上，它是一种类似于字符串的数据类型。
（Symbol值的唯一性）

    var mySymbol = Symbol();

    // 第一种写法
    var a = {};
    a[mySymbol] = 'Hello!';

    // 第二种写法
    var a = {
      [mySymbol]: 'Hello!'
    };

    // 第三种写法
    var a = {};
    Object.defineProperty(a, mySymbol, { value: 'Hello!' });

    // 以上写法都得到同样结果
    a[mySymbol] // "Hello!"

### “集合”数据结构
array、object、 map、set
******
### 函数
#### 1. es6函数参数的默认值
* 参数变量是默认声明的，所以不能用let或const再次声明。
* 函数不能有同名参数


    function log(x, y = 'World') {
    console.log(x, y);
    }

    log('Hello') // Hello World
    log('Hello', 'China') // Hello China

* 参数默认值可以与解构赋值的默认值，结合起来使用


    function foo({x, y = 5}) {
    console.log(x, y);
    }

    foo({}) // undefined, 5
    foo({x: 1}) // 1, 5
    foo({x: 1, y: 2}) // 1, 2
    foo() // TypeError: Cannot read property 'x' of undefined

* 参数默认值的位置

有默认值的参数不是尾参数,无法省略该参数，除非显式输入`undefined`，`null`则没有这个效果。

    function f(x = 1, y) {
      return [x, y];
    }

    f() // [1, undefined]
    f(2) // [2, undefined])
    f(, 1) // 报错
    f(undefined, 1) // [1, 1]

#### 2. rest参数
rest 参数（形式为`...变量名`），用于获取函数的多余参数，这样就不需要使用arguments对象了。rest 参数搭配的变量是一个数组，该变量将多余的参数放入数组中。

    function add(...values) {
      let sum = 0;

      for (var val of values) {
        sum += val;
      }

      return sum;
    }

    add(2, 5, 3) // 10
* rest 参数之后不能再有其他参数（即只能是最后一个参数），否则会报错。
* 函数的length属性，不包括 rest 参数。


    (function(a) {}).length  // 1
    (function(...a) {}).length  // 0
    (function(a, ...b) {}).length  // 1

#### 3. 扩展运算符
扩展运算符（spread）是三个点（`...`）。它好比 rest 参数的逆运算，将一个数组转为用逗号分隔的参数序列。
* 合并数组


    var arr1 = ['a', 'b'];
    var arr2 = ['c'];
    var arr3 = ['d', 'e'];

    // ES5的合并数组
    arr1.concat(arr2, arr3);
    // [ 'a', 'b', 'c', 'd', 'e' ]

    // ES6的合并数组
    [...arr1, ...arr2, ...arr3]
    // [ 'a', 'b', 'c', 'd', 'e' ]

* 与解构赋值结合

将扩展运算符用于数组赋值，只能放在参数的最后一位，否则会报错。(和rest参数一样)

    const [first, ...rest] = [1, 2, 3, 4, 5];
    first // 1
    rest  // [2, 3, 4, 5]

    const [first, ...rest] = [];
    first // undefined
    rest  // []

    const [...butLast, last] = [1, 2, 3, 4, 5];
    // 报错

* 函数的返回值

js函数只能返回一个值，需返回多个值，只能返回数组或对象。扩展运算符提供了解决这个问题的一种变通方法。

    var dateFields = readDateFields(database);
    var d = new Date(...dateFields);

* 字符串

扩展运算符还可以将字符串转为真正的数组。

    [...'hello']
    // [ "h", "e", "l", "l", "o" ]

* 实现了Iterator接口的对象

任何Iterator接口的对象，都可以用扩展运算符转为真正的数组。

    var nodeList = document.querySelectorAll('div');
    var array = [...nodeList];

* Map和Set结构，Generator函数


    let map = new Map([
      [1, 'one'],
      [2, 'two'],
      [3, 'three'],
    ]);

    let arr = [...map.keys()]; // [1, 2, 3]

    var go = function*(){
      yield 1;
      yield 2;
      yield 3;
    };

    [...go()] // [1, 2, 3]

#### 4. 严格模式

只要函数参数使用了默认值、解构赋值、或者扩展运算符，那么函数内部就不能显式设定为严格模式，否则会报错。

#### 5. 箭头函数   
[参考链接](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

`()=>this.function()`  (左边为传参，右边为回调函数---我的理解)
`this.function.bind(this,c)`	完全修复了this的指向，this总是指向词法作用域，也就是外层调用者obj

* 简单示例


    var f = v => v;
    //等同于下面函数
    var f = function(v) {
      return v;
    };

    /***不需要参数或需要多个参数，就使用一个圆括号代表参数部分***/
    var f = () => 5;
    // 等同于
    var f = function () { return 5 };

    var sum = (num1, num2) => num1 + num2;
    // 等同于
    var sum = function(num1, num2) {
      return num1 + num2;
    };

    /***代码块部分多于一条语句，就要使用大括号将它们括起来，并且使用return语句返回。***/
    var sum = (num1, num2) => { return num1 + num2; }

    /***由于大括号被解释为代码块，所以如果箭头函数直接返回一个对象，必须在对象外面加上括号。***/
    var getTempItem = id => ({ id: id, name: "Temp" });

（1）函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。

（2）不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。

（3）不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。

（4）不可以使用yield命令，因此箭头函数不能用作 Generator 函数。


#### 6. call、apply、bind 一般用来指定this的环境
简单示例

    window.color='red';
    var o={color:"blue"};
    function sayColor(){
      alert(this.color);
    };
    sayColor(); //red（全局函数，this是window）
    sayColor.call(this);//red(调用call方法，指定对象是this，这里的this是window，没什么意义)
    sayColor.call(window);//red(调用call方法，指定对象是window，没什么意义)
    sayColor.call(o); //blue (调用call方法，指定对象是o，所以this指代对象o，这里由原来的window指向了o)
    sayColor.apply(o);//blue (调用call方法，指定对象是o，所以this指代对象o，这里由原来的window指向了o)
示例2

    var wx = {
      name: 'liu',
      say: function(x,y){
        alert(this.name + x + y);
      }
    }
    var wh = {
      name: 'qiang'
    }
    wx.say.call(wh,'11','12');    //qiang 11 12
    wx.say.apply(wh,['21','22']); //qiang 21 22
    wx.say.bind(wh,'31','32')();  //qiang 31 32
* call()

call() 方法调用一个函数, 其具有一个指定的this值和分别地提供的参数(参数的列表)。

*call() 和 apply() 方法类似，只有一个区别，就是call()方法接受的是若干个参数的列表，而apply()方法接受的是一个包含多个参数的数组。*

    fun.call(thisArg[, arg1[, arg2[, ...]]])
    // thisArg 在fun函数运行时指定的this值。
    // 需注意的是，指定的this值并不一定是该函数执行时真正的this值，如果这个函数处于非严格模式下，则指定为null和undefined的this值会自动指向全局对象(浏览器中就是window对象)，同时值为原始值(数字，字符串，布尔值)的this会指向该原始值的自动包装对象。

    //arg1, arg2, ... 指定的参数列表。

可以让call()中的对象调用当前对象所拥有的function。你可以使用call()来实现继承：写一个方法，然后让另外一个新的对象来继承它（而不是在新对象中再写一次这个方法）。

#### 7. 函数绑定运算符
函数绑定运算符是并排的两个双冒号（::），
双冒号左边是一个对象，右边是一个函数。

该运算符会自动将左边的对象，作为上下文环境（即this对象），绑定到右边的函数上面


    foo::bar;
    // 等同于
    bar.bind(foo);

    foo::bar(...arguments);
    // 等同于
    bar.apply(foo, arguments);

    const hasOwnProperty = Object.prototype.hasOwnProperty;
    function hasOwn(obj, key) {
      return obj::hasOwnProperty(key);
    }

    let log = ::console.log;
    // 等同于
    var log = console.log.bind(console);

#### 8. 尾调用优化
* 尾调用

函数式编程的一个重要概念，就是指某个函数的最后一步是调用另一个函数。

* 尾递归

函数调用自身，称为递归。如果尾调用自身，就称为尾递归。


******
### 对象的扩展
#### 1. 属性的简洁表示法

    /**直接写入变量和函数，作为对象的属性和方法。**/
    var foo = 'bar';
    var baz = {foo};
    baz // {foo: "bar"}
    // 等同于
    var baz = {foo: foo};

    function f(x, y) {
      return {x, y};
    }
    // 等同于
    function f(x, y) {
      return {x: x, y: y};
    }
    f(1, 2) // Object {x: 1, y: 2}

    /**方法也可以简写。**/
    var o = {
      method() {
        return "Hello!";
      }
    };

    // 等同于

    var o = {
      method: function() {
        return "Hello!";
      }
    };

#### 2. 属性名表达式
属性名表达式如果是一个对象，默认情况下会自动将对象转为字符串[object Object]，这一点要特别小心。


    /**ES6 允许字面量定义对象时，用表达式作为对象的属性名，即把表达式放在方括号内。**/
    var lastWord = 'last word';
    var a = {
      'first word': 'hello',
      [lastWord]: 'world'
    };
    a['first word'] // "hello"
    a[lastWord] // "world"
    a['last word'] // "world"

    /**表达式还可以用于定义方法名**/
    let obj = {
      ['h' + 'ello']() {
        return 'hi';
      }
    };

    obj.hello() // hi

#### 3. Object.is()
ES5比较两个值是否相等，只有两个运算符：相等运算符（==）和严格相等运算符（===）。
(==)会自动转换数据类型；(===) 中NaN不等于自身，+0 等于 -0。
Object.is() 用来比较两个值是否严格相等，与(===)的行为基本一致。


    +0 === -0 //true
    NaN === NaN // false

    Object.is(+0, -0) // false
    Object.is(NaN, NaN) // true

#### 4. Object.assign()
用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）。

目标对象与源对象有同名属性，或多个源对象有同名属性，则后面的属性会覆盖前面的属性。

其他类型的值（即数值、字符串和布尔值）不在首参数，也不会报错。但是，除了字符串会以数组形式，拷贝入目标对象，其他值都不会产生效果。

    var target = { a: 1, b: 1 };

    var source1 = { b: 2, c: 2 };
    var source2 = { c: 3 };

    Object.assign(target, source1, source2);
    target // {a:1, b:2, c:3}

#### 5. 属性的可枚举性
对象的每个属性都有一个描述对象（Descriptor），用来控制该属性的行为。Object.getOwnPropertyDescriptor方法可以获取该属性的描述对象。

    let obj = { foo: 123 };
    Object.getOwnPropertyDescriptor(obj, 'foo')
    //  {
    //    value: 123,
    //    writable: true,
    //    enumerable: true,
    //    configurable: true
    //  }

#### 6. 属性的遍历
（1）for...in

for...in循环遍历对象自身的和继承的可枚举属性（不含 Symbol 属性）。

（2）Object.keys(obj)

Object.keys返回一个数组，包括对象自身的（不含继承的）所有可枚举属性（不含 Symbol 属性）。

（3）Object.getOwnPropertyNames(obj)

Object.getOwnPropertyNames返回一个数组，包含对象自身的所有属性（不含 Symbol 属性，但是包括不可枚举属性）。

（4）Object.getOwnPropertySymbols(obj)

Object.getOwnPropertySymbols返回一个数组，包含对象自身的所有 Symbol 属性。

（5）Reflect.ownKeys(obj)

Reflect.ownKeys返回一个数组，包含对象自身的所有属性，不管属性名是 Symbol 或字符串，也不管是否可枚举。

#### 7.  prototype
`__proto__`属性（前后各两个下划线），用来读取或设置当前对象的prototype对象
* Object.setPrototypeOf()

与`__proto__`相同，用来设置一个对象的prototype对象，返回参数对象本身。它是 ES6 正式推荐的设置原型对象的方法。

    /**将proto对象设为obj对象的原型，所以从obj对象可以读取proto对象的属性。**/
    let proto = {};
    let obj = { x: 10 };
    Object.setPrototypeOf(obj, proto);

    proto.y = 20;
    proto.z = 40;

    obj.x // 10
    obj.y // 20
    obj.z // 40

* Object.getPrototypeOf()

该方法与Object.setPrototypeOf方法配套，用于读取一个对象的原型对象。

#### 8. Object.keys()，Object.values()，Object.entries()

    var obj = { foo: 'bar', baz: 42 };
    Object.keys(obj)
    //['foot','baz']
    Object.values(obj)
    // ["bar", 42]
    Object.entries(obj)
    // [ ["foo", "bar"], ["baz", 42] ]

#### 9. Null传导运算符

    // 如果 a 是 null 或 undefined, 返回 undefined
    // 否则返回 a.b.c().d
    a?.b.c().d

    // 如果 a 是 null 或 undefined，下面的语句不产生任何效果
    // 否则执行 a.b = 42
    a?.b = 42

    // 如果 a 是 null 或 undefined，下面的语句不产生任何效果
    delete a?.b
******

### do
块级作用域可以变为表达式，也就是说可以返回值，
办法就是在块级作用域之前加上do，使它变为do表达式。


### 指数运算符 **

2 ** 2 = 4 （a=a*a 第二个相当于次数）


### proxy '代理器'
遍历器（Iterator）它是一种接口，为各种不同的数据结构提供统一的访问机制。

任何数据结构只要部署Iterator接口，就可以完成遍历操作（即依次处理该数据结构的所有成员）。

### Iterator
Iterator的作用有三个：
  * 一是为各种数据结构，提供一个统一的、简便的访问接口；
  * 二是使得数据结构的成员能够按某种次序排列；
  * 三是ES6创造了一种新的遍历命令for...of循环，Iterator接口主要供for...of消费。

(for.in循环，它遍历的实际上是对象的属性名称。一个Array数组实际上也是一个对象，它的每个元素的索引被视为一个属性。for.of只循环集合本身的元素)

### Generator函数
执行Generator函数会返回一个遍历器对象，也就是说，Generator函数除了状态机，还是一个遍历器对象生成函数。

返回的遍历器对象，可以依次遍历Generator函数内部的每一个状态。（执行过程中可返回多次）

形式上，Generator函数是一个普通函数，但是有两个特征。
* 一是，function关键字与函数名之间有一个星号；
* 二是，函数体内部使用yield语句，定义不同的内部状态

### Promise对象(承诺)
对象用于异步计算。一个 Promise 表示一个现在或将来可用，亦或永远不可用的值。

对象的状态不受外界影响。

Promise对象代表一个异步操作，
有三种状态：Pending（进行中）、Resolved（已完成，又称Fulfilled）和Rejected（已失败）。

一旦状态改变，就不会再变，任何时候都可以得到这个结果。

then()方法返回一个  Promise。它最多需要有两个参数：Promise的成功和失败情况的回调函数。
### class


    class Point {
      constructor(){
        // 类的默认方法
      }

      toString(){
        // ...
      }

      toValue(){
        // ...
      }
    }

    // 等同于

    Point.prototype = {
      toString(){},
      toValue(){}
    };

类的构造函数，不使用new是没法调用的，会报错。

这是它跟普通构造函数的一个主要区别，后者不用new也可以执行。

class不存在变量提升（与es5完全不一样）

ES5的继承，实质是先创造子类的实例对象this，然后再将父类的方法添加到this上面（Parent.apply(this)）。

ES6的继承机制完全不同，实质是先创造父类的实例对象this（所以必须先调用super方法），然后再用子类的构造函数修改this。


### 参数
函数体内可通过arguments对象来访问参数数组，获取传递给函数的每个参数。

    function abc(){
      alert(arguments.length+','+arguments[0]);
    }
    abc("e");	// 1,e



### 闭包
闭包就是能够读取其他函数内部变量的函数。(定义在一个函数内部的函数)
闭包的作用：

读取函数内部的变量；让变量的值始终保存在内存中。

### 高阶函数
高阶函数:一个函数可以接受另一个函数作为参数

map()作为高阶函数，事实上它把运算规则抽象了，因此，我们不但可以计算简单的f(x)=x2，还可以计算任意复杂的函数，比如，把Array的所有数字转为字符串

		var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
		arr.map(String); // ['1', '2', '3', '4', '5', '6', '7', '8', '9']

reduce()把结果继续和序列的下一个元素做累积计算.

比方说对一个Array求和，就可以用reduce实现:

    var arr = [1, 3, 5, 7, 9];
		arr.reduce(function (x, y) {
    			return x + y;
		}); // 25

filter()过滤array返回剩下的元素

sort()排序

### 数组

只要是部署了Iterator接口的数据结构，Array.from都能将其转为数组
Array.of()将一组值转换为数组

copyWithin

    // 将3号位复制到0号位
    [1, 2, 3, 4, 5].copyWithin(0, 3, 4)
    // [4, 2, 3, 4, 5]

fill方法使用给定值，填充一个数组。

    ['a', 'b', 'c'].fill(7, 1, 2)
    // ['a', 7, 'c']

entries()，keys()和values()——用于遍历数组
keys()是对键名的遍历、values()是对键值的遍历，entries()是对键值对的遍历。

    for (let [index, elem] of ['a', 'b'].entries()) {
      console.log(index, elem);
    }
    // 0 "a"
    // 1 "b"

include

返回一个布尔值，表示某个数组是否包含给定的值

slice

		var arr = ['A', 'B', 'C', 'D', 'E', 'F', 'G'];
		arr.slice(0, 3); // 从索引0开始，到索引3结束，但不包括索引3: ['A', 'B', 'C']
		arr.slice(3); // 从索引3开始到结束: ['D', 'E', 'F', 'G']
reverse

		var arr = ['one', 'two', 'three'];
		arr.reverse();
		arr; // ['three', 'two', 'one']
splice

		var arr = ['Microsoft', 'Apple', 'Yahoo', 'AOL', 'Excite', 'Oracle'];
		// 从索引2开始删除3个元素,然后再添加两个元素:
		arr.splice(2, 3, 'Google', 'Facebook'); // 返回删除的元素 ['Yahoo', 'AOL', 'Excite']
		arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
concat  方法把当前的Array和另一个Array连接起来，并返回一个新的Array

join    把当前Array的每个元素都用指定的字符串连接起来，然后返回连接后的字符串

    var arr = ['A', 'B', 'C', 1, 2, 3];
		arr.join('-'); // 'A-B-C-1-2-3'


### 正则表达式RegExp

    .  匹配任意字符
    \d 匹配一个数字
    \w 匹配一个字母
    \s 匹配任何不可见字符，包括空格、制表符、换页符等等。等价于[ \f\n\r\t\v]。
    *  表示任意个字符(包括0)
    +  表示至少一个字符
    ?  表示0或1个字符，匹配模式是非贪婪的
    ^  表示开头
    $  表示结尾
    {n}表示n个字符
    {n,m}表示n到m个字符
    [] 表示范围

### json
`JSON.stringify(a);` 将a对象格式化为json字符串

### 面向对象
继承

Class(es6)

		Class A extends B{
			constructor(name){
				super(name);
				this.arg = arg;
			}
			say(){
				return this.name;
			}
		}



### 浏览器对象
navigator浏览器的相关信息
cookie

JavaScript 所有的代码都是单线程的。

http://g.tbcdn.cn/mtb/lib-flexible/0.3.4/??flexible_css.js,flexible.js
### 正则表达式图示
![Alt text](./regexp.gif)
