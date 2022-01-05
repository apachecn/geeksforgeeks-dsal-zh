# 完美可逆弦

> 原文:[https://www.geeksforgeeks.org/perfect-reversible-string/](https://www.geeksforgeeks.org/perfect-reversible-string/)

给你一个字符串“str”，任务是检查“str”的所有可能的子字符串的反转是否出现在“str”中。

**示例:**

```
Input : str = "ab"
Output: "NO"
// all substrings are "a","b","ab" but reverse
// of "ab" is not present in str

Input : str = "aba"
Output: "YES"

Input : str = "abab"
Output: "NO"
// All substrings are "a", "b", "a", "b", "ab", 
// "ba", "ab", "aba", "bab", "abab" but reverse of
// "abab" is not present in str
```

这个问题的一个**简单解决方案**是生成所有可能的‘ST’子串，并检查它们的反向是否线性存在于‘str’中。
这个问题的有效解决方案**是基于这样一个事实，即当且仅当整个字符串“str”是回文时，“str”的所有子字符串的反向将存在于“str”中。我们可以通过考虑整个字符串来证明这个事实，只有当它是回文时，它的反义词才会存在。如果一个字符串是回文，那么所有子字符串的所有反转都存在。**

**下面是上述想法的实现。**

## **C++**

```
// C++ program to check if a string is perfect
// reversible or nor
#include<bits/stdc++.h>
using namespace std;

// This function basically checks if string is
// palindrome or not
bool isReversible(string str)
{
     int i = 0, j = str.length()-1;

     // iterate from left and right
     while (i < j)
     {
        if (str[i] != str[j])
            return false;
        i++;
        j--;
     }
     return true;
}

// Driver program to run the case
int main()
{
  string str="aba";
  if (isReversible(str))
      cout << "YES";
  else
      cout << "NO";
  return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to check
// if a string is perfect
// reversible or nor
import java.io.*;

class GFG
{

// This function basically
// checks if string is
// palindrome or not
static boolean isReversible(String str)
{
    int i = 0, j = str.length() - 1;

    // iterate from
    // left and right
    while (i < j)
    {
        if (str.charAt(i) != str.charAt(j))
            return false;
        i++;
        j--;
    }
    return true;
}

// Driver Code
public static void main (String[] args)
{
    String str = "aba";
    if (isReversible(str))
        System.out.print("YES");
    else
        System.out.print( "NO");
}
}

// This code is contributed
// by anuj_67.
```

## **蟒蛇 3**

```
# Python3 program to check if
# a string is perfect reversible or not

# This function basically checks
# if string is palindrome or not
def isReversible(str):
    i = 0; j = len(str) - 1;

    # iterate from left and right
    while (i < j):
        if (str[i] != str[j]):
            return False;
        i += 1;
        j -= 1;
    return True;

# Driver Code
str = "aba";
if (isReversible(str)):
    print("YES");
else:
    print("NO");

# This code is contributed by Princi Singh
```

## **C#**

```
// C# program to check if a string
// is perfect reversible or nor
using System;

class GFG
{

// This function basically checks if
// string is palindrome or not
public static bool isReversible(string str)
{
    int i = 0, j = str.Length - 1;

    // iterate from left and right
    while (i < j)
    {
        if (str[i] != str[j])
        {
            return false;
        }
        i++;
        j--;
    }
    return true;
}

// Driver Code
public static void Main(string[] args)
{
    string str = "aba";
    if (isReversible(str))
    {
        Console.Write("YES");
    }
    else
    {
        Console.Write("NO");
    }
}
}

// This code is contributed
// by anuj_67
```

## **java 描述语言**

```
<script>

// JavaScript program to check if a
// string is perfect reversible or not

// This function basically checks
// if string is palindrome or not
function isReversible(str)
{
    var i = 0,
    j = str.length - 1;

    // Iterate from left and right
    while (i < j)
    {
        if (str[i] != str[j])
            return false;

        i++;
        j--;
    }
    return true;
}

// Driver Code
var str = "aba";

if (isReversible(str))
    document.write("YES");
else
    document.write("NO");

// This code is contributed by rdtank   

</script>
```

****输出:****

```
YES
```

**本文由 [**沙莎克·米什拉(古卢)**](https://practice.geeksforgeeks.org/user-profile.php?user=Shashank%20Mishra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。**