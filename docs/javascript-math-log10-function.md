# JavaScript | Math.log10()函数

> 原文:[https://www . geesforgeks . org/JavaScript-math-log 10-function/](https://www.geeksforgeeks.org/javascript-math-log10-function/)

Math.log10()是 JavaScript 中的一个内置函数，它给出任何数字的 10 个对数的底值。
**语法:**

```
Math.log10(p)
```

**参数:**该函数接受单个参数 **p** ，该参数是要计算的以 10 为底的对数的任何数字。

**返回:**返回任意数字的以 10 为基数的对数的值。

**示例:**

```
*Input* : Math.log10(5)
*Output*: 0.6989700043360189

```

**说明:**
这里数字 5 的基数 10 对数的值是 0.6989700043360189，如输出所示。

```
*Input* : Math.log10(10)
*Output*:1

```

**我们来看看这个函数的一些 JavaScript 代码:**

*   **Example 1:**

    ```
    <script>
      // Different numbers are being taken
      // as the parameter of the function.
      document.write(Math.log10(1000) + "<br>");
      document.write(Math.log10(12) + "<br>");
      document.write(Math.log10(26) + "<br>");
      document.write(Math.log10(5));
    </script>
    ```

    **输出:**

    ```
    3
    1.0791812460476249
    1.414973347970818
    0.6989700043360189
    ```

*   **Example 2:**

    ```
    <script>
      // Taken parameter from 1 to 19 incremented by 3.
      for (i = 1; i < 20; i += 3) {
          document.write(Math.log10(i) + "<br>");
      }
    </script>
    ```

    **输出:**

    ```
    0
    0.6020599913279624
    0.8450980400142568
    1
    1.1139433523068367
    1.2041199826559248
    1.2787536009528289

    ```

**错误和异常:**这个函数的参数应该总是一个数字，否则它会返回 NaN，也就是说，当它的参数作为字符串时，它不是一个数字。

*   **Example 1:**

    ```
    <script>
      // Parameters for this function should always be a
      // number otherwise it return NaN i.e, not a number
      // when its parameter taken as string.
      document.write(Math.log10("gfg"));
    <script>
    ```

    **输出:**

    ```
    NaN

    ```

*   **Example 2:** This function gives error when its parameter taken as complex number because it accept only integer value as the parameter.

    ```
    <script>
      // Parametes can never be a complex number because
      // it accept only integer value as the parameter.
      document.write(Math.log10(1 + 2i));
    ```

    **输出:**

    ```
    Error: Invalid or unexpected token

    ```

**应用:**每当我们需要任何数字的基数 10 的对数的值时，我们就借助这个函数。它的价值在数学题中需要很多次。
**让我们看看这个应用的 JavaScript 代码:**

*   **Example 1:**

    ```
    <script>
      // taking parameter as number 14 and 
      //calculated in the form of function.
      function value_of_base_10_logarithms_of_any_number()
      {
          return Math.log10(14);
      }
      document.write(value_of_base_10_logarithms_of_any_number());
    </script>
    ```

    **输出:**

    ```
    1.146128035678238
    ```

**支持的浏览器:**JavaScript math . log 10()函数支持的浏览器如下:

*   谷歌 Chrome
*   微软公司出品的 web 浏览器
*   火狐浏览器
*   歌剧
*   旅行队