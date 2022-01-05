# 从给定字符串中删除标点符号

> 原文:[https://www . geesforgeks . org/remove-标点符号-给定-字符串/](https://www.geeksforgeeks.org/removing-punctuations-given-string/)

给定一个字符串，如果给定的字符是按当前 C 语言环境分类的标点字符，则删除该字符串中的标点符号。默认的 C 语言环境将这些字符分类为标点符号:

```
!"#$%&'()*+,-./:;?@[\]^_`{|}~ 
```

**例:**

```
Input : %welcome' to @geeksforgeek<s
Output : welcome to geeksforgeeks

Input : Hello!!!, he said ---and went.
Output : Hello he said and went
```

设计了一个循环，遍历由该字符串的字符和标点组成的列表，删除标点，然后将它们连接起来。

## C++

```
// CPP program to remove punctuation from a given string

#include <iostream>
using namespace std;

int main()
{
    // input string
    std::string str = "Welcome???@@##$ to#$% Geeks%$^for$%^&Geeks";

    for (int i = 0, len = str.size(); i < len; i++)
    {
        // check whether parsing character is punctuation or not
        if (ispunct(str[i]))
        {
            str.erase(i--, 1);
            len = str.size();
        }
    }

    // print string without punctuation
    std::cout << str;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove punctuation from a given string

public class Test
{
    public static void main(String[] args)
    {
        // input string
        String str = "Welcome???@@##$ to#$% Geeks%$^for$%^&Geeks";

        // similar to Matcher.replaceAll
        str = str.replaceAll("\\p{Punct}","");

        System.out.println(str);
    }

}
// This code is contributed by Gaurav Miglani
```

## 计算机编程语言

```
# Python program to remove punctuation from a given string
# Function to remove punctuation
def Punctuation(string):

    # punctuation marks
    punctuations = '''!()-[]{};:'"\,<>./?@#$%^&*_~'''

    # traverse the given string and if any punctuation
    # marks occur replace it with null
    for x in string.lower():
        if x in punctuations:
            string = string.replace(x, "")

    # Print string without punctuation
    print(string)

# Driver program
string = "Welcome???@@##$ to#$% Geeks%$^for$%^&Geeks"
Punctuation(string)
```

## C#

```
// C# program to remove punctuation
// from a given string
using System;
using System.Text.RegularExpressions;                

class GFG
{
public static void Main()
{
    // input string
    String str = "Welcome???@@##$ to#$% Geeks%$^for$%^&Geeks";

    // similar to Matcher.replaceAll
    str = Regex.Replace(str,@"[^\w\d\s]","");

    Console.Write(str);
}
}

// This code is contributed
// by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to remove punctuation from a given string
    {
        // input string
        var str = "Welcome???@@##$ to#$% Geeks%$^for$%^&Geeks";

        // similar to Matcher.replaceAll
        str = str.replace(/[^a-zA-Z ]/g, "");

        document.write(str);
    }

// This code is contributed by shivanisingh

</script>
```

**输出:**

```
Welcome to GeeksforGeeks
```

本文由**普拉莫德·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。