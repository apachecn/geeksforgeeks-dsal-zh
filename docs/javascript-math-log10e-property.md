# JavaScript 数学 LOG10E 属性

> 原文:[https://www . geesforgeks . org/JavaScript-math-log10e-property/](https://www.geeksforgeeks.org/javascript-math-log10e-property/)

以下是**数学 LOG10E** 属性的示例。

*   **Example:**

## Javascript

```
<script>
  // Here value of Math.LOG10E is printed.
  document.write(Math.LOG10E);                     
</script>
```

**输出:**

```
0.4342944819032518
```

数学。LOG10E 是 JavaScript 中的一个属性，简单来说就是用来求 e 的以 10 为底的对数的值，其中 e 是一个约等于 2.718 的无理数和超越数

**语法:**

```
Math.LOG10E;
```

**返回值:**它只是返回 e 的以 10 为底的对数的值。

下面的例子说明了 JavaScript 中的 Math LOG10E 属性。

*   **Example:** Here, the logarithmic value of e with the base of 10 is simply displayed as the output.

```
Input : Math.LOG10E
Output: 0.4342944819032518
```

上述属性的更多代码如下:

**程序 1:**e 的以 10 为底的对数的值可以如下所示的函数形式打印出来。

## Javascript

```
<script>
  // function is being called.
  function get_Value_of_base_10_lagarithm_of_e()
  {
      return Math.LOG10E;
  }
  // function is calling.
  document.write(get_Value_of_base_10_lagarithm_of_e());
</script>
```

**输出:**

```
0.4342944819032518
```

**程序 2:** 这里我们考虑数学。LOG10E 作为一个函数但实际上它是一个属性

## Javascript

```
<script>
  // Here we consider Math.LOG10E as a function
  // but in actual it is a property that is why
  // error as output is being shown.
  document.write(Math.LOG10E(12));
</script>
```

**输出:**

```
Error: Math.LOG10E is not a function
```

**程序 3:** 每当我们需要求 e 的基数 10 的对数时，我们就借助这个性质。在数学上，它需要很多。

## Javascript

```
<script>
  // Value of Math.LOG10E is printed.
  document.write(Math.LOG10E);
</script>
```

**输出:**

```
0.4342944819032518
```

**支持的浏览器:**

*   谷歌铬
*   Internet browser
*   red fox
*   歌剧
*   旅行队