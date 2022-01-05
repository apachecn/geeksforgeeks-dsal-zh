# 删除 Java 中字符串的所有非字母字符

> 原文:[https://www . geesforgeks . org/remove-all-非字母字符的 java 字符串/](https://www.geeksforgeeks.org/remove-all-non-alphabetical-characters-of-a-string-in-java/)

给定一个由非字母字符组成的字符串。任务是删除字符串中所有非字母字符，并将单词打印到新的一行。

**示例:**

> **输入:** str = "您好，您好吗？"
> **输出:**
> 你好
> 你好
> 怎么样
> 
> 逗号(，)，空格和问号(？)被移除，字符串 s 中总共有 4 个单词。
> 每个令牌都以其在字符串 s 中出现的相同顺序打印
> 
> **输入:**“阿扎德是个好孩子，不是吗？”
> T3【输出:T5【阿扎德】T6【是】T7
> 好
> 小子
> 不是
> t
> 他

**方法:**非字母字符基本上是任何不是数字或字母的字符。可以是英文字母，空格，感叹号(！)、逗号(，)和问号(？)，句号(。)、下划线(_)、撇号(')和 at 符号(@)。方法是使用 Java [String.split](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#split-java.lang.String-) 方法将字符串分割成一个子字符串数组。然后，按照字符串中出现的顺序，在新行中打印每 n 个单词

下面是上述方法的实现:

```
// Java program to split all
// non-alphabetical characters
import java.util.Scanner;

public class Main {

    // Function to trim the non-alphabetical characters
    static void printwords(String str)
    {

        // eliminate leading and trailing spaces
        str = str.trim();

        // split all non-alphabetic characters
        String delims = "\\W+"; // split any non word
        String[] tokens = str.split(delims);

        // print the tokens
        for (String item : tokens) {

            System.out.println(item + " ");
        }
    }

    public static void main(String[] args)
    {

        String str = "Hello, how are you  ?";
        printwords(str);
    }
}
```

**Output:**

```
Hello 
how 
are 
you

```

**时间复杂度:** O(N)