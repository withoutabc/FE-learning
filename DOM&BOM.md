### 获取DOM对象

```js
document.querySelector('css选择器')
//返回匹配的第一个元素，一个HTMLElement对象
document.querySelectorAll('css选择器')
//返回匹配的NodeList对象集合
document.getElementById('')
//根据id获取一个元素
document.getElementsByTagName('')
//根据标签获取一类元素 所有
document.getElementsByClassName('')
//根据类名获取元素 所有
```

### 设置/修改DOM元素内容

```js
// 1.document.write()  位置只能在body前，标签被解析
// 2.元素innerText属性 不解析标签
let box = document.querySelector('') // 获取标签（元素）
box.innerText = '' // box是对象，innerText是值
// 3.元素innerHTML属性 解析标签 用法同上
```

### 设置/修改DOM元素属性

#### 设置/修改常用属性

```js
let pic = document.querySelector('img')
pic.src = ''
pic.title = ''
```

#### 设置/修改元素样式属性

```js
// ① 修改css style
let box = document.querySelector('.box')
box.style.backgroundColor = 'red'
box.style.width = '300px'
box.style.marginTop = '50px'
// ② 修改标签的类名，覆盖
box.className = ''
// ③ 通过classList操作类控制CSS
box.classList.add('') // 追加一个类
box.classList.remove('') // 删除一个类
box.classList.toggle('') // 切换一个类
```

#### 设置/修改表单元素属性

```js
let input = document.querySelector('input')
input.value = ''
input.type = ''
// disabled checked selected 通过布尔值控制
let btn = document.querySelector('button')
btn.disabled = false
```

### 定时器-间歇函数

```js
// 设置定时器
let timer = setInterval(函数，间隔时间)
// 清楚定时器
clearInterval(timer)
```

### 事件监听

```js
// 1.获取元素
let btn = document.querySelector('button')
// 2.事件监听:事件源+事件+事件处理函数
btn.addEventListener('click',function(){
    alert('')
})
```

### 事件类型

| 事件           | 情况         |
| -------------- | ------------ |
| 鼠标点击       | `click`      |
| 鼠标经过       | `mouseenter` |
| 鼠标离开       | `mouseleave` |
| 获得焦点       | `focus`      |
| 失去焦点       | `blur`       |
| 键盘按下触发   | `Keydown`    |
| 键盘抬起触发   | `Keyup`      |
| 用户输入事件   | `input`      |
| 表单值发生改变 | `change`     |

### 节点操作

#### 父节点查找

```js
// 返回最近一级的父节点
子元素.parentNode
```

#### 子节点查找

```js
// 获得所有子节点、包括文本节点（空格、换行）、注释节点等
父元素.childNodes
// 仅获得所有元素节点，返回一个伪数组
父元素.children
```

#### 兄弟节点查找

```js
// 下一个兄弟节点
元素.nextElementSibling
// 上一个兄弟节点
元素.previousElementSibling
```

#### 创建和追加节点

```js
// 创建一个元素节点
document.createElement('标签名')
// 插入到父元素的最后一个元素
父元素.appendChild(要插入的元素)
// 插入到父元素的某个子元素的前面
父元素.insertBefore(要插入的元素，放到哪个元素前面)
```

#### 克隆节点

```js
// 克隆一个已有的元素节点
元素.cloneNode(布尔值)
// true:克隆时包含后代节点一起克隆
// false:克隆时不包含后代节点 默认为false
```

#### 删除节点

```js
父元素.removeChild(子元素)
// 如不存在父子关系则删除失败
```

### 实例化时间

```js
// 获得当前时间
let date = new Date()
// 获得指定时间
let date new Date('1949-10-01')
```

#### 时间对象的方法

| 方法            | 作用               | 说明                 |
| --------------- | ------------------ | -------------------- |
| `getFullYear()` | 获得年份           | 获取四位年份         |
| `getMonth()`    | 获得月份           | 取值为0-11           |
| `getDate()`     | 获取月份中的每一天 | 不同月份取值也不相同 |
| `getDay()`      | 获取星期           | 取值为0-6            |
| `getHours()`    | 获取小时           | 取值为0-23           |
| `getMinutes()`  | 获取分钟           | 取值为0-59           |
| `getSeconds()`  | 获取秒             | 取值为0-59           |

#### 获取时间戳

