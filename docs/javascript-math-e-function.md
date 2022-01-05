# JavaScript | Math.exp()函数

> 原文:[https://www.geeksforgeeks.org/javascript-math-e-function/](https://www.geeksforgeeks.org/javascript-math-e-function/)

**Math.exp()** 是 JavaScript 中的一个内置函数，用于获取**e<sup>p</sup>T5】的值，其中 p 是任意给定的数字。
数字 **e** 是一个数学常数，其近似值等于 **2.718** 。**

*   瑞士数学家雅各布·伯努利发现了它。
*   这个数也叫**欧拉数**。

**语法:**

```
Math.exp(p)
```

**参数:**该功能接受单个参数 **p** 为任意数字。
**返回值:**返回 **e <sup>p</sup>** 的值，其中 p 是任意给定的数字作为参数。

**示例:**

```
*Input* : Math.exp(0)
*Output* : 1
```

**说明:**
这里参数 p 的值为 0，所以在 **e <sup>p</sup>**
中放入值 0 而不是 p 后，其值变为 1。

```
*Input* : Math.exp(2)
*Output* : 7.38905609893065
```

**说明:**
这里参数 p 的值是 2，所以在 **e <sup>p</sup>**
中放入值 2 而不是 p 之后，那么它的值就变成了 7.389050930605

让我们看看 JavaScript 程序:

*   **例 1:**

## java 描述语言

```
<script>
  // Here different values is being taken as
  // as parameter of Math.exp() function.
  document.write(Math.exp(0) + "<br>");
  document.write(Math.exp(1) + "<br>");
  document.write(Math.exp(2) + "<br>");
  document.write(Math.exp(-1) + "<br>");
  document.write(Math.exp(-7) + "<br>");
  document.write(Math.exp(10) + "<br>");
  document.write(Math.exp(1.2));
</script>
```

**输出:**

```
1
2.718281828459045
7.38905609893065
0.36787944117144233
0.0009118819655545162
22026.465794806718
3.3201169227365472
```

*   **例 2:** 这里的参数应该是一个数字，否则会给出一个错误或 NaN，即不是一个数字。

## java 描述语言

```
<script>
  // Here alphabet parameter give error.
  document.write(Math.exp(a));
</script>
```

**输出:**

```
Error: a is not defined
```

## java 描述语言

```
<script>
  // Here parameter as a string give NaN.
  document.write(Math.exp("gfg"));
</script>
```

*   **输出:**

```
NaN
```

**支持的浏览器:**由 *JavaScript Math 支持的浏览器。e()功能*如下:

*   谷歌 Chrome
*   微软公司出品的 web 浏览器
*   火狐浏览器
*   歌剧
*   旅行队