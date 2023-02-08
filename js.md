## 二、进入JavaScript的世界 😁

### 2.1 JavaScript世界的规则

（谈朋友之前，还要清楚别个的喜好和底线不是）

#### 2.1.1 区分大小写

ECMAScript中的一切都区分大小写，无论是变量、函数名还是操作符，我们在**命名时应当有意去进行大小写区分**，如构造函数名的首字母和类名的首字母习惯大写等等。

#### 2.1.2 标识符的规范

标识符就是变量、属性或者函数的名称。标识符可以由一个或多个下列字符组成：

- - 第一个位置上必须是字母、下划线（_）或美元符号（$）。
  - 剩下其他的字符无特殊要求

在JavaScript的世界里，长串的标识符使用**驼峰命名法**来进行命名更为推荐，即第一个单词的首字母小写，后面每个字母的首字母大写，如：firstDay、myCar...

同时关键字（如break、typeof、instanceof、new...）、保留字（public、private、let...）、true、false和null都不能作为标识符

#### 2.1.3 注释

Javascript 注释的语法和 C++ 或许多其他语言类似：

```javascript
// 单行注释

/* 这是一个更长的，
   多行注释
*/

/* 然而，你不能，/* 嵌套注释 */ 语法错误 */
```

**tips：vscode中鼠标选中要注释的代码，同时按住CTRL和 ？ 即可一键注释（部分编译器可能不同）**

#### 2.1.4 严格模式

JavaScript的世界整体来说语法还是比较松散的，但是进入严格模式之后，对语法的限制就变得更加严格。

进入严格模式的方法就是在脚本的开头写上：

```javascript
'use strict';
```

在严格模式下，不规范的写法会被拦截并处理，对于不安全的活动将会抛出错误，会影响JavaScript执行的很多方面。

比如下面的代码，在没有开启严格模式下，不会报错

```javascript
function foo() {
    test = 123;
}
foo();  
console.log(test);  
```

但是，严格模式静止创建全局变量，而不显示的声明他们

```javascript
function foo() {
  	'use strict';
    test = 123;
}
foo();  
console.log(test);  //ReferenceError: test is not defined
```

#### 2.1.5 结尾分号

JavaScript的世界中，所有的语句都以分号结尾。虽然分号结尾不是必须，就算不写分号解析器也会自己确定语句在哪里结尾并隐式补上分号，但是却**强烈建议遵守这个语法**。原因如下：

- - 部分情况不加分号代码可能会和本意有出入。
  - 多条语句写在同一行不加分号会报错

使用分号的好处在于：

- - 加上分号可以避免很多错误，开发人员可以放心的通过删除多余的空格来压缩代码；
  - 加上分号在某些情况下可以增进代码的性能，因为这样解析器就不用花多余的时间去推测在哪里添加分号了。

### 2.2  声明变量 

提到JavaScript就要提到JavaScript变量声明三兄弟啦 👨‍👦‍👦 ，分别是 **var****、****let****、****const****。**

#### var 

1.声明一个变量，**可选**初始化一个值。在变量未赋值的情况下，变量会默认保存一个特殊类型的数据 undefined。

```javascript
var testOne = 'bbh';
var testTwo;

console.log(testOne); // bbh 
console.log(testTwo); //undefined
```

2.使用var时，变量的声明会自动提升到作用域的顶部。值得注意的是，只是变量的声明被提升到作用域的顶部了呦。让我们通过下面的例子理解一下

```javascript
function foo(){
	console.log(age);  //undefined
  var age = 20;
}
foo();
```

很奇怪是不是？不是说好了，会变量提升的吗 😵 ，原因是因为。提升的只有变量，而没有赋值操作，所以上面的代码等价于下面的代码，amazing！💪

```javascript
function foo() {
    var age;
    console.log(age);  //undefined
    age = 20;
}
foo();
```

#### let

let和var的作用差不多，都是用于声明变量，但是有几点主要的区别。

1.**let声明的范围是块级作用域，而var声明范围是函数作用域**

森莫意思捏？

```javascript
function foo() {
    if (true) {
        var name = 'BBH';
        console.log(name);  //BBH
    }
    console.log(name);  //BBH
    if (true) {
        let age = 30;
        console.log(age);  //30
    }
    console.log(age);//Uncaught ReferenceError: age is not defined
}
foo();
```

2.**使用let不能重复声明同一变量，而var可以**

```javascript
var name = 'Billy';
var name = 'Lucy';
var name = 'Jack';
let age = 18;
let age = 21;
console.log (age);  //Uncaught SyntaxError: Identifier 'age' has already been declared
```

