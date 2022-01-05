# JavaScript 数学 asinh()方法

> 原文:[https://www.geeksforgeeks.org/javascript-math-asinh-method/](https://www.geeksforgeeks.org/javascript-math-asinh-method/)

下面是**数学 asinh( )** 方法的例子。

*   **例:**

    ```
    <script>
       // Here different values is being used for
       // getting hyperbolic sine function's values.
       document.write(Math.asinh(3));
       document.write(Math.asinh(22));
       document.write(Math.asinh(-1));
       document.write(Math.asinh(1));
    </script>
    ```

*   **输出:**

    ```
     1.8184464592320668
     3.7847057630994327
    -0.881373587019543
     0.881373587019543

    ```

**数学 asinh()** 方法用来得到一个数的双曲反正弦。双曲反正弦有很多名字，比如双曲逆弦和阿辛。它是双曲正弦函数的逆函数，即任何值的反双曲正弦，比如 x 是值 y，y 的双曲余弦是 x

> 如果 y = asinh(x)
> 那么 x = sinh(y)
> 我们有，
> acosh(x)= ln(x+√x<sup>2</sup>+1)

**语法:**

```
Math.asinh(x)
```

**参数:**该方法接受如上所述的单个参数，如下所述:

*   **x:** 这里 x 是一个将要计算双曲反正弦的数。

**返回值:**返回给定数字的双曲反正弦。

下面的例子说明了 JavaScript 中的数学 asinh()方法:

*   **示例 1:** 在此示例中，在 math.asinh()函数中传递了一个正整数“2”作为参数。它返回传递参数的双曲反正弦。

    ```
    Input : Math.asinh(2)
    Output : 1.4436354751788103
    ```

*   **示例 2:** 在本例中，“0”作为参数在 math.asinh()函数中传递。它返回传递参数的双曲反正弦。

    ```
    Input : Math.asinh(0)
    Output : 0
    ```

*   **示例 3:** 在此示例中，在 math.asinh()函数中传递了一个负整数“-1”作为参数。它返回传递参数的双曲反正弦。

    ```
    Input : Math.asinh(-1)
    Output : -0.881373587019543
    ```

以上方法的更多示例代码如下:
**程序 1:** 每当我们需要获取一个数字的双曲反正弦时，我们可以借助 JavaScript 中的 Math.asinh()函数。

```
<script>
    // Here different values is being used
    // for getting hyperbolic cosine function's values.
    document.write(Math.asinh(5)+"<br>");
    document.write(Math.asinh(12));
</script>
```

**输出:**

```
 2.3124383412727525
 3.179785437699879

```

**程序 2:**

```
<script>
    // Here different values is being used
    // for getting hyperbolic cosine function's values.
    document.write(Math.asinh('Geeks')+"<br>");
    document.write(Math.asinh('Geeksforgeeks'));
</script>    
```

**输出:**

```
NaN
NaN

```

**支持的浏览器:**

*   谷歌 Chrome 38.0
*   Internet Explorer 12.0
*   Firefox 25.0
*   Opera 8.0
*   Safari 25.0