# Java 中的 Math floorDiv()方法

> 原文:[https://www.geeksforgeeks.org/java-floordiv-method-in-math/](https://www.geeksforgeeks.org/java-floordiv-method-in-math/)

**java . lang . math . BloodDiv()**是 Java 中的内置数学函数，它返回小于或等于代数商的最大(最接近正无穷大)int 值。由于 floorDiv()是**静态的**，所以不需要创建对象。

**语法:**

```
public static int floorDiv(data_type x, data_type y)
```

**参数:**该函数接受两个参数，如下所述。

*   **x:** 第一个参数是指分红值。
*   **y:** The second parameter refers to the divisor value.

    参数可以是数据类型 *int* 或 *long。*

例外:

*   **算术异常:**如果除数为零，则抛出算术异常。

**返回值:**此方法返回小于或等于代数商的最大(最接近于正无穷大)整数值。

下面的程序举例说明了 Java . lang . math . flooddiv()方法:

**程序 1:**

```
// Java program to demonstrate working
// of java.lang.Math.floorDiv() method
import java.lang.Math;

class Gfg1{

    // driver code
    public static void main(String args[])
    {
        int a = 25, b = 5;
        System.out.println(Math.floorDiv(a, b));

        // 125/50 value is 2.5, but as output is integer
        // less than or equal to 2.5, So output is 2
        int c = 125, d = 50;
        System.out.println(Math.floorDiv(c, d));
    }
}
```

**Output:**

```
5
2

```

**程序 2:**

```
// Java program to demonstrate working
// of java.lang.Math.floorDiv() method
import java.lang.Math;

class Gfg2 {

    // driver code
    public static void main(String args[])
    {
        int x = 200;
        int y = 0;

        System.out.println(Math.floorDiv(x, y));
    }
}
```

**输出:**

```
Runtime Error :
Exception in thread "main" java.lang.ArithmeticException: / by zero
    at java.lang.Math.floorDiv(Math.java:1052)
    at Gfg2.main(File.java:13)

```