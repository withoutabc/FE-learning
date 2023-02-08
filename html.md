### 标签

| 标签        | 含义    |
| ----------- | ------- |
| `<h1></h1>` | 1级标题 |
| `<h2></h2>` | 2级标题 |
| `<h3></h3>` | 3级标题 |
| `<h4></h4>` | 4级标题 |
| `<h5></h5>` | 5级标题 |
| `<h6></h6>` | 6级标题 |
| `<p></p>`   | 段落    |
| `<br>`      | 换行    |
| `<hr>`      | 水平线  |

| 标签                                                  | 含义   |
| ----------------------------------------------------- | ------ |
| `<b></b>` (strong)                                    | 加粗   |
| `<u></u>` (ins)                                       | 下划线 |
| `<i></i>` (em)                                        | 倾斜   |
| `<s></s>` (del)                                       | 删除线 |
| `<img src="" alt="" title="" width="">`               | 图片   |
| `<audio src="" controls autoplay loop></audio>`       | 音频   |
| `<video src="" controls autoplay loop muted></video>` | 视频   |
| `<a href="__.html"  target=“_blank/_self”>跳转</a >`  | 链接   |

### 列表

##### 无序列表

```php+HTML
<ul>
<li>列举</li>
<li>列举</li>
</ul>
```

##### 有序列表 

```html
<ol>
<li>列举</li>
<li>列举</li>
</ol>
```

##### 自定义列表

```html
<dl>
<dt>标题</dt>
<dd>内容</dd>
<dd>内容</dd>
</dl>
```

### 表格标签

```html
<table border="" width="" height="">
<caption>内容</caption>//标题
<th>
<td>表头</td>
<td rowspan="2">表头</td>
<td>表头</td>
</th>
<tr>
<td>单元格</td>
<td colspan="6">单元格</td>
<td>单元格</td>
</tr>
</table>
```

| 标签              | 含义     |
| ----------------- | -------- |
| `<thead></thead>` | 表格头部 |
| `<tbody></tbody>` | 表格主题 |
| `<tfoot><tfoot>`  | 表格底部 |
| `rowspan`         | 跨行合并 |
| `colspan`         | 跨列合并 |

### 表单标签

##### input系列标签

| 标签  | type属性值 | 说明     |
| ----- | ---------- | -------- |
| input | text       | 文本框   |
| input | password   | 密码框   |
| input | radio      | 单选框   |
| input | checkbox   | 多选框   |
| input | file       | 文件选择 |
| input | submit     | 提交按钮 |
| input | reset      | 重置按钮 |
| input | button     | 普通按钮 |

| 属性名      | 说明                    |
| ----------- | ----------------------- |
| placeholder | 占位符                  |
| name        | 单选只能选一个（radio） |
| checked     | 默认选中（radio）       |
| multiple    | 选中多个文件（file）    |

```php+HTML
<form action="">
用户名：<input type="text">
<br>
<br>
密码：<input type="password">
<br>
<br>
<input type="submit" value="免费注册">
<input type="reset">
<input type="button" value="普通按钮">
</form>
```

##### button按钮标签

```php+HTML
<button>我是按钮</button>
<button type="submit">提交按钮</button>
<button type="reset">重置按钮</button>
<button type="button">普通按钮，没有任何功能</button>
```

##### select下拉菜单标签

```php+HTML
<select>
<option>北京</option>
<option>上海</option>
<option>广州</option>
<option selected>深圳</option>
</select>
```

##### textarea文本域标签

```php+HTML
<textarea cols="60" rows="30"></textarea>
```

##### label标签

```php+HTML
<input type="radio" name="sex" id="man"><label for="man">男</label>
<label><input type="radio" name="sex">女</label>
```

### 语义化标签

##### 无语义

```php+HTML
<div>这是div标签</div>
<div>这是div标签</div>
```

(单独占一行)

```php+HTML
<span>这是span标签</span>
<span>这是span标签</span>
```

(不换行)

##### 有语义

| 标签名（头尾） | 语义       |
| -------------- | ---------- |
| header         | 网页头部   |
| nav            | 网页导航   |
| footer         | 网页底部   |
| aside          | 网页侧边栏 |
| section        | 网页区块   |
| article        | 网页文章   |

### 字符实体

![字符实体](.\html\字符实体.png)