## 🔄️[类型转换](https://zh.javascript.info/type-conversions)

### 字符串转换

-  显式的类型转换  **String(value)**  

```javascript
const boo1 = true;
console.log(typeof a);   // boolean

const str1 = String(a);
console.log(typeof b);   // string
```

- 隐式类型转换

```javascript
const boo1 = true;
console.log(typeof (a+''))  // string

const num = 1;
console.log(typeof (num + ''))
```

### 数字型转换

- 显示类型转换  **Number(value) & parseInt(value)**

```javascript
const str1 = '1';
console.log(typeof Number(str1));  // number
console.log(typeof parseInt(str1));  // number
```

- 隐式类型转换

```javascript
console.log('2' / '1');   // 2
console.log('6' - '2');   // 4
```

事实上，不仅只有string类型能转化为number类型

| 值              | 变成……                                                       |
| --------------- | ------------------------------------------------------------ |
| `undefined`     | `NaN`                                                        |
| `null`          | `0`                                                          |
| `true 和 false` | `1` and `0`                                                  |
| `string`        | 去掉首尾空格后的纯数字字符串中含有的数字。如果剩余字符串为空，则转换结果为 `0`。否则，将会从剩余字符串中“读取”数字。当类型转换出现 error 时返回 `NaN` |

```javascript
console.log(Number(undefined));   // NaN
console.log(Number(null));        // 0
console.log(Number(true));        // 1
console.log(Number(false));       // 0
console.log(Number(''));          // 0
console.log(Number('abc'));       // NaN
```

-  加号 ‘+’ 连接字符串
  **几乎所有的算术运算符都将值转换为数字进行运算**，加号 `+` 是个**例外**。如果其中一个运算元是字符串，则另一个也会被转换为字符串。
  **这仅仅发生在至少其中一方为字符串的情况下**。否则值会被转换为数字。  

```javascript
console.log(1 + '2'); // '12' (字符串在加号右边)
console.log('1' + 2); // '12' (字符串在加号左边)
console.log(true + 2); // 3
```

## 类（Class）

在ES6之前，如果我们要生成一个实例对象，传统的方法就是写一个构造函数，例子如下：

```javascript
function Person(name, age) {
    this.name = name
    this.age = age
}

Person.prototype.information = function () {
    return 'My name is ' + this.name + ', I am ' + this.age
}  // 原型链

const per = new Person('jack', 18)
console.log(per);                      // Person { name: 'jack', age: 18 }
console.log(per.information());        // My name is jack, I am 18
```

**new 运算符**创建一个用户定义的对象类型的实例或具有构造函数的内置对象的实例。

但是在ES6之后，我们只需要写成以下形式：

```javascript
class Person {
    constructor(name, age) {
        this.name = name
        this.age = age
    }
    information() {
        return `My name is ${this.name} I am ${this.age}`
    }
}

const per = new Person('jack', 18)
console.log(per);                      // Person { name: 'jack', age: 18 }
console.log(per.information());        // My name is jack, I am 18
```

## Function

上一节课我们讲了函数其实是一个对象，以及怎么创建函数，这一节课带大家深刻认识一下函数。

### 属性“name”

函数对象包含一些便于使用的属性。

比如，一个函数的名字可以通过属性 “name” 来访问：

```javascript
function sayHi() {   
  console.log("Hi"); 
} 
console.log(sayHi.name); // sayHi
```

更有趣的是，名称赋值的逻辑很智能。即使函数被创建时没有名字，名称赋值的逻辑也能给它赋予一个正确的名字，然后进行赋值：

```javascript
let sayHi = function () {
    console.log("Hi");
};

console.log(sayHi.name); // sayHi（有名字！）
```

当以默认值的方式完成了赋值时，它也有效：

```javascript
function f(sayHi = function () { }) {
    console.log(sayHi.name); // sayHi（生效了！）
}

f();
```

规范中把这种特性叫做「上下文命名」。如果函数自己没有提供，那么在赋值中，会根据上下文来推测一个。

### 属性“length”

```javascript
function fn1(a, b, c) { }

console.log(fn1.length);  // 3

function fn2(a,b,...rest) { }
console.log(fn2.length);  // 2 
```