3.**全局作用域中，let创建的变量不会加在window对象身上，而var会**

```javascript
var name = 'BBH';
let age = 30;
console.log (window.name);  //BBH
console.log (window.age);  //undefined
```

#### const

const和let基本相同，有一个重要的区别就是变量必须初始化，并且修改使用const声明的变量的值会报错。

```javascript
const age = 26;
age = 36;  //Uncaught TypeError: Assignment to constant variable.

const name;  //Uncaught SyntaxError: Missing initializer in const declaration
```

使用const声明的变量一定是个常量，常量的值不可修改。

#### 推荐的声明风格 

1.不推荐使用 var 

三兄弟中的var是年龄最大的一个 👴，在ES6之前只有它一个人来做变量声明的活，但是由于年代悠久，行为怪异，使得JavaScript社区苦恼了很多年。你想由于var可以重复声明同一个变量，那如果当你写了一段很长的代码，你忘记了上面自己声明了哪些变量，所以你在下面又用var声明了同一个变量，这可能会对你代码的功能有所影响。拥有明确作用域和声明位置的let和const两兄弟👬显然更受开发者喜爱。

2.const 优先、let次之

使用const声明可以让浏览器运行时保持变量不变，改变时会报错，这样就能让分析工具提前发现不合法的赋值操作。因此应当优先使用const来声明变量，只有提前知道未来会修改变量时才使用let。

### 2.3 数据类型 

最新的 ECMAScript 标准定义了 8 种数据类型：分别是7中基本数据类型：Undefined、Null、Boolean、Number、string、Symbol和BigInt，还有一种引用数据类型Object。

相比于其他编程语言中五花八门的数据类型来说，JavaScript数据类型相对来说比较少，但是通过他们你可以在程序中开发有用的功能。对象 Object 和 function 是这门语言的另外两个基本元素。你可以把对象当作存放值的一个命名容器，然后将函数当作你的程序能够执行的步骤。

#### 2.3.1 undefined 

undefined，字面意思就是没有定义，很好理解。Undefined这个类型只有一个值，就是undefined。（Undefined以类型出现，首字母大写，以值出现不用，后面的数据类型同理）

当使用var和let声明了变量而不初始化时，相当于默认给变量赋予了undefined。

```javascript
let test;
console.log(test) //undefined
```

#### 2.3.2 Null

Null这个类型也只有唯一值null。null值表示一个空对象，使用typeof进行类型检测null时，会返回object也就可以这么理解（但是事实上这是一个从JavaScript第一版一直遗留下来的bug🐛，基本数据类型是不应该返回引用数据类型这个结果的）。

```javascript
let name = null;
console.log(typeof name); // object
```

Null有一个重要的作用，在定义将要保存对象值的变量时，可以先设置为null，null表示一个空对象（前面提到过），这样只要检查这个变量的值是不是null就可以知道这个变量有没有被重新赋予一个新对象的引用。

#### 2.3.3  Boolean

Boolean有两个字面量：true和false。Boolean在js中使用非常频繁

#### 2.3.4 Number

数字（Number），整数或浮点数

```javascript
let num1 = 1;
let num2 = 2.2;
```

有一个特殊的数值是NaN，表示"Not a Number"，字面意思就是不是数值，用来表示本来要返回数值的操作失败了的返回值。

```javascript
console.log(0/0)  //NaN
```

#### 2.3.5 String

String数据类型表示多个16位Unicode字符序列。可以使用双引号(" ")、单引号(' ')或者反引号(` `)都是合法的。

```javascript
const name = "Billy";
const val = 'test';
const gender = `male`;
```

但是注意不要混合使用哦 👋

字符串是不可变的，一旦创建了，**它的值就不会再改变**，若要修改这个变量的字符串值，就会先销毁原始字符串，再保存新值。

##### **模板字符串**

ES6中新增加了**模板字符串**的使用，这意味着字符串变得更加的灵活。模板字符串使用反引号 (``) 来代替普通字符串中的双引号和单引号，并可用**${}**将变量或表达式括起来。

模板字符串有两个非常重要的作用：

1.实现多行字符串

使用传统的方法我们要拿到多行字符串需要使用换行符 \n，而使用模板字符串就能够不用换行符，直接手动换行就能拿到多行字符串。我们看下面的代码：

```javascript
//传统方法打印多行字符串
console.log('string text line 1\n' + 'string text line 2');
//使用模板字符串输出多行字符串
console.log(`string text line 1
string text line 2`);
```

结果是一样的

