# Java 数学减法精确(长 x，长 y)方法

> 原文:[https://www . geesforgeks . org/Java-math-减法 exactlong-x-long-y-method/](https://www.geeksforgeeks.org/java-math-subtractexactlong-x-long-y-method/)

**java.lang.Math .减法精确()**是 java 中的一个内置数学函数，它返回
参数的差值。如果结果溢出很长时间，它将引发异常。由于减法精确(长 x，长 y)是**静态**，
所以不需要创建对象。

**语法:**

```
public static long subtractExact(long x, long y)
Parameter :
 x : the first value
 y : the second value to be subtracted from the first
Return :
This method returns the difference of the arguments.
Exception :
It throws ArithmeticException - if the result overflows a long.

```

**示例:**展示 **java.lang.Math .减法精确()**方法的工作。

```
// Java program to demonstrate working
// of java.lang.Math.subtractExact() method
import java.lang.Math;

class Gfg1 {

    // driver code
    public static void main(String args[])
    {
        long x = 11111111111l;
        long y = 999l;

        System.out.println(Math.subtractExact(x, y));
    }
}
```

**输出:**

```
11111110112

```

```
// Java program to demonstrate working
// of java.lang.Math.subtractExact() method
import java.lang.Math;

class Gfg2 {

    // driver code
    public static void main(String args[])
    {
        long a = Long.MIN_VALUE;
        long b = 1;

        System.out.println(Math.subtractExact(a, b));
    }
}
```

**输出:**

```
Runtime Error :
Exception in thread "main" java.lang.ArithmeticException: long overflow
    at java.lang.Math.subtractExact(Math.java:849)
    at Gfg2.main(File.java:13)

```