由此可以知道length是除下rest参数下的参数的个数。（rest参数下面会讲到）

### 自定义属性

我们其实可以向函数添加属性，就像给对象添加属性一样。

就像下面这样我们添加了 counter 属性，用来跟踪总的调用次数：

```javascript
function sayHi() {
    console.log("Hi");
    // 计算调用次数
    sayHi.counter++;
}
sayHi.counter = 0; // 初始值
sayHi();
sayHi();
console.log(`Called ${sayHi.counter} times`);  // Called 2 times
```

我们现在是通过给函数添加属性来实现这个调用次数的功能，但是它有一个缺点，就是可以从外部访问到`say.counter`对其作出修改，但是这样往往是不好的，所以我们可以用一个技术来解决它，就是`闭包`。

 闭包这一部分理解起来是有难度的，由于时间关系，同学们课下自己去看。

### 箭头函数➡️（Arrow function）

一般箭头函数的结构像这样：

```javascript
(/*参数列表*/) => {
  /*
  函数体
  */
}
```

你会发现它是没有变量名，没有用`function`关键字来声明，但是多了个➡️`=>`，确实如此，使用的时候可以将它赋给一个变量去使用。

### 下面将一个传统的普通函数来改写成箭头函数。

先恰个🌰：

```javascript
// 传统
const fn = function(a){
  	return a
}
fn(1)   // 1

// 现在去掉function
const fn = (a) => {
  return a
}
fn(1)    // 1
```

#### 那我们能不能继续优化呢😎？   ==>  YES

**当函数接受的参数仅有一个时，**`**()**`**都可以省去，于是可以：**

```javascript
// 现在去掉 ()
const fn = a => {
  return a
}
fn(1)    // 1
```

**当函数体有且仅有一条返回语句，**`**{}**`**和return都可以省去**：

```javascript
// 现在去掉 {} 和 return
const fn = a => a
fn(1)    // 1
```

与原来的比较，现在是不是很简洁呢😊

#### 但是也要有注意事项哦

- 如果函数没有参数，括号（）不能省略

```javascript
const a = () => 1   // right
const a = => 1      // wrong
```

- 如果函数返回一个对象，则返回值用括号（）进行包裹

```javascript
const fn = () => ({name:'jack',age:18})   // right
const fn = () => {name:'jack',age:18}   	// wrong
```

- 当然箭头函数没有 `this`，没有 `arguments`，不能使用 `new` 进行调用，也没有 `super`（this下面会讲到一些）。

#### 更多栗子🌰：

```javascript
// ES6 之前
var list = [1, 2, 3, 4, 5, 6, 7]
var newList = list.map(function (item) {
    return item * item
})

// ES6 之后
const list = [1, 2, 3, 4, 5, 6, 7]
const newList = list.map(item => item * item)
```

### 递归

如果你不是刚接触编程，那么你可能已经很熟悉它了，那么你可以跳过这一章。

递归是一种编程模式，在一个任务可以自然地拆分成多个相同类型但更简单的任务的情况下非常有用。或者，在一个任务可以简化为一个简单的行为加上该任务的一个更简单的变体的时候可以使用。或者，就像我们很快会看到的那样，处理某些数据结构。

当一个函数解决一个任务时，在解决的过程中它可以调用很多其它函数。在部分情况下，函数会调用 **自身**。这就是所谓的 **递归**。

举个🌰：

简单起见，让我们写一个函数 `pow(x, n)`，它可以计算 `x` 的 `n` 次方。换句话说就是，`x` 乘以自身 `n` 次。

```javascript
pow(2, 2) = 4
pow(2, 3) = 8
pow(2, 4) = 16
```

-  使用for循环：  

```javascript
function pow(x, n) {
  let result = 1;

  // 在循环中，用 x 乘以 result n 次
  for (let i = 0; i < n; i++) {
    result *= x;
  }

  return result;
}

console.log(pow(2, 3)); // 8
```

-  使用递归： 
  比如，为了计算 `pow(2, 3)`，递归变体经过了下面几个步骤： 

```javascript
function pow(x, n) {
  if (n == 1)
    return x;
  else
    return x * pow(x, n - 1);
}

alert( pow(2, 3) ); // 8
```

