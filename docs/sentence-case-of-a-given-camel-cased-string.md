# 给定驼色套管管柱的句子情况

> 原文:[https://www . geesforgeks . org/句子-给定大小写-骆驼大小写-字符串/](https://www.geeksforgeeks.org/sentence-case-of-a-given-camel-cased-string/)

给定一个字符串**字符串**(格式为**【卡米凯斯】**，任务是将该字符串转换为可读形式。
**例:**

> **输入:**str = " ilovegeekforgeks "
> **输出:**我爱极客就爱极客
> **输入:** str = "WeLoveToCode"
> **输出:**我们爱编码

**Approach:** 字符串是 camelCased，表示单词之间没有空格分隔，而是每个大写字母都表示一个新单词已经开始。为了提高可读性，我们将其转换为句子大小写。下面给出了转换代码。我们遍历字符串，然后每当遇到小写字母时，我们就这样打印出来。当我们遇到大写字母时，我们输出空格后跟大写字符(转换为小写后)，然后是其余字符。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the original string
// after converting it back from camelCase
void getOrgString(string s)
{

    // Print the first character as it is
    cout << s[0];

    // Traverse the rest of the
    // characters one by one
    int i = 1;
    while (i < s.length()) {

        // If current character is uppercase
        // print space followed by the
        // current character in lowercase
        if (s[i] >= 'A' && s[i] <= 'Z')
            cout << " " << (char)tolower(s[i]);

        // Else print the current character
        else
            cout << s[i];
        i++;
    }
}

// Driver code
int main()
{
    string s = "ILoveGeeksForGeeks";

    getOrgString(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the original string
    // after converting it back from camelCase
    static void getOrgString(String s)
    {

        // Print the first character as it is
        System.out.print(s.charAt(0));

        // Traverse the rest of the
        // characters one by one
        int i = 1;
        while (i < s.length())
        {

            // If current character is uppercase
            // print space followed by the
            // current character in lowercase
            if (s.charAt(i) >= 'A' && s.charAt(i) <= 'Z')
                System.out.print(" "+ Character.toLowerCase(s.charAt(i)));

            // Else print the current character
            else
                System.out.print(s.charAt(i));

            i++;
        }
    }

    // Driver code
    public static void main (String[] args)
    {
                String s = "ILoveGeeksForGeeks";
                getOrgString(s);
    }
}

// This code is contributed by AnkitRai01
```

## 计算机编程语言

```
# Python3 implementation of the approach

# Function to return the original string
# after converting it back from camelCase
def getOrgString(s):

    # Print the first character as it is
    print(s[0],end="")

    # Traverse the rest of the
    # characters one by one
    i = 1
    while (i < len(s)):

        # If current character is uppercase
        # prspace followed by the
        # current character in lowercase
        if (ord(s[i]) >= ord('A') and ord(s[i] )<= ord('Z')):
            print(" ",s[i].lower(),end="")

        # Else print the current character
        else:
            print(s[i],end="")
        i+=1

# Driver code

s = "ILoveGeeksForGeeks"

getOrgString(s)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the original string
    // after converting it back from camelCase
    static void getOrgString(String s)
    {

        // Print the first character as it is
        Console.Write(s[0]);

        // Traverse the rest of the
        // characters one by one
        int i = 1;
        while (i < s.Length)
        {

            // If current character is uppercase
            // print space followed by the
            // current character in lowercase
            if (s[i] >= 'A' && s[i] <= 'Z')
                Console.Write(" "+ char.ToLower(s[i]));

            // Else print the current character
            else
                Console.Write(s[i]);

            i++;
        }
    }

    // Driver code
    public static void Main (String[] args)
    {
                String s = "ILoveGeeksForGeeks";
                getOrgString(s);
    }
}

/* This code is contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>
      // JavaScript implementation of the approach
      // Function to return the original string
      // after converting it back from camelCase
      function getOrgString(s)
      {

        // Print the first character as it is
        document.write(s[0]);

        // Traverse the rest of the
        // characters one by one
        var i = 1;
        while (i < s.length)
        {

          // If current character is uppercase
          // print space followed by the
          // current character in lowercase
          if (
            s[i].charCodeAt(0) >= "A".charCodeAt(0) &&
            s[i].charCodeAt(0) <= "Z".charCodeAt(0)
          )
            document.write("  " + s[i].toLowerCase());

          // Else print the current character
          else document.write(s[i]);
          i++;
        }
      }

      // Driver code
      var s = "ILoveGeeksForGeeks";
      getOrgString(s);

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
I love geeks for geeks
```