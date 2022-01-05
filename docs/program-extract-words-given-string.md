# 从给定字符串中提取单词的程序

> 原文:[https://www . geesforgeks . org/program-extract-words-given-string/](https://www.geeksforgeeks.org/program-extract-words-given-string/)

任务是从给定的字符串中提取单词。单词之间可能有一个或多个空格。

**示例:**

```
Input : geeks for geeks
Output : geeks
         for
         geeks

Input : I love   coding.
Output: I 
         love
         coding
```

我们在下面的帖子中讨论了一个解决方案。
[如何在 C/C++、Python 和 Java 中拆分字符串？](https://www.geeksforgeeks.org/how-to-split-a-string-in-cc-python-and-java/)

在这篇文章中，讨论了一个使用 stringstream 的新解决方案。

```
1\. Make a string stream.
2\. extract words from it till there are still words in the stream.
3\. Print each word on new line.
```

即使我们在单词之间有多个空格，这个解决方案也有效。

## C++

```
// C++ program to extract words from
// a string using stringstream
#include<bits/stdc++.h>
using namespace std;

void printWords(string str)
{
    // word variable to store word
    string word;

    // making a string stream
    stringstream iss(str);

    // Read and print each word.
    while (iss >> word)
        cout << word << endl;
}

// Driver code
int main()
{
    string s = "sky is blue";
    printWords(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program for splitting a string
// using split()
import java.io.*;
class GFG
{
    // Method splits String into
    // all possible tokens
    public static void printWords(String s)
    {    
        // Using split function.
        for (String val: s.split(" "))

            // printing the final value.
            System.out.println(val);
    }

    // Driver Code
    public static void main(String args[])
    {
        // Sample string to check the code
        String Str = "sky is blue";

        // function calling
        printWords(Str);
    }
}

// This code is contributed
// by Animesh_Gupta
```

## 蟒蛇 3

```
# Python3 program to extract words from
# a string
def printWords(strr):
    word = strr.split(" ")
    print(*word, sep="\n")

# Driver code
s = "sky is blue"
printWords(s)

# This code is contributed by shubhamsingh10
```

## C#

```
// A C# program for splitting a string
// using split()
using System;
class GFG
{
    // Method splits String into
    // all possible tokens
    public static void printWords(String s)
    {    
        // Using split function.
        foreach(String val in s.Split(" "))

            // printing the final value.
            Console.WriteLine(val);
    }

    // Driver Code
    static public void Main ()
    {
        // Sample string to check the code
        String Str = "sky is blue";

        // function calling
        printWords(Str);
    }
}

// This code is contributed
// by shivanisingh
```

## java 描述语言

```
<script>

// A Javascript program for splitting
// a string using split()

// Method splits String into
// all possible tokens
function printWords(s)
{   
    s = s.split(" ");
    for(let val = 0; val < s.length; val++)
    {
        document.write(s[val] + "</br>");
    }
}

// Driver code

// Sample string to check the code
let Str = "sky is blue";

// function calling
printWords(Str);

// This code is contributed by divyeshrabadiya07

</script>
```

**输出:**

```
sky
is
blue
```

本文由 **Tanya Anand** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。