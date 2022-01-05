# JavaScript | Math.ceil()函数

> 原文:[https://www . geesforgeks . org/JavaScript-math-ceil-function/](https://www.geeksforgeeks.org/javascript-math-ceil-function/)

JavaScript 中的 **Math.ceil()** 函数用于将作为参数传递的数字舍入到其在**向上舍入方向**上最接近的整数，即舍入到更大的值。

**语法**

```
Math.ceil(value)
```

**参数:**该函数接受单个参数是向上舍入法中要舍入到其
最近整数的数字。
**对作为参数传递给函数的数字进行舍入后，返回:**结果。

**示例:**

```
*Input*  : Math.ceil(4.23)
*Output* : 5

*Input*  : Math.ceil(0.8)
*Output* : 1

```

**错误和异常:**

*   作为参数传递的非数字字符串**返回 NaN**
*   作为参数传递的超过 1 个整数的**数组返回 NaN**
*   作为参数传递的**空变量返回 NaN**
*   作为参数传递的空字符串返回 NaN
*   作为参数传递的**空数组**返回 NaN

下面是一些例子，说明了 JavaScript 中的 Math.ceil()函数:

*   **Example: 1**

    ```
    <!-- NEGATIVE NUMBER EXAMPLE -->
    <script type="text/javascript">
        document.write(Math.ceil(-2) + "<br>"); 
        document.write(Math.ceil(-2.56));          
    </script>
    ```

    **输出:**

    ```
    -2
    -2

    ```

    *   **Example:2**

    ```
    <!-- POSITIVE NUMBER EXAMPLE -->
    <script type="text/javascript">
        document.write(Math.ceil(2) + "<br>"); 
        document.write(Math.ceil(2.56));          
    </script>
    ```

    **输出:**

    ```
    2
    3

    ```

    *   **Example 2:**

    ```
    <!-- STRING EXAMPLE -->
    <script type="text/javascript">
        document.write(Math.ceil("Geeksforgeeks"));          
    </script>
    ```

    **输出:**

    ```
    NaN

    ```

    *   **Example:3**

    ```
    <!-- ADDITION INSIDE FUNCTION EXAMPLE -->
    <script type="text/javascript">
        document.write(Math.ceil(7+9));           
    </script>
    ```

    **输出:**

    ```
    16

    ```

    **支持的浏览器:**JavaScript math . ceil()函数支持的浏览器如下:

    *   谷歌 Chrome
    *   微软公司出品的 web 浏览器
    *   火狐浏览器
    *   歌剧
    *   旅行队