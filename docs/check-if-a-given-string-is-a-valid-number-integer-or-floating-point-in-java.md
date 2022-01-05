# 检查给定字符串在 Java 中是否为有效数字(整数或浮点)

> 原文:[https://www . geeksforgeeks . org/check-如果给定字符串是有效的数字整数或浮点 java/](https://www.geeksforgeeks.org/check-if-a-given-string-is-a-valid-number-integer-or-floating-point-in-java/)

在文章[检查给定字符串是否为有效数字](https://www.geeksforgeeks.org/check-given-string-valid-number-integer-floating-point/)中，我们讨论了检查字符串是否为有效数字的一般方法。在 Java 中，我们可以使用 [Wrapper 类](https://www.geeksforgeeks.org/wrapper-classes-java/) ***parse()*** 方法和 [try-catch 块](https://www.geeksforgeeks.org/flow-control-in-try-catch-finally-in-java/)来检查一个数字。

**为整数**

[整数类](https://www.geeksforgeeks.org/java-lang-integer-class-java/)提供了一个静态方法 *parseInt()* 如果字符串不包含可解析的 *int* ，将抛出 NumberFormatException。我们将使用 catch 块捕获这个异常，从而确认给定的字符串不是有效的整数。下面是 java 程序来演示同样的情况。

```
//Java program to check whether given string
// is a valid integer number

class GFG 
{
    public static void main (String[] args)
    {
        String input1 = "abc";
        String input2 = "1234";

        try 
        {
            // checking valid integer using parseInt() method
            Integer.parseInt(input1);
            System.out.println(input1 + " is a valid integer number");
        } 
        catch (NumberFormatException e) 
        {
            System.out.println(input1 + " is not a valid integer number");
        }

        try 
        {
            // checking valid integer using parseInt() method
            Integer.parseInt(input2);
            System.out.println(input2 + " is a valid integer number");
        } 
        catch (NumberFormatException e)
        {
            System.out.println(input2 + " is not a valid integer number");
        }
    }
}
```

输出:

```
abc is not a valid integer number
1234 is a valid integer number

```

**为浮点数**

[Float 类](https://www.geeksforgeeks.org/java-lang-float-class-in-java/)提供了一个静态方法 *parseFloat()* 如果字符串不包含可解析的 *float* ，将引发 NumberFormatException。我们将使用 catch 块捕获这个异常，从而确认给定的字符串不是有效的浮点数。如果字符串为 *null* ，该方法将抛出 [NullPointerException](https://www.geeksforgeeks.org/null-pointer-exception-in-java/) 。下面是 java 程序来演示同样的情况。

```
// Java program to check whether given string
// is a valid float number.

class GFG 
{
    public static void main (String[] args)
    {
        String input1 = "10e5.4";
        String input2 = "2e10";

        try
        {
            // checking valid float using parseInt() method
            Float.parseFloat(input1);
            System.out.println(input1 + " is a valid float number");
        } 
        catch (NumberFormatException e)
        {
            System.out.println(input1 + " is not a valid float number");
        }

        try 
        {
            // checking valid float using parseInt() method
            Float.parseFloat(input2);
            System.out.println(input2 + " is a valid float number");
        } 
        catch (NumberFormatException e)
        {
            System.out.println(input2 + " is not a valid float number");
        }
    }
}
```

输出:

```
10e5.4 is not a valid float number
2e10 is a valid float number

```

**大数字**

对于大数，我们可以使用 [BigInteger](https://www.geeksforgeeks.org/biginteger-class-in-java/) 和 [BigDecimal](https://docs.oracle.com/javase/7/docs/api/java/math/BigDecimal.html) 类构造函数。下面是 java 程序来演示同样的情况。

```
// Java program to check whether given string
// is a valid number.

import java.math.BigInteger;
import java.math.BigDecimal;

class GFG 
{
    public static void main (String[] args)
    {
        String input1 = "1231456416541214651356151564651954156";
        String input2 = "105612656501606510651e655.4";
        String input3 = "2e102225";

        try 
        {
            // checking valid integer number using BigInteger constructor
            new BigInteger(input1);
            System.out.println(input1 + " is a valid integer number");
        } 
        catch (NumberFormatException e) 
        {
            System.out.println(input1 + " is not a valid integer number");
        }

        try 
        {
            // checking valid float number using BigDecimal constructor
            new BigDecimal(input2);
            System.out.println(input2 + " is a valid float number");
        } 
        catch (NumberFormatException e)
        {
            System.out.println(input2 + " is not a valid float number");
        }

        try 
        {
            // checking valid float number using BigDecimal constructor
            new BigDecimal(input3);
            System.out.println(input3 + " is a valid float number");
        } 
        catch (NumberFormatException e)
        {
            System.out.println(input3 + " is not a valid float number");
        }

    }
}
```

输出:

```
1231456416541214651356151564651954156 is a valid integer number
105612656501606510651e655.4 is not a valid float number
2e102225 is a valid float number

```

本文由**高拉夫·米格拉尼**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。