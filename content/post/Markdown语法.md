+++
title = "Markdown语法"
date = "2019-02-04T11:43:45+08:00"
toc = true
tags = ["Markdown语法"]
categories = ["page 搭建", "Markdown语法"]
description = ""
+++


# Markdown 是什么

> Markdown 是一种轻量级标记语言，创始人为约翰·格鲁伯（John Gruber）。它允许人们**使用易读易写的纯文本格式编写文档，然后转换成有效的 XHTML（或者 HTML）  文档**
>
> 这种语言吸收了很多在电子邮件中已有的纯文本标记的特性。

<!--more-->



# 基本语法

## 标题

一个到多个`#`，然后空格，最后是文字。

```
# 标题H1
## 标题H2
### 标题H3
#### 标题H4
##### 标题H5
###### 标题H6
```

以上文本转换后如下：

# 标题H1
## 标题H2
### 标题H3
#### 标题H4
##### 标题H5
###### 标题H6



---

## 列表

### 无序列表

提示符（`*`或者`-`或者`+`），然后是空格，最后是文字。敲击回车的时候，会自动出现新提示符。想要结束列表，连续敲两下回车即可。 
```
+ A 
+ B 
+ C 
```
以上文本转换后得到： 
+ A 
+ B 
+ C 

### 有序列表

先是数字，然后是`.`，再然后是空格，最后是文字。敲击回车的时候，会自动出现新序号。想要结束列表，连续敲两下回车即可。 

```
1. a 
2. b 
3. b 
```

1. a 
2. b 
3. b 

---

## 代码

### 代码块和语法高亮

使用一对**三个反引号** 
来包含多行代码：

```
​```
    int a = 0;
    a++;
​```
```

效果：

```
    int a = 0;
    a++;
```

在上面的语法基础上，在第一个**三个反引号** 之后添加代码的语言名称，即可实现语法高亮。 



```
​```python
    int a = 0;
    a++;
​```
1234
```


效果：

```python
    int a = 0;
    a++;
```





### 行内代码

可以通过两个反引号（Tab 键上方、数字 1 左侧的那个按键）插入行内代码。 
反引号  int a = 100;   反引号

转换后是：

` int a = 100;`

## 分隔线

在一行中使用三个或更多的`-`或者`*`或者`_` ，然后换行。 
`---（回车）`

效果如下：

---





---

## 强调

### 斜体

用两个`*`把要强调的内容包含起来，则表现为斜体。 
`*我是斜体*` 
效果如下：

*我是斜体*

### 粗体

用两个`**`把要强调的内容包含起来，则表现为粗体。 
`**我是粗体**` 
效果如下：

**我是粗体**



---

## 引用

### 单行引用

在行首使用 `>`符号，就可以将其后的内容标记为引用。 
`>春风得意马蹄疾，一日看尽长安花` 

效果如下：

> 春风得意马蹄疾，一日看尽长安花

### 多行引用

如果仅在第一行使用 `>`， 后面相邻的行即使省略 `>`，也会变成引用内容。 
`>在天愿作比翼鸟，在地愿为连理枝。 `

`天长地久有时尽，此恨绵绵无绝期。`

以上文本被转换为：

> 在天愿作比翼鸟，在地愿为连理枝。 
> 天长地久有时尽，此恨绵绵无绝期。

要结束引用，在引用的末尾连续敲两个回车即可。

### 嵌套的引用

用多个`>`就可以表示嵌套的引用。 
`>子曰` 
`>>学而时习之，不亦说乎？有朋自远方来，不亦乐乎？` 效果如下：

> 子曰
>
> > 学而时习之，不亦说乎？有朋自远方来，不亦乐乎？

### 引用中可以使用其他语法

引用的内容也可以使用其他语法，比如标题、列表、强调等。

```
>1. 我是列表
>2. 我是列表
>3. 我是列表
> 
>*我是斜体*
>**我是粗体**
>
>        int a = 0;
>        int b = 1;
>        int c = a + b; 12345678910
```

效果如下：

>1. 我是列表
>2. 我是列表
>3. 我是列表
>
>*我是斜体*
>**我是粗体**
>
>   int a = 0;
>   int b = 1;
>   int c = a + b; 12345678910

---

## 超链接

### 行内式

格式为： 
`[链接文字](地址 '标题')` 
**注**：地址与标题之间有一个空格。

