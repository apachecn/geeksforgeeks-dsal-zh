# 查找给定字符串中“1(0+)1”的所有模式| SET 2(正则表达式方法)

> 原文:[https://www . geesforgeks . org/find-patterns-101-given-string-set-2 regular-expression-approach/](https://www.geeksforgeeks.org/find-patterns-101-given-string-set-2regular-expression-approach/)

在[集合 1](https://www.geeksforgeeks.org/find-patterns-101-given-string/) 中，我们已经讨论了对形式 1(0+)1 的模式进行计数的一般方法，其中(0+)表示 0 的任何非空连续序列。在这篇文章中，我们将讨论[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)对其进行计数的方法。

**例:**

```
Input : 1101001
Output : 2

Input : 100001abc101
Output : 2

```

下面是上述模式的正则表达式之一

```
10+1

```

因此，每当我们发现匹配时，我们就增加计数器来计算模式。由于匹配的最后一个字符总是“1”，我们必须再次从该索引开始搜索。

```
//Java program to count the patterns 
// of the form 1(0+)1 using Regex

import java.util.regex.Matcher;
import java.util.regex.Pattern;

class GFG 
{
    static int patternCount(String str) 
    {
        // regular expression for the pattern
        String regex = "10+1";

        // compiling regex
        Pattern p = Pattern.compile(regex);

        // Matcher object
        Matcher m = p.matcher(str);

        // counter
        int counter = 0;

        // whenever match found
        // increment counter
        while(m.find())
        {
            // As last character of current match
            // is always one, starting match from that index
            m.region(m.end()-1, str.length());

            counter++;
        }

        return counter;
    }

    // Driver Method
    public static void main (String[] args)
    {
        String str = "1001ab010abc01001";
        System.out.println(patternCount(str));
    }
}
```

输出:

```
2

```

**相关文章:**

*   [Regular expression Java](https://www.geeksforgeeks.org/write-regular-expressions/)
*   [quantifier](https://www.geeksforgeeks.org/quantifiers-in-java/)
*   [Use regex to extract each word from the string](https://www.geeksforgeeks.org/extracting-word-string-java/)
*   [Check whether the given string is a valid number (integer or floating point)](https://www.geeksforgeeks.org/check-given-string-valid-number-integer-floating-point-java-set-2-regular-expression-approach/)
*   [Use Regex to print the first letter of each word in the string](https://www.geeksforgeeks.org/print-first-letter-word-string-using-regex/)

本文由**高拉夫·米格拉尼**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。