```js
// 1.getTime()
let date = new Date()
date.getTime()
// 2.+new Date()
// 3.Date.now() 当前时间，不能指定

// 计算倒计时
d = parselnt(总秒数/60/60/24) // 计算天数
h = parselnt(总秒数/60/60%24) // 计算小时
m = parselnt(总秒数/60%60)    // 计算分钟
s = parselnt(总秒数%60)       // 计算当前秒数
```

### 事件对象

```js
document.addEventListener('mousemove',function(e){
    
})
```

#### 获取事件对象

| 属性名              | 说明                                     |
| ------------------- | ---------------------------------------- |
| `type`              | 获取当前的事件类型                       |
| `clientX`/`clientY` | 获取光标相对于浏览器可见窗口左上角的位置 |
| `offsetX`/`offsetY` | 获取光标相对于当前DOM元素左上角的位置    |
| `key`               | 用户按下的键盘键的值                     |

#### 阻止事件流动

```js
// 阻止冒泡事件，把事件限制在当前元素内
事件对象.stopPropagation()
// 鼠标经过事件
// mouseover,mouseout 会有冒泡效果
// mouseenter,mouseleave 没有冒泡效果
```

#### 阻止默认行为

```js
// 阻止默认行为，比如链接点击不跳转，表单域的跳转
<body>
    <a> href="http://www.baidu.com">跳转到百度</a>
    <script>
       let a = document.querySelector('a')
       a.addEventListener('click',function(e){
       // 阻止默认行为方法
       e.preventDefault()
       })
    </script>
</body>
```

#### 事件委托

```js
<ul>
    <li>第一个li</li>
    <li>第二个li</li>
    <li>第三个li</li>
    <li>第四个li</li>
    <li>第五个li</li>
</ul>
<script>
    let ul = document.querySelector('ul')
    ul.addEventListener('click',function(){
    e.target.style.color = 'red'
})
</script>
// 优点：给父级元素加事件
// 原理：利用事件冒泡的特点，给父元素添加事件，子元素可以触发
```

### 滚动事件

```js
window.addEventListener('scroll',function(){
    
})
```

### 加载事件

```js
// 页面加载完毕执行事件
window.addEventListener('load',function(){
    
})
// 初始HTML文档被完全加载和解析完成之后，DOMContentLoaded事件被触发
// 无需等待样式表、图像完全加载
document.addEventListener('DOMContentLoaded',function(){
    
})
```

### 元素大小和位置

#### scroll家族

```js
// 1.获取宽高
// 元素内容总宽高，返回值不带单位
// scrollWidth和scrollHeight
// 2.获取位置
// 获取元素内容往左，往上滚出去看不到的距离
// scrollLeft和scrollTop
// 可以修改的属性，不带单位
```

##### 检测页面滚动距离

```js
window.addEventListener('scroll',function(){
    console.log(document.documentElement.scrollTop)
})
// document.documentElement 返回HTML元素
```

#### offset家族

```js
// 1.获取宽高
// 获取元素的自身宽高（包含元素自身设置的宽高、padding、border）
// offsetWidth和offsetHeight
// 2.获取位置
// 获取元素距离自己定位父级元素的左、上距离
// offsetLeft和offsetTop
// 只读属性
```

#### client家族

```js
// 获取宽高
// 获取当前可视区域宽高
// clientWidth和clientHeight
```

##### 窗口变化事件

```js
window.addEventListener('resize',function(){
    console.log(document.documentElement.clientWidth)
})
```

### 延时函数

```js
// 仅执行一次
let timer = setTimeout(回调函数，等待的毫秒数)
clearTimeout(timer)
```

### location对象

```js
// 跳转页面
location.href = ""

// query
location.search
// target.html
<script>
    console.log(location.search)
// ?username=...
</script>
// location.search.html
<body>
    <form action = "target.html">
        <input type = "text" name = "username">
        <button>提交</button>
    </form>
</body>

// path
location.hash
<body>
    <a href="#one">第一个</a>
    <a href="#two">第二个</a>
    <script>
        console.log(location.hash)
// #one/#two
    </script>
</body>

// 刷新当前页面
location.reload() // 有本地缓存
location.reload(true) // 强制刷新，从网上拉取
```

### navigator对象

