# JavaScript | Math.log2()函数

> 原文:[https://www . geesforgeks . org/JavaScript-math-log 2-function/](https://www.geeksforgeeks.org/javascript-math-log2-function/)

Math.log2()是 JavaScript 中的一个内置函数，它给出任何数字的基数为 2 的对数的值。
**语法:**

```
Math.log2(p)
```

**参数:**该函数接受单个参数 **p** ，该参数是要计算的以 2 为底的对数的任何数字。

**返回:**返回任意数字的以 2 为基数的对数的值。

**示例:**

```
*Input* : Math.log2(5)

*Output*: 2.321928094887362
```

**解释:**
这里数字 5 的 be 2 对数的值是 2.321928094887362，如输出所示。

```
*Input* : Math.log2(10)
*Output*:3.321928094887362
```

**我们来看看这个函数的一些 JavaScript 代码:**

*   **例 1:**

## java 描述语言

```
<script>
  // Different numbers are being taken
  // as the parameter of the function.
  document.write(Math.log2(1000) + "<br>");
  document.write(Math.log2(12) + "<br>");
  document.write(Math.log2(26) + "<br>");
  document.write(Math.log2(5));
</script>                   
```

**输出:**

```
9.965784284662087
3.584962500721156
4.700439718141092
2.321928094887362
```

*   **例 2:**

## java 描述语言

```
<script>
  // Taken parameter from 1 to 19 incremented by 3.
  for (i = 1; i < 20; i += 3) {
      document.write(Math.log2(i) + "<br>");
  }
</script>
```

**输出:**

```
0
2
2.807354922057604
3.321928094887362
3.700439718141092
4
4.247927513443585
```

**错误和异常:**该函数的参数应该始终是一个数字，否则它会返回 NaN，即当其参数被视为字符串时，它不是一个数字。

*   **例 1:**

## java 描述语言

```
<script>
  // Parameters for this function should always be a
  // number otherwise it return NaN i.e, not a number
  // when its parameter taken as string.
  document.write(Math.log2("gfg"));
</script>
```

**输出:**

```
NaN
```

*   **例 2:** 该函数在参数取复数时给出误差，因为它只接受整数值作为参数。

## java 描述语言

```
<script>
  // Parametes can never be a complex number because
  // it accept only integer value as the parameter.
  document.write(Math.log2(1 + 2i));
</script>
```

**输出:**

```
Error: Invalid or unexpected token
```

**应用:**每当我们需要任何数的基数为 2 的对数的值时，我们就借助这个函数。它的价值在数学题中需要很多次。
**让我们看看这个应用的 JavaScript 代码:**

*   **例 1:**

## java 描述语言

```
<script>
  // taking parameter as number 14 and
  //calculated in the form of function.
  function value_of_base_2_logarithms_of_any_number()
  {
    return Math.log2(14);
  }
  document.write(value_of_base_2_logarithms_of_any_number());
</script>                   
```

**输出:**

```
3.807354922057604
```

**支持的浏览器:**JavaScript math . log 2()函数支持的浏览器如下:

*   谷歌 Chrome
*   微软公司出品的 web 浏览器
*   火狐浏览器
*   歌剧
*   旅行队