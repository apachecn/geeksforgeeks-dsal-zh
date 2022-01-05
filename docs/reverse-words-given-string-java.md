# 在 Java 中反转给定字符串中的单词

> 原文:[https://www . geesforgeks . org/reverse-words-given-string-Java/](https://www.geeksforgeeks.org/reverse-words-given-string-java/)

让我们来看看一种不用任何字符串库函数就能在 Java 中反转给定字符串的方法

示例:

```
Input : "Welcome to geeksforgeeks"
Output : "geeksforgeeks to Welcome"

Input : "I love Java Programming"
Output :"Programming Java love I"

```

先决条件:[Java 中的正则表达式](https://www.geeksforgeeks.org/regular-expressions-in-java/)

```
// Java Program to reverse a String
// without using inbuilt String function
import java.util.regex.Pattern;
public class Exp {

    // Method to reverse words of a String
    static String reverseWords(String str)
    {

        // Specifying the pattern to be searched
        Pattern pattern = Pattern.compile("\\s");

        // splitting String str with a pattern
        // (i.e )splitting the string whenever their
        //  is whitespace and store in temp array.
        String[] temp = pattern.split(str);
        String result = "";

        // Iterate over the temp array and store
        // the string in reverse order.
        for (int i = 0; i < temp.length; i++) {
            if (i == temp.length - 1)
                result = temp[i] + result;
            else
                result = " " + temp[i] + result;
        }
        return result;
    }

    // Driver methods to test above method
    public static void main(String[] args)
    {
        String s1 = "Welcome to geeksforgeeks";
        System.out.println(reverseWords(s1));

        String s2 = "I love Java Programming";
        System.out.println(reverseWords(s2));
    }
}
```

输出:

```
geeksforgeeks to Welcome
Programming Java love I

```

你可以在这里找到[在字符串](https://www.geeksforgeeks.org/reverse-words-in-a-given-string/)中倒排单词的 c++解决方案

本文由 **Sumit Ghosh** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。