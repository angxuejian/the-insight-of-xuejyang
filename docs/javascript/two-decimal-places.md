# Two decimal places


1、使用`toFixed`方法

```js
const number = 123.5678
const roundedNumber = number.toFixed(2)

console.log(roundedNumber);  // '123.57'
```

`toFixed` 可以成功保留小数，但是会更改为**string**类型，并且会四舍五入。

<br/>
<br/>

2、使用`Math.floor`方法
```js
const number = 123.4567;
const truncatedNumber = Math.floor(number * 100) / 100;

console.log(truncatedNumber);  // 123.45
```
`Math.floor` 可以成功保留小数，并且不会更改类型和四舍五入。

根据乘法，`Math.floor(number * 100)` 会得到一个整数，然后除以 100，得到保留两位的小数。