例如： 
`[百度首页](https://www.baidu.com/ "跳转到百度首页")`

效果如下：

[百度首页](https://www.baidu.com/)

当你把鼠标停留在链接名称上，则会显示出标题。

**注**：在不需要的情况下，标题可以省略。



### 参考式

参考式超链接一般用在学术论文上，或者某个链接在文章中多处被引用的情况，这样便于对链接统一管理。

参考式链接的写法相当于把行内式拆分成两部分，并通过一个**链接标记**来连接两部分。

语法说明： 
参考式链接分为两部分：首先写 
`[链接文字][链接标记]`

然后在文本的任意位置写 
`[链接标记]:地址 "标题"`

如果链接文字本身可以作链接标记，你也可以把上面两行分别写为： 
`[链接文字][]` 
`[链接文字]:地址 "标题"`

例如： 
`我经常去的几个网站是[GitHub][1]，[知乎][2]，[简书][3]。`

```
[1]:https://github.com "github.com"
[2]:https://www.zhihu.com "zhihu.com" 
[3]:http://www.jianshu.com "jianshu.com" 
```

效果：

我经常去的几个网站是[GitHub](https://github.com/)，[知乎](https://www.zhihu.com/)，[简书](http://www.jianshu.com/)。

如果把链接文字本身作为链接标记，则写为： 
`我经常去的几个网站是[GitHub][]，[知乎][]，[简书][]。`

`[GitHub]:https://github.com "github.com"` 
`[知乎]:https://www.zhihu.com "zhihu.com"` 
`[简书]:http://www.jianshu.com "jianshu.com"`

效果： 
我经常去的几个网站是[GitHub](https://github.com/)，[知乎](https://www.zhihu.com/)，[简书](http://www.jianshu.com/)。

## 图片

插入图片的语法和插入超链接的语法基本一致，只是在最前面多一个`!`。也分为行内式和参考式两种。 
行内式： `![炮姐](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1549263234828&di=4a344f759b9ceb725d0e741500b7d0b3&imgtype=0&src=http%3A%2F%2Fb-ssl.duitang.com%2Fuploads%2Fitem%2F201503%2F29%2F20150329004520_mL3HU.jpeg "炮姐萌吗")`

![炮姐](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1549263234828&di=4a344f759b9ceb725d0e741500b7d0b3&imgtype=0&src=http%3A%2F%2Fb-ssl.duitang.com%2Fuploads%2Fitem%2F201503%2F29%2F20150329004520_mL3HU.jpeg "炮姐萌吗")

参考式1： 
`![炮姐][4]`

```
[4]:https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1549263234828&di=4a344f759b9ceb725d0e741500b7d0b3&imgtype=0&src=http%3A%2F%2Fb-ssl.duitang.com%2Fuploads%2Fitem%2F201503%2F29%2F20150329004520_mL3HU.jpeg "参考式1——炮姐萌吗"
```

![炮姐](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1549263234828&di=4a344f759b9ceb725d0e741500b7d0b3&imgtype=0&src=http%3A%2F%2Fb-ssl.duitang.com%2Fuploads%2Fitem%2F201503%2F29%2F20150329004520_mL3HU.jpeg "炮姐萌吗")

参考式2（把链接文字本身作为链接标记）： 
`![炮姐][]`

```
[炮姐]:https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1549263234828&di=4a344f759b9ceb725d0e741500b7d0b3&imgtype=0&src=http%3A%2F%2Fb-ssl.duitang.com%2Fuploads%2Fitem%2F201503%2F29%2F20150329004520_mL3HU.jpeg "参考式2——炮姐萌吗"
```

![炮姐](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1549263234828&di=4a344f759b9ceb725d0e741500b7d0b3&imgtype=0&src=http%3A%2F%2Fb-ssl.duitang.com%2Fuploads%2Fitem%2F201503%2F29%2F20150329004520_mL3HU.jpeg "炮姐萌吗")

## 转义字符

Markdown可以利用反斜线`\`来插入一些在语法中有其它意义的符号。 
例如：想把星号加在文字两侧（但不是斜体），你可以在星号的前面加上反斜线： 
`\*literal asterisks\*` 
效果： 
*literal asterisks*

Markdown 支持在下面这些符号前面加上反斜线来插入普通的符号：

> \ 反斜线 
> ` 反引号 
> * 星号 
>   _ 下划线 
>   {} 大括号 
>   [] 方括号 
>   () 括号 
> #井号 
> + 加号 
> - 減号 
>   . 英文句点 
>   ! 感叹号

# 扩展语法

### 删除线

用两个`~~`把文字包起来。

```
~~我是删除线~~
1
```

效果： 
~~我是删除线~~



## 表格

#### 基本格式

使用`|` 来分隔不同的单元格，使用`-`来分隔表头和其他行。 
`name | age` 
`---- | ---` 
`Leslie| 12` 
`Mike | 32` 

效果：

| name   | age  |
| ------ | ---- |
| Leslie | 12   |
| Mike   | 32   |

#### 指定对齐方式

在表头下方的分隔线`----`标记中加入`:`，即可指定对齐方式。

`:---`代表左对齐； 
`:---:` 代表居中对齐； 
`---:`代表右对齐。

```md
left | center | right 
:---:| :----  |------:
| aaaaaaaaa| bbbbbbbbbbbb |ccccccccccccccccccccc |
| a        | b            | c     |
```

效果

| left | center    |        right |
| :--: | :-------- | -----------: |
|      | aaaaaaaaa | bbbbbbbbbbbb |
|      | a         |            b |

如果不使用对齐标记，单元格中的内容默认左对齐，表头单元格中的内容默认居中对齐（MarkdownPad就是这样，不同的实现可能会有不同的效果）。

#### 表格内换行

可以用`<br>`表示换行。

```
Name  | Lucky Number
----  | ---
Leslie| 2<br>7
Mike  | 3<br>5<br>8
```

效果：

| Name   | Lucky Number |
| ------ | ------------ |
| Leslie | 2<br>7       |
| Mike   | 3<br>5<br>8  |

#### 表格内嵌套

同引用一样，表格的内容也可以使用其他语法，比如公式、引用、行内代码等。

```
Name |  *abcdef*
---- |-----
Leslie| `int a=18;`
Mike |  $\log_28$
Ann| >青霄有路终须到，金榜无名誓不归
```

效果：

| Name   | *abcdef*                        |
| ------ | ------------------------------- |
| Leslie | `int a=18;`                     |
| Mike   | $\log_28$                       |
| Ann    | >青霄有路终须到，金榜无名誓不归 |

---

# 内嵌HTML

## 下划线

Markdown 并无下划线的原生语法，因为会和链接的默认样式产生混淆。如果你非要给文字加个下划线，也有办法。 
用`<u>`和`</u>`把文字括起来，则有下划线效果。

`<u>我有下划线，可是我不是链接</u>` 
效果：

<u>我有下划线，可是我不是链接</u>

## 字体、字号、颜色

例1：指定字体 
`<font face="隶书"> 我是隶书 </font>` 
效果： 
<font face="隶书"> 我是隶书 </font>

例2：指定字号 
size的取值范围：从 1 到 7 ，浏览器默认值是 3。 
`<font size=5 > 我的size = 5 </font> `
效果：
<font size=5 > 我的size = 5 </font>

例3：指定颜色 
`<font color=GreenYellow>我的color=GreenYellow </font> `
效果：
<font color=GreenYellow>我的color=GreenYellow </font>

## 背景色

Markdown本身不支持背景色设置，需要采用内置html的方式实现。借助 `table`，`tr`， `td` 等表格标签的 `bgcolor` 属性来实现背景色功能。

举例1： 
`<table><tr><td bgcolor=orange> 背景色是橙色 </td></tr></table>` 
效果：

<table><tr><td bgcolor=orange> 背景色是橙色 </td></tr></table>

举例2： 
`<table><tr><td bgcolor=green> <font size = 4 color=yellow> Hello World </font> </td></tr></table>` 
效果：

<table><tr><td bgcolor=green> <font size = 4 color=yellow> Hello World </font> </td></tr></table>

## 注脚

**语法说明：** 
在需要添加注脚的文字后加上脚注名字,称为加注。 然后在文本的任意位置(一般在最后)添加脚注，脚注前必须有对应的脚注名字。

`  [^注脚名字`]

`  [^注脚名字]: `



## emoji表情符号

emoji表情使用:EMOJICODE:的格式，详细列表可见 
<https://www.webpagefx.com/tools/emoji-cheat-sheet/>

当然现在很多markdown工具或者网站都不支持。

语法：

`:kissing_smiling_eyes:`    





