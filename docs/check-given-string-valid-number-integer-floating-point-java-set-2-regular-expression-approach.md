# 检查给定的字符串在 Java | SET 2(正则表达式方法)

中是否是有效的数字(整数或浮点)

> 原文:[https://www . geesforgeks . org/check-given-string-valid-number-integer-floating-point-Java-set-2-正则表达式-approach/](https://www.geeksforgeeks.org/check-given-string-valid-number-integer-floating-point-java-set-2-regular-expression-approach/)

在[集合 1](https://www.geeksforgeeks.org/check-given-string-valid-number-integer-floating-point/) 中，我们讨论了检查字符串是否是有效数字的一般方法。在这篇文章中，我们将讨论[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)检查数字的方法。

**例:**

```
Input : str = "11.5"
Output : true

Input : str = "abc"
Output : false

Input : str = "2e10"
Output : true

Input : 10e5.4
Output : false
```

**检查给定的字符串是否是有效的整数**

**对于整数:**下面是整数的常规定义。

```
sign -> + | - | epsilon
digit -> 0 | 1 | .... | 9
num -> sign digit digit*

```

因此整数的正则表达式之一是

```
[+-]?[0-9][0-9]*

```

```
// Java program to check whether given string
// is a valid integer number using regex

import java.util.regex.Matcher;
import java.util.regex.Pattern;

class GFG 
{
    public static void main (String[] args)
    {
        String input1 = "abc";
        String input2 = "1234";

        // regular expression for an integer number
        String regex = "[+-]?[0-9]+";

        // compiling regex
        Pattern p = Pattern.compile(regex);

        // Creates a matcher that will match input1 against regex
        Matcher m = p.matcher(input1);

        // If match found and equal to input1
        if(m.find() && m.group().equals(input1))
            System.out.println(input1 + " is a valid integer number");
        else
            System.out.println(input1 + " is not a valid integer number");

        // Creates a matcher that will match input2 against regex
        m = p.matcher(input2);

        // If match found and equal to input2
        if(m.find() && m.group().equals(input2))
                System.out.println(input2 + " is a valid integer number");    
        else
            System.out.println(input2 + " is not a valid integer number");
    }
}
```

输出:

```
abc is not a valid integer number
1234 is a valid integer number

```

下面是整数

```
[+-]?[0-9]+
[+-]?\d\d*
[+-]?\d+

```

的其他短手正则表达式

**检查给定的字符串是否是有效的浮点数**

**对于浮点数:**下面是浮点数的常规定义。

```
sign -> + | - | epsilon
digit -> 0 | 1 | .... | 9
digits -> digit digit*
optional_fraction -> . digits | epsilon
optional_exponent -> ((E | e) (+ | - | epsilon) digits) | epsilon
num -> sign digits optional_fraction optional_exponent

```

因此浮点数的正则表达式之一是

```
[+-]?[0-9]+(\.[0-9]+)?([Ee][+-]?[0-9]+)?

```

```
//Java program to check whether given string
// is a valid floating point number using regex

import java.util.regex.Matcher;
import java.util.regex.Pattern;

class GFG 
{
    public static void main (String[] args)
    {
        String input1 = "10e5.4";
        String input2 = "2e10";

        // regular expression for a floating point number
        String regex = "[+-]?[0-9]+(\\.[0-9]+)?([Ee][+-]?[0-9]+)?";

        // compiling regex
        Pattern p = Pattern.compile(regex);

        // Creates a matcher that will match input1 against regex
        Matcher m = p.matcher(input1);

        // If match found and equal to input1
        if(m.find() && m.group().equals(input1))
            System.out.println(input1 + " is a valid float number");
        else
            System.out.println(input1 + " is not a valid float number");

        // Creates a matcher that will match input2 against regex
        m = p.matcher(input2);

        // If match found and equal to input2
        if(m.find() && m.group().equals(input2))
                System.out.println(input2 + " is a valid float number");    
        else
            System.out.println(input2 + " is not a valid float number");
    }
}
```

输出:

```
10e5.4 is not a valid float number
2e10 is a valid float number

```

下面是另一个浮点数的短线正则表达式

```
[+-]?\d+(\.\d+)?([Ee][+-]?\d+)?

```

相关文章:[在 Java 中检查给定的字符串是否为有效数字(整数或浮点)](https://www.geeksforgeeks.org/check-if-a-given-string-is-a-valid-number-integer-or-floating-point-in-java/)

本文由**高拉夫·米格拉尼**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。