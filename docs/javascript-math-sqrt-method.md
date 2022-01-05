# JavaScript 数学 sqrt()方法

> 原文:[https://www.geeksforgeeks.org/javascript-math-sqrt-method/](https://www.geeksforgeeks.org/javascript-math-sqrt-method/)

下面是**数学 sqrt()** 方法的例子。

*   **例:**

    ```
    <script type="text/javascript">
        document.write(Math.sqrt(-2) + "<br>"); 
        document.write(Math.sqrt(-2.56));          
    </script>
    ```

*   **输出:**

    ```
    NaN
    NaN

    ```

JavaScript 中的 **Math.sqrt()** 方法用于计算作为参数传递给函数的数字的平方根。
**语法**

```
Math.sqrt(value)
```

**参数:**该方法接受如上所述的单个参数，如下所述:

*   **值**保存要计算平方根的数字。

**返回:**作为参数传递的数字的平方根。

下面的例子说明了 JavaScript 中的 Mathe sqrt()方法:

*   **例 1:**

    ```
    Input : Math.sqrt(4)
    Output : 2
    ```

    *   **Example 2:**

    ```
    Input : Math.sqrt(-4)
    Output : NaN
    ```

    **错误和异常:**

    *   作为参数传递的非数字字符串**返回 NaN**
    *   作为参数传递的超过 1 个整数的**数组返回 NaN**
    *   作为参数传递的一个**负数**返回 NaN
    *   作为参数传递的空字符串返回 NaN
    *   作为参数传递的**空数组**返回 NaN

    以上方法的更多代码如下:
    **程序 1:**

    ```
    <script type="text/javascript">
        document.write(Math.sqrt(2) + "<br>"); 
        document.write(Math.sqrt(2.56));          
    </script>
    ```

    **输出:**

    ```
    1.4142135623730951
    1.6

    ```

    **程序 2:**

    ```
    <script type="text/javascript">
        document.write(Math.floor("Geeksforgeeks"));          
    </script>
    ```

    **输出:**

    ```
    NaN

    ```

    **程序 3:**

    ```
    <script type="text/javascript">
        document.write(Math.floor(7.2+9.3));           
    </script>
    ```

    **输出:**

    ```
    4.06201920231798
    ```

    **支持的浏览器:**

    *   谷歌 Chrome
    *   微软公司出品的 web 浏览器
    *   火狐浏览器
    *   歌剧
    *   旅行队