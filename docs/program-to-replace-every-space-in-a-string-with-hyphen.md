# 用连字符

替换字符串中每个空格的程序

> 原文:[https://www . geeksforgeeks . org/program-to-用连字符替换字符串中的每个空格/](https://www.geeksforgeeks.org/program-to-replace-every-space-in-a-string-with-hyphen/)

给定一个字符串，任务是用连字符“-”替换单词之间的所有空格。
**例:**

```
Input: str = "Geeks for Geeks."
Output: Geeks-for-Geeks.

Input: str = "A computer science portal for geeks"
Output: A-computer-science-portal-for-geeks
```

**进场:**

1.  逐个字符遍历整个字符串。
2.  如果字符是空格，用连字符“-”替换。

下面是上述方法的实现:

## C++

```
// C++ program to replace space with -

#include <cstring>
#include <iostream>
using namespace std;

int main()
{

    // Get the String
    string str = "A computer science portal for geeks";

    // Traverse the string character by character.
    for (int i = 0; i < str.length(); ++i) {

        // Changing the ith character
        // to '-' if it's a space.
        if (str[i] == ' ') {

            str[i] = '-';
        }
    }

    // Print the modified string.
    cout << str << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to replace space with -

class GFG
{

    // Function to replace Space with -
    static String replaceSpace(String str)
    {

        String s = "";

        // Traverse the string character by character.
        for (int i = 0; i < str.length(); ++i) {

            // Changing the ith character
            // to '-' if it's a space.
            if (str.charAt(i) == ' ')
                s += '-';

            else
                s += str.charAt(i);

        }

        // return the modified string.
        return s;

    }

    public static void main(String []args)
    {

        // Get the String
        String str = "A computer science portal for geeks";

        System.out.println(replaceSpace(str));

    }

}
```

## 蟒蛇 3

```
# Python 3 program to replace space with -

# Driver Code
if __name__ == '__main__':

    # Get the String
    str = "A computer science portal for geeks"

    # Traverse the string character by character.
    for i in range(0, len(str), 1):

        # Changing the ith character
        # to '-' if it's a space.
        if (str[i] == ' '):
            str = str.replace(str[i], '-')

    # Print the modified string.
    print(str)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```

// C# program to replace space with -
using System;
public class GFG
{

    // Function to replace Space with -
    static String replaceSpace(String str)
    {

        String s = "";

        // Traverse the string character by character.
        for (int i = 0; i < str.Length; ++i) {

            // Changing the ith character
            // to '-' if it's a space.
            if (str[i] == ' ')
                s += '-';

            else
                s += str[i];

        }

        // return the modified string.
        return s;

    }

    public static void Main()
    {

        // Get the String
        String str = "A computer science portal for geeks";

        Console.Write(replaceSpace(str));

    }

}
// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to replace space with -

// Get the String
$str = "A computer science portal for geeks";

// Traverse the string character by character.
for ($i = 0; $i < strlen($str); ++$i)
{

    // Changing the ith character
    // to '-' if it's a space.
    if ($str[$i] == ' ')
    {
        $str[$i] = '-';
    }
}

// Print the modified string.
echo $str . "\n";

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>
      // JavaScript program to replace space with -

      // Get the String
      var str = "A computer science portal for geeks";

      var newStr = str.split("");

      // Traverse the string character by character.
      for (var i = 0; i < newStr.length; ++i) {
        // Changing the ith character
        // to '-' if it's a space.
        if (newStr[i] === " ") {
          newStr[i] = "-";
        }
      }

      // Print the modified string.
      document.write(newStr.join("") + "<br>");
    </script>
```

**Output:** 

```
A-computer-science-portal-for-geeks
```