1. 1. `pow(2, 3) = 2 * pow(2, 2)`
   2. `pow(2, 2) = 2 * pow(2, 1)`
   3. `pow(2, 1) = 2`

当然我们也可以用 ? : 与箭头函数的方式这样写

```javascript
const pow = (x, n) => (n == 1) ? x : (x * pow(x, n - 1));

console.log(pow(2, 3));  // 8
```

### 函数默认值：

```javascript
// ES6之前，如果我们写函数需要定义初始值的时候，需要这么写：
var config = (data) => {
    if(data === undefined) data = 'data is empty';
    return data
}

// ES6之后
const config = (data = 'data is empty') => data
```

### 函数的参数：

在 js 中，不会因为多传入参数或者少传入参数会出现报错的情况。

#### Arguments：

在ES6之前，我们获取函数参数的方式就只有一种，就是通过 arguments，我们可以尝试先把它打印一下

```javascript
const fn = function(){
	console.log(arguments)
	console.log(arguments.length);
	console.log(arguments[1]);
	console.log(arguments[0]);
}
fn(1,2,3,4,5);     
// [Arguments] { '0': 1, '1': 2, '2': 3, '3': 4, '4': 5 }
// 5
// 2
// 1
```

上面的arguments虽然可以获取length，也可以通过下标访问，也是可以迭代的，但是需要注意的是arguments是一个**类数组，**它不拥有数组的一些方法。但是我们可以利用Array.from()方法将arguments转为数组。那我们如果想操作参数怎么办呢？

这就要请出来ES6推出的 Rest 参数。

#### Rest 参数

Rest 参数可以通过使用三个点 `...` 并在后面跟着包含剩余参数的数组名称，来将它们包含在函数定义中。这些点的字面意思是“将剩余参数收集到一个数组中”。

用简单例子来看的话就是：

```javascript
const a = function (...args) {
    console.log(args)
}
a(1,2,3,4,5);      // [1,2,3,4,5]
```

再来个例子：

```javascript
const fn = function(...args) => args.reduce((pre,cur) => pre + cur);   // 计算传入参数的和

fn(1,2,3,4,5)    // 15
```

#### Spread 语法

spread 语法是展开运算符，可以把数组展开

```javascript
console.log(...[1, 2, 3]);     // 1 2 3
console.log(...'123456')       // 123456
```

#### 应用：

**复制或者修改数据：**

```javascript
const arr1 = [1,2,3];
const arr2 = [...a];
console.log(arr2)

const obj1 = {name:'小明',age:18};
const obj2 = {...obj1};
console.log(obj2)      // {name:'小明',age:18}
// 修改数据
const obj3 = {...obj1,name:'jack',gender:'man'};
console.log(obj3)      // { name: 'jack', age: 18, gender: 'man' }
```

**合并数据：**

```javascript
// ES6 之前
const a = [1,2,3];
const b = [1,5,6];
const c = a.concat(b);  // [1,2,3,1,5,6]

const obj1 = {
  a:1,
}
const obj2 = {
  b:1,
}
const obj = Object.assign({}, obj1, obj2); // {a:1,b:1}

// ES6 之后
const a = [1,2,3];
const b = [1,5,6];
// new Set()，用于数组去重
const c = [...new Set([...a,...b])]; // [1,2,3,5,6]

const obj1 = {
  a:1,
}
const obj2 = {
  b:1,
}
const obj = {...obj1,...obj2}; // {a:1,b:1}
```

**与结构赋值相结合（下面讲）**

```javascript
const arr = [1,2,3,4,5];
const [a,...arr2] = arr;
console.log(a);      // 1
console.log(arr2);   // [2,3,4,5]
```

## Object 

### 属性的简洁表示

```javascript
// 变量简洁表示
const a = 10;
const b = {a};
console.log(b);   // {a:10}

// 等同于
const c = {a:a};
console.log(c);  // {a:10}


// 方法的简洁表示
const dog = {
  speak(){
    console.log('wang wang');
  }
}

// 等同于 
const dog1 = {
  speak: function(){
    console.log('wang wang');
  }
}

dog.speak();   // "wang wang"
dog1.speak();  // "wang wang"
```

### 属性名表达式

