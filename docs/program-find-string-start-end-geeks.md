# 查找一个字符串是否以另一个给定的字符串开始和结束

> 原文:[https://www . geesforgeks . org/program-find-string-start-end-geeks/](https://www.geeksforgeeks.org/program-find-string-start-end-geeks/)

给定一个字符串和一个角字符串 cs，我们需要找出字符串是否以角字符串 cs 开始和结束。
**例:**

```
Input : str = "geeksmanishgeeks", cs = "geeks"
Output : Yes

Input : str = "shreya dhatwalia", cs = "abc"
Output : No
```

**算法**

*   查找给定字符串的长度以及角字符串 cs。让这个长度分别为 n 和 cl。
*   如果 cl>n，返回 false，因为 cs 不能大于 str。
*   否则，从字符串中找出长度为 cl 的前缀和后缀。如果前缀和后缀都与角字符串 cs 匹配，则返回 true，否则返回 false。

## C++

```
// CPP program to find if a given corner string
// is present at corners.
#include <bits/stdc++.h>
using namespace std;

bool isCornerPresent(string str, string corner)
{
    int n = str.length();
    int cl = corner.length();

    // If length of corner string is more, it
    // cannot be present at corners.
    if (n < cl)
       return false;

    // Return true if corner string is present at
    // both corners of given string.
    return (str.substr(0, cl).compare(corner) == 0 &&
            str.substr(n-cl, cl).compare(corner) == 0);
}

// Driver code
int main()
{
   string str = "geeksforgeeks";
   string corner = "geeks";
   if (isCornerPresent(str, corner))
      cout << "Yes";
   else
      cout << "No";
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if a given corner
// string is present at corners.
import java.io.*;
class GFG {

    static boolean isCornerPresent(String str,
                                   String corner)
    {
        int n = str.length();
        int cl = corner.length();

        // If length of corner string
        // is more, it cannot be present
        // at corners.
        if (n < cl)
        return false;

        // Return true if corner string
        // is present at both corners
        // of given string.
        return (str.substring(0, cl).equals(corner) &&
                str.substring(n - cl, n).equals(corner));
    }

    // Driver Code
    public static void main (String[] args)
    {
        String str = "geeksforgeeks";
        String corner = "geeks";
        if (isCornerPresent(str, corner))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by Manish_100
```

## 蟒蛇 3

```
# Python program to find
# if a given corner string
# is present at corners.

def isCornerPresent(str, corner) :

    n = len(str)
    cl = len(corner)

    # If length of corner
    # string is more, it
    # cannot be present
    # at corners.
    if (n < cl) :
        return False

    # Return true if corner
    # string is present at
    # both corners of given
    # string.
    return ((str[: cl] == corner) and
            (str[n - cl :] == corner))

# Driver Code
str = "geeksforgeeks"
corner = "geeks"
if (isCornerPresent(str, corner)) :
    print ("Yes")
else :
    print ("No")

# This code is contributed by
# Manish Shaw(manishshaw1)
```

## C#

```
// C# program to find if a
// given corner string is
// present at corners.
using System;

class GFG
{
static bool isCornerPresent(string str,
                            string corner)
{
    int n = str.Length;
    int cl = corner.Length;

    // If length of corner
    // string is more, it
    // cannot be present
    // at corners.
    if (n < cl)
        return false;

    // Return true if corner
    // string is present at
    // both corners of given
    // string.
    return (str.Substring(0,
            cl).Equals(corner) &&
            str.Substring(n - cl,
            cl).Equals(corner));
}

// Driver Code
static void Main ()
{
    string str = "geeksforgeeks";
    string corner = "geeks";
    if (isCornerPresent(str, corner))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if a
// given corner string is
// present at corners.

function isCornerPresent($str,
                         $corner)
{
    $n = strlen($str);
    $cl = strlen($corner);

    // If length of corner
    // string is more, it
    // cannot be present
    // at corners.
    if ($n < $cl)
        return false;

    // Return true if corner
    // string is present at
    // both corners of given
    // string.
    return (!strcmp(substr($str, 0,
                           $cl), $corner) &&
            !strcmp(substr($str, $n -
                           $cl, $cl), $corner));
}

// Driver Code
$str = "geeksforgeeks";
$corner = "geeks";
if (isCornerPresent($str, $corner))
    echo ("Yes");
else
    echo ("No");

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>
      // JavaScript program to find if a given corner string
      // is present at corners.
      function isCornerPresent(str, corner) {
        var n = str.length;
        var cl = corner.length;

        // If length of corner string is more, it
        // cannot be present at corners.
        if (n < cl) return false;

        // Return true if corner string is present at
        // both corners of given string.
        return (
          str.substring(0, cl).localeCompare(corner) === 0 &&
          str.substring(n - cl, n).localeCompare(corner) === 0
        );
      }

      // Driver code
      var str = "geeksforgeeks";
      var corner = "geeks";
      if (isCornerPresent(str, corner)) document.write("Yes");
      else document.write("No");
    </script>
```

**输出:**

```
Yes
```