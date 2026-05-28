# CSS 技巧


> [原文地址](https://markodenic.com/css-tips)，原文章中的示例并不会搬运过来，这里只作为翻译正文。


## 什么是CSS？

[层叠样式表 (CSS)](https://markodenic.com/category/css/)是一种样式表语言，用于描述用HTML等标记语言编写文档的呈现方式。CSS还是实现万维网的主要技术之一，当然还有[HTML](https://markodenic.com/category/html/)与[JavaScript](https://markodenic.com/category/javascript/)

[CSS](https://markodenic.com/category/css/)专门设计用于将页面表现（样式）与内容进行分离，包括布局、颜色、字体。这样的设计可以提高内容的阅读性，并且在页面表现（样式）定义上可以提高更多的灵活性与控制能力，使用单独的`.css`文件可以让多个网页共享样式，减少内容的复杂性和重复性。

## 打字机效果

你是否知道只使用CSS就可以实现打字机效果？

## 投影

当你处理透明图片时，你可以优先使用 `filter`中的 `drop-shadow()`方法来给图片内容创建阴影，而不是去使用`box-shadow`属性（该属性会在整个元素盒子后面创建一个矩形阴影）。


filter: drop-shadow(2px 4px 8px #585858);

## 平滑滚动

无需使用JavaScript，只需使用一行CSS即可实现平滑滚动。


## 居中

只需使用三行CSS，即可轻松实现任何元素的垂直和水平居中。

探索其他[ div 居中的方法](https://markodenic.com/snippets/css/center-a-div/)。


## 光标

你是否知道你可以使用`自己的图片`或者`表情`来定义光标样式。

## 截断文本

你是否知道可以使用纯CSS来实现文本截断

## 截断指定行数的文本

你可以使用`-webkit-line-clamp`属性来截断指定行数的文本，并且在截断处会显示省略号。


## CSS `::selection`伪元素

CSS `::selection`伪元素将样式应用于用户选中的文本区域。（例如在文本上进行点击并拖动鼠标）


## 调整元素尺寸

你是否知道你可以调整任何元素的尺寸，就像`<textarea>`？

> 块元素需要搭配 `overflow: auto;`。译者新增非原文

## CSS模态框

无需JavaScript，你可以使用CSS `:target`伪类来创建模态框

> `<a href="#btn">open</a>` / `<a href="#">close</a>`。译者新增非原文

## `calc()`

`calc()`是CSS的函数，允许你计算指定CSS属性值。

## 空元素样式

当元素没有子元素或内容时，你可以使用CSS`:empty`选择器来设置其样式。

## 你可以创建自定义滚动条

## position: sticky;

只需两行CSS，你就可以创建顶部磁吸效果。

## CSS滚动吸附

你可以使用CSS滚动吸附功能来创建良好可控的滚动体验。

## 动态提示框

使用CSS `attr()`函数来创建动态提示框。

## caret-color

你可以改变文本输入框的光标颜色。

## `::in-range`和`::out-of-range`伪类

使用`::in-range`和`::out-of-range`伪类，可以为当前值位于 `min` 和 `max` 范围内或范围外的输入框设置样式。

## 花体字

使用CSS`background-clip`属性来创建漂亮的标题。

## 弹性间距

使用CSS`gap`属性来设置行和列之间的间距。

## grayscale() 函数

使用 CSS filter `grayscale()`函数，可以将输入图像转换为灰度图像。

## 创建漂亮的圆角渐变边框：

<br>

---

<br>

编码愉快！

还想了解更多？这里有如何创建[CSS呼吸动画](https://markodenic.com/css-pulse-animation/)教程。

<br>
<br>

> 旨在学习英语而开启的翻译篇章，翻译均为自己理解和第三方工具帮助。