```javascript
// 对象属性的定义
const stu = {};
stu.name = 'yang'; // 方法一
stu['age'] = 18;   // 方法二
console.log(stu) // { name: 'yang', age: 18 }

// 使用字面量定义，ES6之前，只能使用方法一进行,也就是不能让对象的key是一个变量
const stu2 = {
  name: 'jie',
  age: 18
}

// ES6之后允许我们通过方法二进行对象字面量的定义
const a = 'age';
const stu3 = {
  name: 'cao',
  [a]: 18
}
console.log(stu3); // { name: 'cao', age: 18 }

// 遍历输出
for(const i in stu3) {
  console.log(stu3[i]);
}   // cao 18
```

## this😊

或许有的同学会想到，如何在对象中定义方法获取到此对象中的其他属性呢？

例如这种：

```javascript
// 这里的 ??? 应该填写什么呢
const stu = {
  name: 'ying',
  getName() {
    console.log(???);  
  }
}

stu.getName();  // ying
```

这就要请出来js中大名鼎鼎的this了

或许你会说上面例子可以填写 `stu.name`，确实可以运行：

```javascript
const stu = {
  name: 'ying',
  getName() {
    console.log(stu.name);  
  }
}

stu.getName();  // ying
```

但是下面的例子就不对了：

```javascript
const stu1 = {
  name: 'mzy',
  getName(){
    console.log(stu1.name);
  }
}

const stu2 = {
  name: 'yang'
}

stu2.getName = stu1.getName;
stu2.getName();   // mzy
```

这样就会出现问题，如何解决呢  => 就要用到this

```javascript
const stu1 = {
  name: 'mzy',
  getName(){
    console.log(this.name);
  }
}

const stu2 = {
  name: 'yang'
}

stu2.getName = stu1.getName;
stu2.getName();   // yang
```

其实this不光用在对象之中，还可以用到函数中

上节课使用构造函数创建一个对象就用到了this

```javascript
function Person(name, age) {
    this.name = name
    this.age = age
    this.sayName = function () {
        console.log(this.name)
    }
    this.sayThis = function () {
        console.log(this);
    }
}
const p1 = new Person('BBH', 30)

p1.sayThis();  
/*
	Person {
  name: 'BBH',
  age: 30,
  sayName: [Function (anonymous)],
  sayThis: [Function (anonymous)]
}
*/

p1.sayName();  // BBH
```

这里使用new关键字就会把this绑定到Person身上，所以下面输出this.name才会是BBH

那我们普通的函数输出this会是什么呢，在浏览器中输出

```javascript
function fn() {
    console.log(this);
}
fn()  // window
```

这里打印会是window对象

我们不妨先在浏览器中输出一下this，发现输出`window`对象，是的，在浏览器中的顶层全局对象就是window

其实我们在声明一个函数的时候，默认会把window身上绑定这个方法，我们可以看一下

```javascript
function fn() {
    console.log(this);
}
fn()
debugger;   // 打个断点
```

