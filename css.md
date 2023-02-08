

### 基础选择器

##### 标签选择器

![标签选择器](.\css\标签选择器.png)

##### 类选择器

![类选择器](.\css\类选择器.png)

##### id选择器

![id选择器](.\css\id选择器.png)

##### 通配符选择器

![通配符选择器](.\css\通配符选择器.png)

### 字体和文本样式

| 属性名                                               | 功能             |
| ---------------------------------------------------- | ---------------- |
| font-size:数字px                                     | 字体大小         |
| font-weight:700(加粗)                                | 字体粗细         |
| font-style:normal/italic                             | 是否倾斜         |
| font-family:微软雅黑，黑体，sans-serif               | 字体             |
| text-indent:数字px/em(一个字)                        | 文本缩进         |
| text-align:left/right/right                          | 文本水平对齐方式 |
| text-decoration:underline/line-through/overline/none | 文本修饰         |
| line-height:数字px/数字(倍数)                        | 行高             |
| margin: 0 auto                                       | 标签居中         |

##### 叠加

叠加：后面的覆盖前面的

##### font连写

```css
// 复合
font:style weight size/height 字体；
```

##### 垂直居中

垂直居中设置行高属性值=自身高度属性值(文字是单行的)

```css
<style>
<div>{
width:400px;
height:400px;
background-color:pink;
text-align:center;
line-weight:400px;
}
</style>
```

### 颜色取值

![颜色取值](.\css\颜色取值.png)

### 选择器进阶

##### 后代选择器：空格

![后代选择器](.\css\后代选择器.png)

##### 子代选择器：>

![子代选择器](.\css\子代选择器.png)

##### 并集选择器：,

![并集选择器](.\css\并集选择器.png)

##### 交集选择器：.

![交集选择器](.\css\交集选择器.png)

##### hover

![伪类选择器](.\css\伪类选择器.png)

##### emmet语法

| 记忆       | 示例              | 效果                                 |
| ---------- | ----------------- | ------------------------------------ |
| 标签名     | div               | <div></div>                          |
| id选择器   | #one              | <div class="red"></div>              |
| 交集选择器 | p.red#one         | <p class="red" id="one"></p>         |
| 子代选择器 | ul>li             | <ul><li></li><ul>                    |
| 内部文本   | ul>li{我是li内容} | <ul><li>我是li内容</ul></li>         |
| 创建多个   | ul>li*3           | <ul><li></li><li></li><li></li></ul> |
| 类选择器   | .red              | <div id="one"></div>                 |

### 背景

| 属性名                                               | 含义     |
| ---------------------------------------------------- | -------- |
| width:400px                                          | 宽度     |
| height:400px                                         | 高度     |
| background-color:pink                                | 背景颜色 |
| background-image:url(‘图片路径’)                     | 背景图片 |
| background-repeat:repeat/no-repeat/repeat-x/repeat-y | 背景平铺 |
| background-position:水平位置  垂直位置               | 背景位置 |

![背景位置](.\css\背景位置.png)

##### 背景连写

```css
background：color image repeat position
```

### 元素显示模式

##### 块级元素

![块级元素](.\css\块级元素.png)

##### 行内元素

![行内元素](.\css\行内元素.png)

行内块元素

![行内块元素](.\css\行内块元素.png)

##### 元素模式转换

| 属性                 | 效果             |
| -------------------- | ---------------- |
| display:block        | 转换成块级元素   |
| display:inline-block | 转换成行内块元素 |
| display:inline       | 转换成行内元素   |

![选择器优先级](.\css\选择器优先级.png)

### 盒子模型

| 属性名                                    | 含义                 |
| ----------------------------------------- | -------------------- |
| `width:数字px`                            | 内容区域宽度         |
| `height:数字px`                           | 内容区域高度         |
| `border:数字px solid/dashed/dotted color` | 边框（不分先后顺序） |
| `border-left(方位名词)`                   | 只作用于某个边       |
| `padding:数字px`                          | 内边距               |
| `box-sizing:border-box`                   | 自动内减             |
| `margin（同border可加方位）`              | 外边距               |

##### padding

