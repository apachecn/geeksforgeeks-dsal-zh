# 在 Java 中使用正则表达式获取字符串中每个单词的第一个字母

> 原文:[https://www . geesforgeks . org/get-first-letter-word-string-using-regex-Java/](https://www.geeksforgeeks.org/get-first-letter-word-string-using-regex-java/)

给定一个字符串，提取其中每个单词的第一个字母。“单词”被定义为字母字符的连续串，即任何大写或小写字符 a-z 或 A-Z

示例:

```
Input : Geeks for geeks
Output :Gfg

Input : United Kingdom
Output : UK

```

下面是[正则表达式](https://www.geeksforgeeks.org/regular-expressions-in-java/)提取每个单词的第一个字母。它使用'/b '(边界匹配器之一)。请参考[如何写正则表达式？](https://www.geeksforgeeks.org/write-regular-expressions/)要学会它。

```
\b[a-zA-Z]

```

```
// Java program to demonstrate extracting first
// letter of each word using Regex
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class Test
{
    static void printFirst(String s)
    {
        Pattern p = Pattern.compile("\\b[a-zA-Z]");
        Matcher m = p.matcher(s);

        while (m.find())
            System.out.print(m.group());

        System.out.println();
    }

    public static void main(String[] args)
    {
        String s1 = "Geeks for Geeks";
        String s2 = "A Computer Science Portal for Geeks";
        printFirst(s1);
        printFirst(s2);
    }
}
```

输出:

```
GfG
ACSPfG

```

本文由**高拉夫·米格拉尼**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。