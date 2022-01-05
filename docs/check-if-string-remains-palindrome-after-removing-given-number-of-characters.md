# 删除给定数量的字符后检查字符串是否保留回文

> 原文:[https://www . geesforgeks . org/check-if-string-return-remove-给定字符数/](https://www.geeksforgeeks.org/check-if-string-remains-palindrome-after-removing-given-number-of-characters/)

给定一个回文字符串**字符串**和一个整数 **N** 。任务是找出是否有可能从给定字符串中精确删除 **N** 个字符，从而使该字符串保持回文状态。
**举例:**

> **输入:**str =“ABBA”，N = 1
> **输出:**是
> 去掉‘b’，再串串
> “ABA”还是回文。
> **输入:** str = "aba "，N = 1
> **输出:**是

**方法:**可以观察到，总是有可能从回文串中移除任何数量的小于或等于其长度的字符，使得结果串保持回文串。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if str
// remains a palindrome after removing
// exactly N characters from it
bool isPossible(string str, int n)
{
    // Find the length of the string
    int len = str.length();

    // If it is possible
    if (len >= n)
        return true;

    return false;
}

// Driver code
int main()
{
    string str = "abccba";
    int n = 4;

    if (isPossible(str, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function that returns true if str
    // remains a palindrome after removing
    // exactly N characters from it
    static boolean isPossible(String str, int n)
    {
        // Find the length of the string
        int len = str.length();

        // If it is possible
        if (len >= n)
            return true;

        return false;
    }

    // Driver code
    public static void main (String[] args)
    {
        String str = "abccba";
        int n = 4;

        if (isPossible(str, n))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by AnkitRai01
```

## 计算机编程语言

```
# Python3 implementation of the approach

# Function that returns true if str
# remains a palindrome after removing
# exactly N characters from it
def isPossible(str, n):

    # Find the length of the string
    l = len(str)

    # If it is possible
    if (l >= n):
        return True

    return False

# Driver code
str = "abccba"
n = 4

if(isPossible(str, n)):
    print("Yes")
else:
    print("No")
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that returns true if str
    // remains a palindrome after removing
    // exactly N characters from it
    static bool isPossible(String str, int n)
    {
        // Find the length of the string
        int len = str.Length;

        // If it is possible
        if (len >= n)
            return true;

        return false;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "abccba";
        int n = 4;

        if (isPossible(str, n))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Function that returns true if str
// remains a palindrome after removing
// exactly N characters from it
function isPossible(str, n)
{
    // Find the length of the string
    var len = str.length;

    // If it is possible
    if (len >= n)
        return true;

    return false;
}

var str = "abccba";
    var n = 4;

    if (isPossible(str, n))
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(1)