```js
<script>
    // 检测 userAgent(浏览器信息)
    !(function(){
        const userAgent = navigator.userAgent
        // 验证是否为Android或iPhone
        const android = userAgent.match(/(Android);?[\s\/]+([\d.]+)?/)
        const iphone = userAgent.match(/(iPhone\sOS)\s([\d_]+)/)
         // 如果是Android或iPhone,则跳转至移动站点
        if (android||iphone){
        location.href='http://m.itcast.cn'
    }
    })()
</script>
```

### history对象

```js
// 前进
history.forward()
// 后退
history.back()
// 设置格数
history.go(±数字)
```

### 本地存储

```js
// 存储数据
localStorage.setItem(key,value)
// 获取数据
localStorage.getItem(key)
```

#### 存储复杂数据类型

```js
// JSON.stringify(复杂数据类型)
// 将复杂数据转换成JSON字符串 存储 在本地
// JSON.parse(JSON字符串)
// 将JSON字符串转换成对象 取出 时候使用
let obj = {
    "name":"刘德华",
    "age":17,
    "address":"程序员"
}
localStorage.setItem('obj',JSON.stringify(obj))
console.log(JSON.parse(localStorage.getItem('obj')))
```

### 自定义属性

```js
getAttribute('属性名') // 获取自定义属性
setAttribute('属性名','属性值') // 设置自定义属性
removeAttribute('属性名') // 删除自定义属性
// 
<div class="box" data-index="0" data-name="andy"></div>
<script>
   let box = document.querySelector('.box')
   console.log(box.dataset)
   console.log(box.dataset.index)
</script>
```

### 正则表达式

#### 基本使用

```js
let reg = /前端/
let str = "我们都在学前端"
reg.test(str) // true
reg.exec(str) // 不存在返回null,存在返回数组（包含位置）
```

#### 元字符

##### 边界符

| 边界符 | 说明               |
| ------ | ------------------ |
| ^      | 表示匹配行首的文本 |
| $      | 表示匹配行尾的文本 |

```js
console.log(/^哈$/.test('哈哈')) // false
console.log(/^哈$/.test('哈')) // true
```

##### 量词

| 量词  | 说明      |
| ----- | --------- |
| *     | 0次及以上 |
| +     | 1次及以上 |
| ?     | 0或1次    |
| {n}   | n次       |
| {n,}  | n次及以上 |
| {n,m} | n到m次    |

```js
console.log(/^a{3}$/.test('aaaa')) // false
```

##### 字符类

| 符号 | 说明                 |
| ---- | -------------------- |
| []   | 出现其中任何一个为真 |

```js
console.log(/^[abc]$/.test('a')) // true
console.log(/^[abc]$/.test('b')) // true
console.log(/^[abc]$/.test('c')) // true
```

```js
// [-]连字符
console.log(/^[a-zA-Z0-9-_]$/.test('d')) // true
```

腾讯QQ号：
`/^[1-9][0-9]{4,}$/` (腾讯QQ号从10000开始)

| 符号 | 说明                           |
| ---- | ------------------------------ |
| [^]  | 取反符号                       |
| .    | 匹配除换行符之外的任何单个字符 |

预定义

| 预定类 | 说明                                     | 等价           |
| ------ | ---------------------------------------- | -------------- |
| \d     | 匹配0-9的任一数字                        | [0-9]          |
| \D     | 匹配0-9以外的任意字符                    | [^0-9]         |
| \w     | 匹配任意字母、数字和下划线               | [A-Za-z0-9_]   |
| \W     | 匹配除字母、数字和下划线                 | [^A-Za-z0-9]   |
| \s     | 匹配空格（包括换行符、制表符、空格符等） | [\t\r\n\v\f]   |
| \S     | 匹配非空格的字符                         | [^ \t\r\n\v\f] |

日期格式：

`/^\d{4}-\d{1,2}-\d{1,2}/`

#### 修饰符

`/表达式/修饰符`

| 修饰符 | 说明                         |
| ------ | ---------------------------- |
| `i`    | 正则匹配时字母不区分大小写   |
| `g`    | 匹配所有满足正则表达式的结果 |

##### 替换

`字符串.replace(/正则表达式|表达式/,'替换的文本')`

### 属性选择器

```js
<style>
    <input name="username" type="text" placeholder="设置用户名称"
</style>
let username = document.querySelector('[name=username]')
```