| 值的个数 | 作用方向    |
| -------- | ----------- |
| 1        | 四个方向    |
| 2        | 上下 左右   |
| 3        | 上 左右 下  |
| 4        | 上 右 下 左 |

互相嵌套的块级元素：子元素margin-top会作用于父级。

结果：父元素一起往下移动

解决：给父元素设置overflow:hidden/border-top/padding-top

行内元素使用line-height设置行高（span）

### 结构伪类选择器

| 选择器                  | 说明                      |
| ----------------------- | ------------------------- |
| `E:first-child{}`       | 匹配父元素中第一个元素    |
| `E:last-child{}`        | 匹配父元素中最后一个元素  |
| `E:nth-child(n){}`      | 匹配父元素中第n个元素     |
| `E:nth-last-child(n){}` | 匹配父元素中倒数第n个元素 |

##### n的选择

n取值为0，1，2，3，4，5，6......

偶数：2n/even

奇数：2n±1/odd

前五个：-n+5

从第五个往后：n+5

### 伪元素

| 伪元素     | 作用                             |
| ---------- | -------------------------------- |
| `::before` | 在父元素内容的最前添加一个伪元素 |
| `::after`  | 在父元素内容的最后添加一个伪元素 |

```css
.father::before{
content:'必须添加';
}
```

### 浮动

`float:right/left`

脱离标准流，依次排列，可视为行内块元素

##### 清除浮动

1.给父元素设置

```css
overflow:hidden
```

2.单/双伪元素法

```php+html
<style>
.clearfix::after{
    content:'';
    display:block;
    clear:both;
    height:0;
    visibility:hidden;
}
//    
.clearfix::before,
.clearfix::after{
   content:'';
   display:table;
    }
    
.clearfix::after{
   clear:both;
    }
</style>
<body>
<div class="top clearfix">
<div class="left"></div>
<div class="right"></div>
</div>
</body>
```

### 定位

##### 子盒子在父盒子居中

```css
left:50%;
margin-left:-宽度一半；

top:50%;
margin-top:-高度一半；
```

以下省略margin-...

```css
transform:translate(-50%,-50%);
```

属性名：position

| 定位方式 | 属性值     |
| -------- | ---------- |
| 静态定位 | static     |
| 相对定位 | relative   |
| 绝对定位 | absolutely |
| 固定定位 | fixed      |

##### 子绝父相

子元素相对父元素定位时使用

##### 固定定位

```css
position:fixed;
```

### 装饰

##### 垂直对齐方式

属性名：vertical-align

| 属性值   | 效果           |
| -------- | -------------- |
| baseline | 默认，基线对齐 |
| top      | 顶部对齐       |
| middle   | 中部对齐       |
| bottom   | 底部对齐       |

##### 光标类型

属性名：cursor

| 属性名  | 效果                 |
| ------- | -------------------- |
| default | 默认值，通常是箭头   |
| pointer | 小手效果，可以点击   |
| text    | 工字型，可以选择文字 |
| move    | 十字光标，可以移动   |

##### 边框圆角

属性名：border-radius

取值：数字px(可以取多个或一个)/百分数

##### 溢出部分显示效果

属性名：overflow

| 属性名  | 效果                               |
| ------- | ---------------------------------- |
| visible | 默认值，溢出部分可见               |
| hidden  | 溢出部分隐藏                       |
| scroll  | 无论是否溢出，都显示滚动条         |
| auto    | 根据是否溢出，自动显示或隐藏滚动条 |

##### 元素本身隐藏

占位隐藏

```css
visibility:hidden;
```

不占位隐藏

```css
display:none;
```

可配合完成下拉菜单

##### 元素整体透明度

属性名：opacity

属性值：0-1（0:完全透明，1:完全不透明)

##### 表格边框合并

```css
border-collapse:collapse;
```

### 选择器拓展

##### 焦点伪类选择器（表单）

```css
// 获得焦点时进行
input:focus{
    background-color:skyblue;
}
```

##### 属性选择器

选择具有某属性或属性值等于某的标签

| 选择器          | 功能                                           |
| --------------- | ---------------------------------------------- |
| `E[attr]`       | 选择具有`attr`属性的`E`元素                    |
| `E[attr="val"]` | 选择具有`attr`属性并且属性值等于`val`的`E`元素 |

