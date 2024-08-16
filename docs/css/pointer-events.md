# Pointer events

`pointer-events` CSS 属性指定在什么情况下 (如果有) 某个特定的图形元素可以成为鼠标事件的 target

1、none

对一个元素进行样式设置时，该元素将不会响应任何鼠标事件（例如点击、悬停、拖动等），并且这些事件会传递给该元素下面的其他元素。

<h4>示例：</h4>

1. 让元素透明于鼠标事件。在某些情况下，你可能希望一个元素（比如一个浮动的提示框或动画效果）不会阻挡鼠标事件，使得下层的内容可以被点击或交互。此时，你可以对这个元素应用 pointer-events: none。
2. 创建只用于视觉效果的元素。如果你有一个仅用于视觉效果（例如装饰性背景或动画效果）的元素，而不希望它阻挡鼠标事件，可以使用 pointer-events: none。

```css
pointer-events: none
```