# Align content

`align-content` 是用来控制多行或多列的项目在其父容器中的对齐方式的属性。它主要用于Flex布局和Grid布局中。

1、center

[2024年4月16日起](https://web.dev/blog/align-content-block?hl=zh-cn)，默认布局(flow)中借助`align-content: center`实现了让元素内容垂直居中，无须借助Flexbox布局和Grid布局来实现垂直居中

```html
<div style='align-content: center;'>
    Content.
</div>
```

版本：Chrome: 123 | Firefox: 125 | Safari: 17.4


