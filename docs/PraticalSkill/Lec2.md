# MarkDown

## 什么是markdown

Markdown是一种轻量级标记语言，排版语法简洁，让人们更多地关注内容本身而非排版。它使用易读易写的纯文本格式编写文档，可与HTML混编，可导出 HTML、PDF 以及本身的 .md 格式的文件。因简洁、高效、易读、易写，Markdown被大量使用，如Github、Wikipedia、简书等。

## 怎么使用markdown

- VScode + Markdown preview enhanced
- Typora

辅助工具： oss+PicGo

## 标题语法

# level
## level
### level

```md
# level
## level
### level
```

## 段落语法

- 换段落：使用空白行或者`<p>` `</p>`
- 换行：使用回车，或者<br>

翻页：
```html
<div STYLE="page-break-after: always;"></div>
```

## 强调语法

**加粗**
*斜体*
***加粗且斜体***
~~划掉~~
==高亮==
__666__


```md
**加粗**
*斜体*
***加粗且斜体***
~~划掉~~
==高亮==
__666__
```

## 应用语法

> 这是一段引用
> >这是嵌套引用

```md
> 这是一段引用
> >这是嵌套引用
```

## 列表语法

1. First item
1. Second item
1. Third item
1. Fourth item

```md
1. First item
1. Second item
1. Third item
1. Fourth item
```

```html
<ol>
<li>First item</li>
<li>Second item</li>
<li>Third item</li>
<li>Fourth item</li>
</ol>
```

- First item
- Second item
- Third item
- Fourth item

```md
- First item
- Second item
- Third item
- Fourth item
```

- First item
- Second item
- Third item
    - Indented item
    - Indented item
- Fourth item

```html
<ul>
<li>First item</li>
<li>Second item</li>
<li>Third item
<ul>
<li>Indented item</li>
<li>Indented item</li>
</ul>
</li>
<li>Fourth item</li>
</ul>	
```

## 代码语法

```html
<code>
</code>
```

```py

```py
print("hello world")
```
```


## 分割线


---

```
---
```


## 链接

[这是一个链接](https://zjuers.com/)

```md
[超链接显示名](超链接地址 "超链接title")
```

```html
<a href="超链接地址" title="超链接title">超链接显示名</a>
```

```md
![图片alt](图片链接 "图片title")
```

```html
<img src="图片链接" alt="图片alt" title="图片title">
```

给图片加链接

```md
[![pic](https://blog-pic-thorin.oss-cn-hangzhou.aliyuncs.com/b2082c0fc6b483abc54eee77a933416.jpg)](https://markdown.com.cn)
```

[![pic](https://blog-pic-thorin.oss-cn-hangzhou.aliyuncs.com/b2082c0fc6b483abc54eee77a933416.jpg)](https://markdown.com.cn)


### 调整图片大小

![pic](https://blog-pic-thorin.oss-cn-hangzhou.aliyuncs.com/b2082c0fc6b483abc54eee77a933416.jpg#pic_left)

<div align="left">
<img src=https://blog-pic-thorin.oss-cn-hangzhou.aliyuncs.com/b2082c0fc6b483abc54eee77a933416.jpg width=200 height=100/>
</div>

<img src=https://blog-pic-thorin.oss-cn-hangzhou.aliyuncs.com/b2082c0fc6b483abc54eee77a933416.jpg width=200 height=100 />

## 部分常用HTML语法（tex基本都可以替代）

### 下划线

<ins>下划线部分</ins>，其语法为

```html
<ins>下划线部分</ins>
```

### 上标

上标<sup>内容</sup>，其语法为

```html
<sup>上标的内容</sup>
```

### 下标

下标<sub>内容</sub>，其语法为

```html
<sub>下标的内容</sub>
```

###  按键

 <kbd>按键</kbd>，其语法为

```html
 <kbd>按键</kbd>
```

### 字体

```html
<font color=#06oo11 size=3 face="Times New Roman">
```

## 表格语法

Markdown 中表格使用 | 来分隔不同的单元格，使用 - 来分隔表头和其他行，通过 : 号和 - 的相对位置可以来设置表格的对齐方式。

- :- 左对齐

- -: 右对齐

- :-: 居中

下面是一个表格的例子

| 左对齐 | 右对齐 | 居中 |
|:------ |:------:| ----:|
| 1      | 1      | 1    |
| 2      | 2      | 2    |

源码如下

```
| 左对齐 | 右对齐 | 居中 |
|:------ |:------:| ----:|
| 1      | 1      | 1    |
| 2      | 2      | 2    |
```

<table>
    <tr>
        <td>/</td> 
        <td>N</td> 
        <td>5</td> 
   </tr>
    <tr>
        <td rowspan="4">O(N^6)</td>    
  		 <td>I</td> 
      	 <td>1</td>
    </tr>
    <tr>
        <td>T</td> 
        <td>2</td>
    </tr>
    <tr>
        <td>T</td>
        <td>0</td>

    </tr>
    <tr>
        <td>D</td>
        <td>0</td>

    </tr>
</table>

```html
<table>
    <tr>
        <td>/</td> 
        <td>N</td> 
        <td>5</td> 
   </tr>
    <tr>
        <td rowspan="4">O(N^6)</td>    
  		 <td>I</td> 
      	 <td>1</td>
    </tr>
    <tr>
        <td>T</td> 
        <td>2</td>
    </tr>
    <tr>
        <td>T</td>
        <td>0</td>

    </tr>
    <tr>
        <td>D</td>
        <td>0</td>

    </tr>
</table>
```


## 目录

在对应位置使用 [toc] 即可生成全文的目录。

可以通过这个 [在线编辑器](https://markdown.com.cn/editor/) 体验一下Markdown！