title: MarkDown基本语法

tags: markdown
--------------

### h1~h5的级别

```html
# 这是 H1
### 这是 H3
```

### p标签

```
默认语句就是p标签
```

<!-- more -->

### 区块标签

> 这是区块

```
> 加内容
```

### 分割线

---

### 无序列表

-	列表1
-	列表2
-	列表3

```
- 无序列表1
```

### 有序列表

1.	有序列表1
2.	有序列表2
3.	有序列表3

```html
1.有序列表
```

### 文本

-	这是一段文本上部分

-	这是一段文本下部分

	这是第二段文本

```html
-		这是一段文本上部分

		这是一段文本下部分

-		这是第二段文本

文本段落后加tab可以切换
```

### em标签

*这是em*

```
*这是em*
```

### strong标签

**这是strong**

```
**这是strong**
```

### 表格

| 标题1 | 标题2 |
|-------|-------|
| 内容1 | 内容2 |
| 内容3 | 内容4 |

```html
| 标题1 | 标题2 |
|-------|-------|
| 内容1 | 内容2 |
| 内容3 | 内容4 |
```

### js代码

```javascript
var a;
function test(){
	return a;
}
```

### json代码

```javascript
	"rules": [{
	    "file_type": "Markdown",
	    "pips": [
	    ],
	    "folder_viewer": "Finder",
```

### 添加链接地址

[测试链接](http:www.baidu.com)

```html
[测试链接](http:www.baidu.com "Title Here")
```
