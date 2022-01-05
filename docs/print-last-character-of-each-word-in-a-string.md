# 打印字符串中每个单词的最后一个字符

> 原文:[https://www . geesforgeks . org/print-字符串中每个单词的最后一个字符/](https://www.geeksforgeeks.org/print-last-character-of-each-word-in-a-string/)

给定字符串 **str** ，任务是打印字符串中每个单词的最后一个字符。

**示例:**

> **输入:** str = "极客换极客"
> **输出:** s r s
> 
> **输入:** str = "计算机应用程序"
> **输出:** r s

**方法:**在给定字符串的末尾添加一个空格，即 **" "** ，这样字符串中的最后一个单词后面也会跟一个空格，就像字符串中的所有其他单词一样。现在开始逐字符遍历字符串，并打印每个后跟空格的字符。
以下是上述办法的实施情况:

## C++

```
// CPP implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to print the last character
// of each word in the given string
void printLastChar(string str)
{

    // Now, last word is also followed by a space
    str = str + " ";
    for (int i = 1; i < str.length(); i++)
    {

        // If current character is a space
        if (str[i] == ' ')

            // Then previous character must be
            // the last character of some word
            cout << str[i - 1] << " ";
    }
}

// Driver code
int main()
{
    string str = "Geeks for Geeks";
    printLastChar(str);
}

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to print the last character
    // of each word in the given string
    static void printLastChar(String str)
    {

        // Now, last word is also followed by a space
        str = str + " ";
        for (int i = 1; i < str.length(); i++) {

            // If current character is a space
            if (str.charAt(i) == ' ')

                // Then previous character must be
                // the last character of some word
                System.out.print(str.charAt(i - 1) + " ");
        }
    }

    // Driver code
    public static void main(String s[])
    {
        String str = "Geeks for Geeks";
        printLastChar(str);
    }
}
```

## 蟒蛇 3

```
# Function to print the last character
# of each word in the given string
def printLastChar(string):

    # Now, last word is also followed by a space
    string = string + " "
    for i in range(len(string)):

        # If current character is a space
        if string[i] == ' ':

            # Then previous character must be
            # the last character of some word
            print(string[i - 1], end = " ")

# Driver code
string = "Geeks for Geeks"
printLastChar(string)

# This code is contributed by Shrikant13
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to print the last character
    // of each word in the given string
    static void printLastChar(string str)
    {

        // Now, last word is also followed by a space
        str = str + " ";
        for (int i = 1; i < str.Length; i++)
        {

            // If current character is a space
            if (str[i] == ' ')

                // Then previous character must be
                // the last character of some word
                Console.Write(str[i - 1] + " ");
        }
    }

    // Driver code
    public static void Main()
    {
        string str = "Geeks for Geeks";
        printLastChar(str);
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to print the last character
// of each word in the given string
function printLastChar($str)
{
    // Now, last word is also followed by a space
    $str = $str . " ";
    for ($i = 1; $i < strlen($str); $i++)
    {
        // If current character is a space
        if (!strcmp($str[$i], ' '))

            // Then previous character must be
            // the last character of some word
            echo($str[$i - 1] . " ");
    }
}

// Driver code
$str = "Geeks for Geeks";
printLastChar($str);

// This code contributed by PrinciRaj1992
?>
```

## java 描述语言

```
<script>
      // JavaScript implementation of the approach
      // Function to print the last character
      // of each word in the given string
      function printLastChar(str) {
        // Now, last word is also followed by a space
        str = str + " ";
        for (var i = 1; i < str.length; i++) {
          // If current character is a space
          if (str[i] === " ")
            // Then previous character must be
            // the last character of some word
            document.write(str[i - 1] + " ");
        }
      }

      // Driver code
      var str = "Geeks for Geeks";
      printLastChar(str);
</script>
```

**Output:** 

```
s r s
```