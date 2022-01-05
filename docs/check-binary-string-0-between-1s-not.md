# 检查二进制字符串是否有介于 1 和 1 之间的 0 |设置 1(一般方法)

> 原文:[https://www . geesforgeks . org/check-binary-string-0-介于-1s-not/](https://www.geeksforgeeks.org/check-binary-string-0-between-1s-not/)

给定一个 0 和 1 的字符串，我们需要检查给定的字符串是否有效。当 1 之间不存在零时，给定字符串有效。例如，1111，00001111110，1111000 是有效字符串，但 01010011，01010，101 不是。
这里讨论了一种解决问题的方法，其他使用正则表达式的方法给出了[集合 2](https://www.geeksforgeeks.org/check-binary-string-0-1s-not-set-2-regular-expression-approach/)
**示例:**

```
Input : 100
Output : VALID

Input : 1110001
Output : NOT VALID
There is 0 between 1s

Input : 00011
Output : VALID
```

```
Algorithm:
```

1.  查找字符串中第一个出现的 1。先这样吧。
2.  查找字符串中最后出现的 1。让它持续下去。
3.  从第一个循环到最后一个循环，如果有 0，则返回 false。如果未找到 0，则返回 true。

```
Explanation:
Suppose we have a string:  01111011110000 
Now take two variables say A and B. run a loop for 0 to length of the string and point A
to the first occurrence of 1, after that again run a loop from length of the string to 0
and point second variable to the last occurrence of 1.
So A = 1 (Position of first '1' is the string) and B = 9 (last occurrence of '1').
Now run a loop from A to B and check that '0' is present between 1 or not, if "YES" than 
set flag to 1 and break the loop, else set flag  to 0.
In this case flag will set to 1 as the given string is not valid and print "NOT VALID".
```

## C++

```
// C++ program to check if a string is valid or not.
#include <bits/stdc++.h>
using namespace std;

// Function returns 1 when string is valid
// else returns 0
bool checkString(string s)
{
    int len = s.length();

    // Find first occurrence of 1 in s[]
    int first = s.size() + 1;
    for (int i = 0; i < len; i++) {
        if (s[i] == '1') {
            first = i;
            break;
        }
    }

    // Find last occurrence of 1 in s[]
    int last = 0;
    for (int i = len - 1; i >= 0; i--) {
        if (s[i] == '1') {
            last = i;
            break;
        }
    }

    // Check if there is any 0 in range
    for (int i = first; i <= last; i++)
        if (s[i] == '0')
            return false;

    return true;
}

// Driver code
int main()
{
    string s = "00011111111100000";
    checkString(s) ? cout << "VALID\n" : cout << "NOT VALID\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a string is valid or not.

class Test {
    // Method returns 1 when string is valid
    // else returns 0
    static boolean checkString(String s)
    {
        int len = s.length();

        // Find first occurrence of 1 in s[]
        int first = 0;
        for (int i = 0; i < len; i++) {
            if (s.charAt(i) == '1') {
                first = i;
                break;
            }
        }

        // Find last occurrence of 1 in s[]
        int last = 0;
        for (int i = len - 1; i >= 0; i--) {
            if (s.charAt(i) == '1') {
                last = i;
                break;
            }
        }

        // Check if there is any 0 in range
        for (int i = first; i <= last; i++)
            if (s.charAt(i) == '0')
                return false;

        return true;
    }

    // Driver method
    public static void main(String args[])
    {
        String s = "00011111111100000";
        System.out.println(checkString(s) ? "VALID" : "NOT VALID");
    }
}
```

## 计算机编程语言

```
# Python3 program to check if
# a string is valid or not.

# Function returns 1 when
# string is valid else
# returns 0
def checkString(s):

    Len = len(s)

    # Find first occurrence
    # of 1 in s[]
    first = len(s) + 1

    for i in range(Len):
        if(s[i] == '1'):
            first = i
            break

    # Find last occurrence
    # of 1 in s[]
    last = 0

    for i in range(Len - 1,
                   -1, -1):
        if(s[i] == '1'):
            last = i
            break

    # Check if there is any
    # 0 in range
    for i in range(first,
                   last + 1):
        if(s[i] == '0'):
            return False
    return True

# Driver code
s = "00011111111100000"
if(checkString(s)):
    print("VALID")
else:
    print("NOT VALID")

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program to check if a
// string is valid or not.
using System;

class GFG {

    // Method returns 1 when string is valid
    // else returns 0
    static bool checkString(String s)
    {
        int len = s.Length;

        // Find first occurrence of 1 in s[]
        int first = 0;
        for (int i = 0; i < len; i++) {
            if (s[i] == '1') {
                first = i;
                break;
            }
        }

        // Find last occurrence of 1 in s[]
        int last = 0;
        for (int i = len - 1; i >= 0; i--) {
            if (s[i] == '1') {
                last = i;
                break;
            }
        }

        // Check if there is any 0 in range
        for (int i = first; i <= last; i++)
            if (s[i] == '0')
                return false;

        return true;
    }

    // Driver method
    public static void Main()
    {
        string s = "00011111111100000";
        Console.WriteLine(checkString(s) ?
                   "VALID" : "NOT VALID");
    }
}

// This code is contributed by Sam007
```

## java 描述语言

```
<script>

    // JavaScript program to check 
    // if a string is valid or not.

    // Method returns 1 when string is valid
    // else returns 0
    function checkString(s)
    {
        let len = s.length;

        // Find first occurrence of 1 in s[]
        let first = 0;
        for (let i = 0; i < len; i++) {
            if (s[i] == '1') {
                first = i;
                break;
            }
        }

        // Find last occurrence of 1 in s[]
        let last = 0;
        for (let i = len - 1; i >= 0; i--) {
            if (s[i] == '1') {
                last = i;
                break;
            }
        }

        // Check if there is any 0 in range
        for (let i = first; i <= last; i++)
            if (s[i] == '0')
                return false;

        return true;
    }

    let s = "00011111111100000";
    document.write(checkString(s) ?
                      "VALID" : "NOT VALID");

</script>
```

**输出:**

```
VALID
```

**时间复杂度:** O(n)

本文由 [**萨赫勒拉吉普特**](https://www.linkedin.com/in/sahil-rajput-3ba2b3134/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。