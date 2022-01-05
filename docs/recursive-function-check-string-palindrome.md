# 检查字符串是否回文的递归函数

> 原文:[https://www . geesforgeks . org/recursive-function-check-string-回文/](https://www.geeksforgeeks.org/recursive-function-check-string-palindrome/)

给定一个字符串，编写一个递归函数，检查给定的字符串是否是回文，否则，不是回文。

**示例:**

```
Input : malayalam
Output : Yes
Reverse of malayalam is also
malayalam.

Input : max
Output : No
Reverse of max is not max. 
```

我们在这里讨论了一个迭代函数。
递归函数的思想很简单:

```
1) If there is only one character in string
   return true.
2) Else compare first and last characters
   and recur for remaining substring.
```

下面是上述想法的实现:

## C++

```
// A recursive C++ program to
// check whether a given number
// is palindrome or not
#include <bits/stdc++.h>
using namespace std;

// A recursive function that
// check a str[s..e] is
// palindrome or not.
bool isPalRec(char str[],
              int s, int e)
{

    // If there is only one character
    if (s == e)
    return true;

    // If first and last
    // characters do not match
    if (str[s] != str[e])
    return false;

    // If there are more than
    // two characters, check if
    // middle substring is also
    // palindrome or not.
    if (s < e + 1)
    return isPalRec(str, s + 1, e - 1);

    return true;
}

bool isPalindrome(char str[])
{
    int n = strlen(str);

    // An empty string is
    // considered as palindrome
    if (n == 0)
        return true;

    return isPalRec(str, 0, n - 1);
}

// Driver Code
int main()
{
    char str[] = "geeg";

    if (isPalindrome(str))
    cout << "Yes";
    else
    cout << "No";

    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// A recursive C program to
// check whether a given number
// is palindrome or not
#include <stdio.h>
#include <string.h>
#include <stdbool.h>

// A recursive function that
// check a str[s..e] is
// palindrome or not.
bool isPalRec(char str[],
              int s, int e)
{
    // If there is only one character
    if (s == e)
    return true;

    // If first and last
    // characters do not match
    if (str[s] != str[e])
    return false;

    // If there are more than
    // two characters, check if
    // middle substring is also
    // palindrome or not.
    if (s < e + 1)
    return isPalRec(str, s + 1, e - 1);

    return true;
}

bool isPalindrome(char str[])
{
int n = strlen(str);

// An empty string is
// considered as palindrome
if (n == 0)
    return true;

return isPalRec(str, 0, n - 1);
}

// Driver Code
int main()
{
    char str[] = "geeg";

    if (isPalindrome(str))
    printf("Yes");
    else
    printf("No");

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A recursive JAVA program to
// check whether a given String
// is palindrome or not
import java.io.*;

class GFG
{
    // A recursive function that
    // check a str(s..e) is
    // palindrome or not.
    static boolean isPalRec(String str,
                            int s, int e)
    {
        // If there is only one character
        if (s == e)
            return true;

        // If first and last
        // characters do not match
        if ((str.charAt(s)) != (str.charAt(e)))
            return false;

        // If there are more than
        // two characters, check if
        // middle substring is also
        // palindrome or not.
        if (s < e + 1)
            return isPalRec(str, s + 1, e - 1);

        return true;
    }

    static boolean isPalindrome(String str)
    {
        int n = str.length();

    // An empty string is
    // considered as palindrome
        if (n == 0)
            return true;

        return isPalRec(str, 0, n - 1);
    }

    // Driver Code
    public static void main(String args[])
    {
        String str = "geeg";

        if (isPalindrome(str))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed
// by Nikita Tiwari
```

## 计算机编程语言

```
# A recursive Python program
# to check whether a given
# number is palindrome or not

# A recursive function that
# check a str[s..e] is
# palindrome or not.
def isPalRec(st, s, e) :

    # If there is only one character
    if (s == e):
        return True

    # If first and last
    # characters do not match
    if (st[s] != st[e]) :
        return False

    # If there are more than
    # two characters, check if
    # middle substring is also
    # palindrome or not.
    if (s < e + 1) :
        return isPalRec(st, s + 1, e - 1);

    return True

def isPalindrome(st) :
    n = len(st)

    # An empty string is
    # considered as palindrome
    if (n == 0) :
        return True

    return isPalRec(st, 0, n - 1);

# Driver Code
st = "geeg"
if (isPalindrome(st)) :
    print "Yes"
else :
    print "No"

# This code is contributed
# by Nikita Tiwari.
```

## C#

```
// A recursive C# program to
// check whether a given number
// is palindrome or not
using System;

class GFG
{

    // A recursive function that
    // check a str(s..e)
    // is palindrome or not.
    static bool isPalRec(String str,
                         int s,
                         int e)
    {

        // If there is only one character
        if (s == e)
            return true;

        // If first and last character
        // do not match
        if ((str[s]) != (str[e]))
            return false;

        // If there are more than two
        // characters, check if middle
        // substring is also
        // palindrome or not.
        if (s < e + 1)
            return isPalRec(str, s + 1,
                            e - 1);
             return true;
    }

    static bool isPalindrome(String str)
    {
        int n = str.Length;

        // An empty string is considered
        // as palindrome
        if (n == 0)
            return true;

        return isPalRec(str, 0, n - 1);
    }

    // Driver Code
    public static void Main()
    {
        String str = "geeg";

        if (isPalindrome(str))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A recursive php program to
// check whether a given number
// is palindrome or not

// A recursive function that
// check a str[s..e] is
// palindrome or not.
function isPalRec($str, $s,$e)
{
    // If there is only one character
    if ($s == $e)
    return true;

    // If first and last
    // characters do not match
    if ($str[$s] != $str[$e])
    return false;

    // If there are more than two
    // characters, check if middle
    // substring is also palindrome or not.
    if ($s < $e + 1)
    return isPalRec($str, $s + 1, $e - 1);

    return true;
}

function isPalindrome($str)
{
$n = strlen($str);

// An empty string is
// considered as palindrome
if ($n == 0)
    return true;

return isPalRec($str, 0, $n - 1);
}

// Driver Code
{
    $str = "geeg";

    if (isPalindrome($str))
    echo("Yes");
    else
    echo("No");

    return 0;
}

// This code is contributed
// by nitin mittal.
?>
```

## java 描述语言

```
<script>
    // A recursive javascript program to
    // check whether a given String
    // is palindrome or not
    // A recursive function that
    // check a str(s..e) is
    // palindrome or not.
    function isPalRec( str , s , e) {
        // If there is only one character
        if (s == e)
            return true;

        // If first and last
        // characters do not match
        if ((str.charAt(s)) != (str.charAt(e)))
            return false;

        // If there are more than
        // two characters, check if
        // middle substring is also
        // palindrome or not.
        if (s < e + 1)
            return isPalRec(str, s + 1, e - 1);

        return true;
    }

    function isPalindrome( str) {
        var n = str.length;

        // An empty string is
        // considered as palindrome
        if (n == 0)
            return true;

        return isPalRec(str, 0, n - 1);
    }

    // Driver Code

        var str = "geeg";

        if (isPalindrome(str))
            document.write("Yes");
        else
            document.write("No");

// This code contributed by gauravrajput1
</script>
```

**输出:**

```
Yes
```

本文由**萨赫勒拉杰普特**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。