![img](https://cdn.nlark.com/yuque/0/2021/png/21538792/1635561272837-8d219658-02c5-4307-8c75-3a08d21bcfd5.png)

2.插入表达式

按照传统的方法，要插入表达式我们需要使用字符串的拼接，而使用模板字符串的**${}**就能将变量直接插入其中，非常好用。🤘

```javascript
let a = 1;
let b = 2;
//两种方法结果都是一样的。
console.log ("a+b="+(a+b));  //a+b=3
console.log (`a+b=${a+b}`);  //a+b=3
```

#### 2.3.6 Object

ECMAScript中的对象是一组数据和功能的集合。对象通过new操作符后跟对象类型的名称创建。

创建对象有五种方法：

1. 1. 使用new操作符进行创建
   2. 使用对象字面量的方式创建
   3. 构造函数方式创建
   4. 工厂模式创建
   5. Object.create()方式创建

对象的知识在JavaScript的世界中非常重要，我们会在后面展开详细叙述。

### 2.4 变量 & 作用域

相比于其它语言，在JavaScript的世界中，变量是松散的，因此变量也不过只是一个特定称谓的名字。由于没有规则定义变量必须包含什么数据类型（像c语言就需要），所以你想让变量在任何时候变成任何元素都没有关系，这样对于开发者而言很轻松，也很危险。

一套设计良好的规则来储存变量，并且之后可以方便找到这些变量，这个规则被称为作用域，Js采用**词法作用域**即（**静态作用域**）

#### 2.4.1 原始值与引用值

ECMAScript中变量分为两类：**原始值**和**引用值**。原始值就是简单的数据（基本数据类型），而引用值就是由多个值构成的对象（引用数据类型）。

值得注意的是，保存原始值的变量是按值访问的，我们操作的就是存储在内存中的实际值，而保存引用值的变量是**按引用访问**的。学过c++等类似其他编程语言的同学可能会有疑问，访问对象不是应该访问的是地址吗？原因在于，**在JavaScript的世界中，禁止我们直接访问内存地址**，因此也不能直接操作对象所在的内存空间。

#### 2.4.2 复制值

原始值与引用值在通过变量赋值时也有所不同。

##### 2.4.2.1 原始值的复制

在将一个原始值赋值于另一变量时，原始值会被复制到新变量的位置，会在栈内新开辟一块内存，这两个变量完全独立，互不干扰。

```javascript
let num1 = 1；
let num2 = num1;
```

在内存中的变化过程如图：

![img](https://cdn.nlark.com/yuque/0/2021/png/21538792/1635171778654-f60ecf1a-46c0-4c3e-bd53-c335af09c403.png)

##### 2.4.2.2 引用值的复制

但是在将一个变量的引用值赋值给另一变量时，存储在变量中的值也会被复制到新变量所在的位置，不同的在于，复制的值是一个指向原变量的指针，因此两个变量实际上指向同一个对象。当一个对象发生改变时，另一个对象也会发生变化。

```javascript
// 对象字面量新建一个空对象
let obj1 = new Object();
let obj2 = obj1;
obj1.name = 'BBH';
console.log (obj2.name);  //BBH
```

我们明明修改的是obj1啊，为什么obj2也随之改变了呢 😩，下面这张图可以帮助我们更好的理解 🧐

![img](https://cdn.nlark.com/yuque/0/2021/png/21538792/1635172302802-c65bd15d-54a0-4bb8-849e-3183975e80f5.png)

#### 2.4.3 不一样的参数传递

ECMScript中所有函数的参数都是按值传递的。这一位置函数外的值会被复制带函数内部的参数中。

按值传递，值是直接复制到形参之中，而按引用传递参数，值在内存中的位置会保存在形参之中，因此函数内部的变化会影响到函数外部的变化（因为内外变量都指向同一个内存地址），这在JavaScript的世界里是不可能的，我们看下面的例子。

```javascript
function foo(num){
  num = 10;
  console.log(num);
}
let num = 0;
console.log(num); //0
foo(num);//10
console.log(num);//0
  
```

通过上面的例子我们就可以看出来，传递的其实是值

但我们再看看下面这个例子

```javascript
function foo(obj){
  obj.name = 'BBH';
}
let person = new Object();
foo(person);
console.log(person.name);//BBH
```

我们不是说了“ECMScript中所有函数的参数都是按值传递的”吗？为什么在函数内部修改obj的name值，外部的person也会随之改变呢？🤔 

稍安勿躁，让我们看看下面的代码

```javascript
function foo(obj){
  obj.name = 'BBH';
  obj = new Object();
  obj.name = 'K';
}
let person = new Object();
foo(person);
console.log(person.name);//BBH
```

当我把 person 传进去的时候，实际是传递了“指针”(就是它的内存地址)这个值 ，并不是person 本身。那么传进foo函数是 person和obj 拥有相同内存地址（它们都指向了同一个对象），因此改变了 obj.name的值就是改变了person.name 的值。当 obj 赋于一个新的内存地址的时候 ，obj的内存地址就和person的内存地址不是同一个了，因此改变了obj.name的时候 person,name是不会改变的。

大家下去可以再理解一下😬

#### 2.4.4 变量们的作用域

什么是作用域呢？简单来说，作用于就是一个变量的作用范围，使用作用于可以防止内吨泄露，命名冲突等种种问题。我们需要牢记的一点就是：

**内层作用域可以访问外层作用域的变量，外层作用域不能访问内层作用域。**

```javascript
function test(){
    const a = 'inner';
}
console.log (a);  //Uncaught ReferenceError: a is not defined
```

显然外层不能读取到函数内部变量，目前它在函数作用域中的变量是私有的，不会内存外泄。当然要读取到它也可以通过闭包等方法获取。

作用域的最主要作用就是**隔离变量**，在不同的作用域下同名变量不会有冲突。

tips:另一个重要概念是执行上下文，执行上下文就是js被执行和解析时的环境，作用域和执行上下文这俩概念容易混淆。主要区别在于**作用域在解释阶段确定的，不会改变；执行上下文在运行阶段确定的，随时可能改变。**

##### 2.4.4.1 全局，函数和块级作用域

作用域可以分为**全局作用域**、**函数作用域**和**块级作用域**。

### 2.5  Object 续集 🧐

#### 2.5.1 创建一个对象

还在为单身而苦恼吗？不用担心，相信通过本次内容的学习，你会自己new一个理想中的对象的！

##### 2.5.1.1 使用Object( )构造函数

```javascript
let obj = new Object();
obj.name = 'BBH';
obj.age = '30';
console.log(obj); // {name:'BBH', age:'30'}
```

##### 2.5.1.2 使用对象字面量

```javascript
let obj = {
    name: 'BBH',
    age: '30'
}
console.log(obj); // {name:'BBH', age:'30'}
```

##### 2.5.1.3 使用构造函数创建一个对象

```javascript
function Person(name, age) {
  this.name = name
  this.age  = age
  this.sayname = () => {
    console.log(this.name)
  }
}
const p1 = new Person('BBH', 30)
const p2 = new Person('star', 19)
```

ECMScript中的构造函数是用于创建特定类型对象的，如Object和Array这样的原生构造函数，可以直接使用。当然使用像上面案例中的自定义构造函数也是很常见的。

**PS**：构造函数和普通函数的唯一区别就是调用他们的方式不同：任何函数，只要通过new操作符调用就是构造函数，反之就是普通函数。

###### 使用new创建新的实例历程

1. 创建一个新对象
2. 将构造函数的作用域赋给新对象
3. 执行构造函数中的代码
4. 返回新对象

------

上面是三种较为常用的创建一个对象的方法，下面我们在介绍其他几种方法，课上不做讲解，大家可以课下看一下课件

##### 2.5.1.4 使用工厂模式

```javascript
function Person(name, age) {
  const obj = {}
  obj.name = name
  obj.age = age
  return obj
}

const person = Person('BBH', 30)
const person1 = Person('star', 19)
console.log(person instanceof Person) // -> false
console.log(person1.__proto__ == person.__proto_) // -> false
```

通过输出我们可以看到，通过构造函数创建的对象，我们没有办法解决对象识别的问题 

**工厂模式和构造函数的不同之处**

1. 构造函数没有显示的创建一个对象
2. 构造函数直接将属性和方法赋给this对象（就是正在新建的这个对象）
3. 构造函数没有return语句
4. 虽然构造函数解决了对象识别的问题，但是就像工厂模式一样，每个方法都会在每个实例中重新创建一遍。我们可以把函数定义转移到构造函数外部来解决这个问题，但是这样就没有封装性可言了。

##### 2.5.1.5 使用原型模式

**或许大多数人还没有接触原型这个概念，所以这种方法先不着急去使用，可以理解了原型后在拐回来看这个方法也不迟 😁**

我们创建的每个函数都有一个prototype属性，这个属性是一个指针，指向一个对象，而这个对象的用途是包含可以由特定类型的所有实例共享的属性和方法。

**PS**：JS中万物皆对象，但分为两大类：普通对象和函数对象。所有的函数对象都有一个prototype属性，普通对象是没有prototype属性的，只有_proto_。

```javascript
function Person() {
    Person.prototype.name = "BBH";
    Person.prototype.age = 30;
    Person.prototype.sayName = function () {
        console.log(this.name);
    }
}

let person = new Person();
person.sayName();//BBH
console.log(person.name)//BBH
```

原型模式虽然解决了构造函数每个方法都会在每个实例中重新创建一遍的问题。但是所有实例在默认情况下都取得了相同的属性值，实例一般都是要有属于自己的全部属性的。

------

其实创建对象不单单可以使用一种方法，可以使用以上方法进行组合后，去创建一个新对象

#### 2.5.2 对象属性的增改查

##### 属性添加

1. 使用点 . 语法

```javascript
let obj = {
    name:'BBH',
    age:30
}
obj.gender = 'male';
console.log (obj);  //{name: 'BBH', age: 30, gender: 'male'}
```

1. 使用中括号[]

```javascript
let obj = new Object();
obj['name'] = 'BBH';
console.log (obj);  //{name: 'BBH'}
```

开发人员在动态添加对象属性的时候，更倾向于使用点方法，因为它更简单。但是如果遇到需要使用非字符串的数据作为属性的话，就只能选择中括号语法。中括号中可以穿任何类型的数据，甚至传递一个对象都是合法的。因为传递的数据会被toString()方法进行转换。

```javascript
let a = 'name'
let b = 1; 
let c = {
    name:"test"
}
let obj = new Object();
obj[a] = 'Billy';
obj[b] = 'test1';
obj[c] = 'test2';
console.log (obj);  //{1: 'test1', name: 'Billy', [object Object]: 'test2'}
```

##### 属性修改

通过**点语法**和**中括号**同样能够实现属性的修改。 

```javascript
let obj = {
    x:1,
    y:2
}
obj.y = 10;
obj['x'] = 10;
console.log (obj);  //{x: 10, y: 10}
```

**PS:**要修改的前提是这个属性原本存在，如果原本不存在那么就是实现的添加属性的操作。

##### 属性查找

仍然是通过点语法和中括号语法。

```javascript
let obj = {
    x:1,
    y:2
}
console.log (obj.y);  //2
```

虽然本节课讲的主要是点语法和中括号语法，但是增删改查的方法远不止这些，还有Object.getOwnPropertyNames()、Object.keys()、Object.getOwnPropertyDescriptor()等等方法，这些都等着我们在后面的学习中进行深入的探索。

#### 2.5.3 Object的两个儿子👨🏼‍🤝‍👨🏼

typeof 可以用来进行数据类型检测，我们在使用typeof进行数据类型检测时，除了基本数据类型会返回基本数据类型的结果，按照前面我们所提到的，难道除了其中7种基本数据类型之外，其他的都返回Object吗，漏漏漏！在检测Function时，它是独立的，虽然都是Object

```javascript
//  基本数据类型
const num = 1;
let flag = true;
const str = 'string';
const u = undefined;
const n = null;
const s = Symbol();
const big = BigInt('99999999999999');
// 引用数据类型
let obj = {

}
// 创建一个函数
function test(){
    
}
// 创建一个数组
const arr = [];

console.log (typeof num);  //number
console.log (typeof flag);  //boolean
console.log (typeof str);  //string
console.log (typeof u);  //undefined
console.log (typeof n);  //object  （版本遗留问题）
console.log (typeof s);  //symbol
console.log (typeof big);  //bigint

console.log (typeof obj);  //object
console.log (typeof test);  //function
console.log (typeof arr);  //object
```

函数是一个对象，毋庸置疑，但是返回的结果却是function，这是因为函数属于对象子类型。在JavaScript的世界中，除了Function，还有另一个对象子类型，就是数组(Array)。

```javascript
const arr = [];
console.log (arr instanceof Array);  //true
```

显然数组也是有自己的类型的，因此这两种类型（Function和Array）都是对象子类型，我们可以把它们称为Object的儿子们。下面我们会详细介绍它们。

#####  数组

数组是一组有序的数据，在JavaScript的世界中，数组可以存储任何类型的数据且数组可以动态添加，自动增长（太舒服辣）。

###### 1 创建数组

创建数组的常见方法有三种

1. 使用构造函数Array( )

```
let animals = new Array(3);  //创建一个包含三个元素的数组
let cars = new Array('benz','BMW');  //创建一个包含两个元素的数组，分别保存字符串benz和BMW
```

1. 使用数组字面量

```javascript
let arr = ['benz','BMW',1,2,3];
```

1. 最后一种方式是使用ES6新增的方法from()来创建

```javascript
let arr = ['benz','BMW',1,2,3];
let copyArr = Array.from(arr);
console.log (copyArr);  //['benz', 'BMW', 1, 2, 3]
```

可以看出，使用Array.from()实际上是通过传入一个可迭代对象或类数组，对一个可迭代对象执行浅复制来创建的，这种创建对象的方式不太常用。

###### 2 数组空位

使用数组字面量初始化数组时，可以使用一串逗号来创建空位。

```javascript
let a1 =[,,,,,];
console.log(a1.length);  //5
console.log(a1[0]);  //undefined
```

在JavaScript的世界中，这种空位是被认可为存在的元素的，只不过值为undefined。

###### 3 数组索引

要取得或设置数组的值，需要使用中括号并提供数组的索引。

```javascript
let arr = ['red','yellow','blue'];
console.log (arr[1]);  //yellow
```

中括号中提供的索引表示要访问的对应的值。值得注意的有两点：

1. 是数组索引在读取和设置时都是从0开始的，这一点对于很多第一次学习编程语言的同学来说会很不习惯，但是在其他编程语言如c、c++里面都是一样的。
2. 是如果写入的索引超过了数组的最大索引，那么数组长度会自动扩展到索引的位置，不会报错。这一点和别的编程语言就不同了。

```javascript
let arr = ['red','yellow','blue'];
console.log (arr[10]);  //undefined
arr[0] = 'black;
console.log(arr)  //['black', 'yellow', 'blue']
```

数组中的元素的数量保存在length属性中。

```javascript
let arr = ['red','yellow','blue'];
console.log(arr.length);  //3
```

使用length有个小技巧，就是通过它可以向数组末尾添加元素。

```javascript
let arr = ['red','yellow','blue'];
arr[arr.length] = 'black';
console.log(arr);  //['red', 'yellow', 'blue', 'black']
```

###### 4 检测数组

检测数组可以通过instanceof操作符和isArray()方法来检测。

```javascript
let arr = ['red','yellow','blue'];
console.log (arr instanceof Array);  //true
console.log (Array.isArray(arr));  //true
```

###### 5 数组方法（重要）🤜🤛

前面提到过，前端的核心工作就是处理数据，渲染数据，因此对于数组中数据的熟练处理至关重要，要处理这些数据，就必须要用到数组的方法（api）。

- - **数组元素的增删**

- - - push：向数组末尾添加一个或多个元素，并返回数组的新的长度。

- - - - 语法：**arr.****push(insertData1, insertData2, ......)**

- - - pop：删除数组末尾的最后一个元素，并将被删除元素作为返回值返回。

- - - - 语法：**arr.pop()**

- - - shift：删除数组开头一个元素，并返回新的数组长。

- - - - 语法：**arr.shift()**

- - - unshift：向数组开头添加一个或多个元素。

- - - - 语法：**arr.****unshift(insertData1, insertData2, ......)**

 

```javascript
let arr = ['red','yellow','blue'];
//向末尾添加元素last
arr.push('last');
//向开头添加元素first
arr.unshift('first');
console.log (arr);  //['first', 'red', 'yellow', 'blue', 'last']
//删除末尾元素last
arr.pop();
//删除开头元素first
arr.shift();
console.log (arr);  //['red', 'yellow', 'blue']
```

- - **数组的循环**

- - - forEach()  用于代替普通for循环的方法，但是用起来比for循环更方便。

- - - - 语法：**arr.forEach(callback);**
      - callback默认有三个参数，分别为遍历的值，索引，数组自身。

- - - map()  同样是用于实现数组的循环的，但是相比于forEach更常用。它们之间的主要区别在于是否有返回值，我们会希望使用 map 来制作一个新的数组，而使用 forEach 映射到数组上。

- - - - 语法：**arr.map(callback);**
      - callback默认有三个参数，分别为遍历的值，索引，数组自身。

- - - filter()  用于过滤一些不合格“元素”， 如果回调函数返回true，该元素就留下来。

- - - - 语法：**arr.filter(callback);**
      - callback默认有三个参数，分别为遍历的值，索引，数组自身。

- - - reduce()  可以用来计算数组的和或者阶层。

- - - - 语法：**arr.reduce(callback);**
      - callback默认有三个参数，分别为累加器，当.前遍历的元素，索引。

- - - find()  找到第一个符合条件的数组成员，如果没有找到，返回undefined

- - - - 语法：**arr.find(callback);**
      - callback默认有三个参数，分别为遍历的值，索引，数组自身。

- - - ...

```javascript
/**
 * forEach
 */
let arr = ['red','yellow','blue'];
arr.forEach(function(val, index, arr){
    console.log(val, index, arr);
});
//arr中有三个元素，循环三次，方法内传入的回调可以设置三个参数，遍历的值、索引、和遍历的数组。
//red 0 (3) ['red', 'yellow', 'blue']
//yellow 1 (3) ['red', 'yellow', 'blue']
//blue 2 (3) ['red', 'yellow', 'blue']

/**
 * map
 */
arr.map((item, index, arr)=>{
    console.log (item, index, arr);
})
//map和forEach几乎一样，但是map在开发中更常见
//red 0 (3) ['red', 'yellow', 'blue']
//yellow 1 (3) ['red', 'yellow', 'blue']
//blue 2 (3) ['red', 'yellow', 'blue']

/**
 * filter
 */
const res = arr.filter((val)=>{
    return val === 'red'
})
console.log (res);
//通过判断条件过滤出数组中符合条件的项并以数组形式返回
//['red']

/**
 * reduce
 */
let res = arr.reduce((total, cur, index) =>{
    return total+cur;
});
console.log (res);
//reduce作为参数的回调函数中可以设置累加器，当前遍历的元素，和索引三个参数，使用reduce可以实现用来计算数组的和或者阶层。
//reduce和react中的redux有异曲同工之妙，建议在学习redux之前一定要将reduce理解透彻
//打印的结果做了一个字符串的拼接，就为：
//redyellowblue

/**
 * find
 */
let res = arr.find((item)=>{
    return item === 'red';
})
console.log (res);
//和filter不同，find方法只会返回匹配的值，所以值为：
//red
```

- - **数组元素的截取**

- - - slice()  可从已有的数组中返回选定的元素。

- - - - **语法：arr.slice(startIndex, endIndex)**
      - slice方法不会改变原数组，会将截取到的新数组返回。

- - - splice()  强大的api，可以实现数组元素的插入、删除、替换。

- - - - **语法：arr.splice(****start,num,data1,data2,...****)**
      - 值得注意的是，和slice不同，splice会直接对原数组造成影响，并且传入的参数的意义也完全不同。需要我们进行区分。
      - slice的第一个参数为截取数组的起始位置索引，第二个参数为结束位置的索引，而splice的第一个参数为截取数组的起始位置索引，第二参数为删除的数量，后面的参数为添加的元素。

```javascript
let arr = ['red','yellow','blue','black','blue'];
console.log (arr.slice(1,3));  //['yellow', 'blue'];
arr.splice(1,3);
console.log (arr);  //['red', 'blue']

//使用splice实现插入
let arr2 = [1,2,3,4,5];
//splice的第一个槽位插入数组末尾的索引（这个位置我们用来准备插入元素），接着第二个
//槽位设置为0，表示删除0个元素，第三个参数设置为数组索引+1作为插入值插入。
arr2.splice(arr2.length,0,arr2.length+1);
console.log (arr2);  //[1, 2, 3, 4, 5, 6]

//使用splice实现删除
arr2.splice(arr2.length-1,1);
console.log (arr2);  //[1, 2, 3, 4, 5]

//使用splice实现替换
arr2.splice(arr2.length-1,1,'add');
console.log (arr2);  //[1, 2, 3, 4, 'add']
//删除掉元素然后再在这个位置插入新元素就可以做到替换
```

- - **数组的拼接**

- - - concat()  用于实现一个或多个数组的拼接

- - - - 语法：**arr1.concat(arr2);**

```javascript
let arr1 = [1,2,3];
let arr2 = [4,5,6];
console.log (arr1.concat(arr2));  //[1, 2, 3, 4, 5, 6]
```

- - **数组转字符串**

- - - join()  将数组中的所有元素放入一个字符串，并返回这个字符串。

- - - - 语法：arr.join('可选字符串');
      - join方法中的参数是有可选的，不设置则默认以 , 隔开，设置了就以设置的字符串隔开

```javascript
let arr1 = [1,2,3];
let arr2 = [4,5,6];
// console.log (arr1.concat(arr2));
console.log (arr1.join());  //1,2,3
console.log (arr2.join('@'));  //4@5@6
```

- - - toString()	  将数组中所有元素都放入一个字符串并返回这个字符串。

- - - - 语法：arr.toString();
      - toString方法类似于没有参数的join方法。

```javascript
let arr1 = [1,2,3];
let arr2 = [4,5,6];
console.log (arr1.toString());  //1,2,3
console.log (arr2.toString());  //4,5,6 
```

- - 数组的排序

- - - reverse()  颠倒数组排列顺序

- - - - 语法：arr.reverse()
      - reverse虽然可以将数组顺序颠倒，但是不如sort灵活。

```javascript
let arr = [1,2,3,4,5];
console.log (arr.reverse());  //[5, 4, 3, 2, 1]
```

- - - sort()  重新排列数组元素，最小的值排在前面，最大的值排在后面

- - - - 语法：arr.sort()
      - sort()会在每一项上调用String()转型函数，然后比较字符串来决定顺序（按照Unicode编码来排）。这样在比较时会存在隐患。

```javascript
let arr = [1,2,3,4,5,10];
arr.sort();
console.log (arr); //[1, 10, 2, 3, 4, 5]
//显然这不是理想的排列结果，10应该放置于数组末尾，但是字符串"10"在字符串"2"之前，所以会这样排
```

- - - - 要解决这个问题，我们需要手写一个比较函数，然后传入sort()中。

```javascript
let arr = [1,5,10,7,3];
function compare(val1,val2){
    if(val1>val2){
        return 1;
    }
    else if(val1<val2){
        return -1;
    }
    else{
        return 0;
    }
}
arr.sort(compare);
console.log (arr);  //[1, 3, 5, 7, 10]
```

##### 函数

######  1 创建函数

我们可以使用四方式来创建函数，函数声明、函数表达式、箭头函数和Function构造函数。

1.在js中，使用函数声明的方式来创建函数是最频繁的。

语法：**function 函数名(参数1，参数2){ 函数体 }**

```javascript
function sum(num1,num2){
    return num1+num2;
}
const res = sum(1,2);
console.log (res);  //3
```

2.另一种创建函数的方式是使用函数表达式来创建。

语法：l**et 变量 = function(参数1，参数2){ 函数体 }**

```javascript
//赋值操作右边的函数因为没有名称，所以我们称它为匿名函数
let sum = function(num1,num2){
    return num1+num2;
}
const res = sum(1,2);
console.log (res);  //3
```

3.还有一种和函数表达式很相似的创建函数的方式，我们称为箭头函数。

语法：**let 变量 = (参数1，参数2)=>{ 函数体 }**

```javascript
let sum = (num1,num2)=>{
    return num1+num2;
}
const res = sum(1,2);
console.log (res);  //3
```

4.最后一种方法是使用构造函数，就和创建一个对象、数组相似。这种方式并不常用而且会影响性能。

```javascript
let sum = new Function("num1","num2","return num1+num2");
const res = sum(1,2);
console.log (res);  //3
```

使用最后一种方法会影响性能的原因在于创建的过程中代码会执行两次，第一次是将它作为常规代码，第二次是解释传给构造的字符串。但是把函数想象成对象，把函数名想成指针的思想非常重要，最后一种方法就是这种概念的经典诠释。

###### 2 函数名

大多数的函数都是有自己的名字的，这个名字和函数的功能息息相关，没有名字的函数被称为匿名函数，箭头函数就是经典的匿名函数。

函数名是一个指向函数的指针，所以它跟其他包含对象指针的变量具有相同的行为。这也就意味着一个函数可以有多个名称。

```javascript
function sum(a, b) {
    return a + b;
}
let copySum = sum;

let res1 = sum(1,2);
let res2 = copySum(2,3);
console.log ('res1=',res1);  //res1=3
console.log ('res2=',res2);  //res2=5
//就算将原来指向函数的指针置为空，但是函数仍然存在。所以副本函数还是可以运行。
sum = null;
console.log (copySum(5,6));  //11
```

###### 3 函数的属性

每个函数都有两个属性，length和prototype。

prototype的知识前面我们后边课程会讲，而对于length想必大家都充满了疑惑，函数有啥length呢，不应该只有数组才有吗？确实函数中是由length的情况较为少见，它是用来**保存函数定义的形参个数**的。

```javascript
function sum(a, b) {
    return a + b;
}
function test1(a) {
    return a;
}
function test2() {
    return;
}
console.log (sum.length);  //2
console.log (test1.length);  //1
console.log (test2.length);  //0
```

函数的方法就不像数组那么多了，就只有两个：call和apply，用来转函数体内this的指向的，this会指向传入小括号内的对象，后边课程中会进行讲解。

###### 4 立即调用函数

立即调用函数又称立即调用的匿名函数(IIFE，Immediately Involked Function Expression，需要记得英文的简写形式)。

```javascript
//基本语法
(function(){
	块级作用域
})()
//运用
(function(){
	console.log (111);  //111
})()
```

使用立即执行函数可以有效防止变量外泄，这一点运用得非常广泛（比如webpack的底层）。