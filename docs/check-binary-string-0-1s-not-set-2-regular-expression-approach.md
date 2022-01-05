# 检查二进制字符串是否有介于 1 和 2 之间的 0 |设置 2(正则表达式方法)

> 原文:[https://www . geesforgeks . org/check-binary-string-0-1s-not-set-2-正则表达式-approach/](https://www.geeksforgeeks.org/check-binary-string-0-1s-not-set-2-regular-expression-approach/)

给定一个 0 和 1 的字符串，我们需要检查给定的字符串是否有效。当 1 之间不存在零时，给定字符串有效。例如，1111，00001111110，1111000 是有效字符串，但 01010011，01010，101 不是。

示例:

```
Input : 100
Output : VALID

Input : 1110001
Output : NOT VALID
There is 0 between 1s

Input : 00011
Output : VALID

```

在[集合 1](https://www.geeksforgeeks.org/check-binary-string-0-between-1s-not/) 中，我们讨论了字符串有效性的一般方法。在这篇文章中，我们将讨论[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)同样的方法，它很简单。

我们知道，在一个字符串中如果 1 之间有零，那么这个字符串是无效的。因此下面是无效字符串模式的正则表达式之一。

```
10+1

```

这是简单的正则表达式算法。

1.  Circular matcher (string)
2.  If the above regular expression match is found in the matcher, then the string is invalid, otherwise it is valid.

```
// Java regex program to check for valid string

import java.util.regex.Matcher;
import java.util.regex.Pattern;

class GFG 
{
    // Method to check for valid string
    static boolean checkString(String str)
    {
        // regular expression for invalid string
        String regex = "10+1";

        // compiling regex
        Pattern p = Pattern.compile(regex);

        // Matcher object
        Matcher m = p.matcher(str);

        // loop over matcher
        while(m.find())
        {
            // if match found,
            // then string is invalid
            return false;
        }

        // if match doesn't found
        // then string is valid
        return true;    
    }

    // Driver method
    public static void main (String[] args)
    {
        String str = "00011111111100000";

        System.out.println(checkString(str) ? "VALID" : "NOT VALID");
    }
}
```

输出:

```
VALID

```

本文由**高拉夫·米格拉尼**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。