![img](https://cdn.nlark.com/yuque/0/2022/png/22846415/1667194338826-b1cd0366-70ba-4483-a396-238be84ee6b7.png)

所以我们那里的`fn()`相当于`window.fn()`，所以输出`this`会是`window`对象。

这里其实就引出来this的指向问题，在 ES5 中，其实 this 的指向，始终坚持一个原理：**this 永远指向最后调用它的那个对象**，记住这句话，this 你已经了解一半了。这句话其实在前面的例子也有所论证。

所以就会有：

```javascript
const name = "windowsName";
const obj = {
    name: "Cherry",
    sayName() {
        console.log(this);
    }
}
obj.sayName();    // Cherry

const fn = obj.sayThis;
fn();  // <=> window.fn()  =>  window
```

但是其实箭头函数跟普通函数的this有所区别，this的指向问题一直是js基础里面一个比较难的点，由于时间限制，这里我讲的比较粗浅，大家可以多去看看相关的文章。

这里给大家推荐下这篇文章：<https://juejin.im/entry/6844903487721963533>或者<https://www.ruanyifeng.com/blog/2010/04/using_this_keyword_in_javascript.html>

## 变量的解构赋值

ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。

### 数组解构赋值

#### 基本用法

以前，赋值只能指定值

```javascript
const a = 1;
const b = 2;
const c = 3;
```

ES6之后允许我们这样写

```javascript
const [a,b,c] = [1,2,3];
console.log(a,b,c);    // 1 2 3
```

 上面代码表示，可以从数组中提取值，按照对应位置，对变量赋值。

本质上，这种写法属于“模式匹配”，只要等号两边的模式相同，左边的变量就会被赋予对应的值。下面是一些使用嵌套数组进行解构的例子。

```javascript
let [foo, [[bar], baz]] = [1, [[2], 3]];
foo // 1
bar // 2
baz // 3

let [ , , third] = ["foo", "bar", "baz"];
third // "baz"

let [x, , y] = [1, 2, 3];
x // 1
y // 3

let [head, ...tail] = [1, 2, 3, 4];
head // 1
tail // [2, 3, 4]

let [x, y, ...z] = ['a'];
x // "a"
y // undefined
z // []

// 交换值
let [a,b] = [1,2];
[a,b] = [b,a];
console.log(a,b);   // 2 1
```

但是下面就会报错

```javascript
// 报错
let [foo] = 1;
let [foo] = false;
let [foo] = NaN;
let [foo] = undefined;
let [foo] = null;
let [foo] = {};
```

#### 默认值

```javascript
let [foo = true] = [];
foo // true

let [x, y = 'b'] = ['a']; // x='a', y='b'
let [x, y = 'b'] = ['a', undefined]; // x='a', y='b'
```

需要注意的是：

ES6 内部使用严格相等运算符（===）（==与===什么区别？参考<https://juejin.cn/post/6844903456407289869>），判断一个位置是否有值。所以，只有当一个数组成员严格等于undefined，默认值才会生效。

```javascript
let [x = 1] = [undefined];
x // 1

let [x = 1] = [null];
x // null
```

### 对象解构赋值

#### 基本用法

```javascript
const per = {
    name: 'mzy',
    age: 18,
    address: {
      city: 'Chongqing'
    }
}

const { name, age } = per;  
console.log(name);  // mzy
console.log(age);   // 18


// 可以很方便地将现有对象的方法，赋值到某个变量。
let { sin, cos } = Math;

const { log } = console;
log('hello') // hello

// 嵌套
const {address: {city}} = per;
console.log(city); // Chongqing

// 起别名
const {address: {city : home}} = per;
console.log(home);  // Chongqing
```

#### 默认值

```javascript
const per = {
    name: 'mzy',
    age: 18,
    address: {
        city: 'Chongqing'
    }
}

const { name, age = 19, home = 'Henan' } = per;
console.log(name);  // "mzy"
console.log(age);   // 18
console.log(home);  // "Henan"
```

### 函数参数的解构

```javascript
const fn = ({ a, b }) => {
    console.log(a);
    console.log(b);
}

const fn2 = ([a, b]) => {
    console.log(a);
    console.log(b);
}

fn({ c: 18, b: 20 })  // undefined 20
fn({ a: 18, b: 20 })  // 18 20

fn2([1, 2])  // 1 2
```

## js内存管理

像 C 语言这样的底层语言一般都有底层的内存管理接口，比如 malloc()和free()。相反，JavaScript 是在创建变量（对象，字符串等）时自动进行了分配内存，并且在不使用它们时“自动”释放。释放的过程称为垃圾回收。

### [内存生命周期](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Memory_Management#%E5%86%85%E5%AD%98%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F)

不管什么程序语言，内存生命周期基本是一致的：

1. 分配你所需要的内存
2. 使用分配到的内存（读、写）
3. 不需要时将其释放\归还

所有语言第二部分都是明确的。第一和第三部分在底层语言中是明确的，但在像 JavaScript 这些高级语言中，大部分都是隐含的。

### [JavaScript 的内存分配](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Memory_Management#javascript_%E7%9A%84%E5%86%85%E5%AD%98%E5%88%86%E9%85%8D)

#### 值的初始化

为了不让程序员费心分配内存，JavaScript 在定义变量时就完成了内存分配。

```javascript
const n = 123; // 给数值变量分配内存
const s = "azerty"; // 给字符串分配内存

const o = {
  a: 1,
  b: null
}; // 给对象及其包含的值分配内存

// 给数组及其包含的值分配内存（就像对象一样）
const a = [1, null, "abra"];

function f(a){
  return a + 2;
} // 给函数（可调用的对象）分配内存
```

### [使用值](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Memory_Management#%E4%BD%BF%E7%94%A8%E5%80%BC)

使用值的过程实际上是对分配内存进行读取与写入的操作。读取与写入可能是写入一个变量或者一个对象的属性值，甚至传递函数的参数。

### [当内存不再需要使用时释放](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Memory_Management#%E5%BD%93%E5%86%85%E5%AD%98%E4%B8%8D%E5%86%8D%E9%9C%80%E8%A6%81%E4%BD%BF%E7%94%A8%E6%97%B6%E9%87%8A%E6%94%BE)

大多数内存管理的问题都在这个阶段。在这里最艰难的任务是找到“哪些被分配的内存确实已经不再需要了”。它往往要求开发人员来确定在程序中哪一块内存不再需要并且释放它。

高级语言解释器嵌入了“垃圾回收器”，它的主要工作是跟踪内存的分配和使用，以便当分配的内存不再使用时，自动释放它。这只能是一个近似的过程，因为要知道是否仍然需要某块内存是[无法判定的](http://en.wikipedia.org/wiki/Decidability_%28logic%29)（无法通过某种算法解决）。

### ♻️垃圾回收

对于开发者来说，JavaScript 的内存管理是自动的、无形的。我们创建的原始值、对象、函数……这一切都会占用内存。

当我们不再需要某个东西时会发生什么？JavaScript 引擎如何发现它并清理它？

#### 可达性

JavaScript 中主要的内存管理概念是**可达性**。

简而言之，“可达”值是那些以某种方式可访问或可用的值。它们一定是存储在内存中的。

1.  这里列出固有的可达值的基本集合，这些值明显不能被释放。
   比方说： 

- - **当前函数的局部变量和参数**
  - 嵌套调用时，当前**调用链上所有函数的变量与参数**
  - **全局变量**
  - （还有一些内部的）

这些值被称作 **根（roots）**。

1.  如果一个值可以通过引用或引用链从根访问任何其他值，则认为该值是可达的。
   比方说，如果全局变量中有一个对象，并且该对象有一个属性引用了另一个对象，则 **该** 对象被认为是可达的。而且它引用的内容也是可达的。 

这里是一个最简单的例子：

```javascript
// user 具有对这个对象的引用
let user = {
  name: "John"
};
```

![img](https://cdn.nlark.com/yuque/0/2021/png/2695465/1636187034953-1c55442a-3204-4a0a-a7f4-aeddd6fa1f2d.png)

这里的箭头描述了一个对象引用。全局变量 `"user"` 引用了对象 `{name："John"}`。

如果 `user` 的值被重写了，这个引用就没了：

```javascript
user = null;
```

![img](https://cdn.nlark.com/yuque/0/2021/png/2695465/1636187053477-23a4434d-8200-4c78-b2ea-532a44537018.png)

现在 John 变成不可达的了。因为没有引用了，就不能访问到它了。垃圾回收器会认为它是垃圾数据并进行回收，然后释放内存。

现在，我们把 `user` 的引用复制给 `admin`：

```javascript
// user 具有对这个对象的引用
let user = {
  name: "John"
};

let admin = user;
```

![img](https://cdn.nlark.com/yuque/0/2021/png/2695465/1636187072001-5ed7b883-ff70-4df0-bdb6-d3a6ad3bd8ea.png)

现在如果执行刚刚的那个操作：

```javascript
user = null;
```

![img](https://cdn.nlark.com/yuque/0/2021/png/2695465/1636187087767-ffc491d9-49a4-433f-9adf-767e1f3a05fc.png)

然后对象仍然可以被通过 `admin` 这个全局变量访问到，所以对象还在内存中。

------

在 JavaScript 引擎中有一个被称作 [垃圾回收器](https://en.wikipedia.org/wiki/Garbage_collection_(computer_science)) 的东西在后台执行。它监控着所有对象的状态，并删除掉那些已经不可达的。