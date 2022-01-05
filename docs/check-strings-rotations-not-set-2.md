# 检查琴弦是否相互旋转|设置 2

> 原文:[https://www . geesforgeks . org/check-strings-rotations-not-set-2/](https://www.geeksforgeeks.org/check-strings-rotations-not-set-2/)

给定两个字符串 s1 和 s2，检查 s2 是否是 s1 的旋转。
**例:**

```
Input : ABACD, CDABA
Output : True

Input : GEEKS, EKSGE
Output : True
```

我们在早期的帖子中讨论了一种方法，它将子串匹配作为一种模式来处理。在这篇文章中，我们将使用 **KMP 算法的 lps** (最长的适当前缀，也是后缀)构造，这将有助于找到字符串 b 的前缀和字符串 a 的后缀的最长匹配。由此我们将知道**旋转点**，从这个点匹配字符。如果所有的字符都匹配，那么它是一个旋转，否则不是。
以下是上述方法的基本实现。

## C++

```
// C++ program to check if
// two strings are rotations
// of each other
#include<bits/stdc++.h>
using namespace std;
bool isRotation(string a,
                string b)
{
  int n = a.length();
  int m = b.length();
  if (n != m)
    return false;

  // create lps[] that
  // will hold the longest
  // prefix suffix values
  // for pattern
  int lps[n];

  // length of the previous
  // longest prefix suffix
  int len = 0;
  int i = 1;

  // lps[0] is always 0
  lps[0] = 0;

  // the loop calculates
  // lps[i] for i = 1 to n-1
  while (i < n)
  {
    if (a[i] == b[len])
    {
      lps[i] = ++len;
      ++i;
    }
    else
    {
      if (len == 0)
      {
        lps[i] = 0;
        ++i;
      }
      else
      {
        len = lps[len - 1];
      }
    }
  }

  i = 0;

  // Match from that rotating
  // point
  for (int k = lps[n - 1];
           k < m; ++k)
  {
    if (b[k] != a[i++])
      return false;
  }
  return true;
}

// Driver code
int main()
{
  string s1 = "ABACD";
  string s2 = "CDABA";
  cout << (isRotation(s1, s2) ?
           "1" : "0");
}

// This code is contributed by Chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if two strings are rotations
// of each other.
import java.util.*;
import java.lang.*;
import java.io.*;
class stringMatching {
    public static boolean isRotation(String a, String b)
    {
        int n = a.length();
        int m = b.length();
        if (n != m)
            return false;

        // create lps[] that will hold the longest
        // prefix suffix values for pattern
        int lps[] = new int[n];

        // length of the previous longest prefix suffix
        int len = 0;
        int i = 1;
        lps[0] = 0; // lps[0] is always 0

        // the loop calculates lps[i] for i = 1 to n-1
        while (i < n) {
            if (a.charAt(i) == b.charAt(len)) {
                lps[i] = ++len;
                ++i;
            }
            else {
                if (len == 0) {
                    lps[i] = 0;
                    ++i;
                }
                else {
                    len = lps[len - 1];
                }
            }
        }

        i = 0;

        // match from that rotating point
        for (int k = lps[n - 1]; k < m; ++k) {
            if (b.charAt(k) != a.charAt(i++))
                return false;
        }
        return true;
    }

    // Driver code
    public static void main(String[] args)
    {
        String s1 = "ABACD";
        String s2 = "CDABA";

        System.out.println(isRotation(s1, s2) ? "1" : "0");
    }
}
```

## 蟒蛇 3

```
# Python program to check if
# two strings are rotations
# of each other
def isRotation(a: str, b: str) -> bool:
    n = len(a)
    m = len(b)
    if (n != m):
        return False

    # create lps[] that
    # will hold the longest
    # prefix suffix values
    # for pattern
    lps = [0 for _ in range(n)]

    # length of the previous
    # longest prefix suffix
    length = 0
    i = 1

    # lps[0] is always 0
    lps[0] = 0

    # the loop calculates
    # lps[i] for i = 1 to n-1
    while (i < n):
        if (a[i] == b[length]):
            length += 1
            lps[i] = length
            i += 1
        else:
            if (length == 0):
                lps[i] = 0
                i += 1
            else:
                length = lps[length - 1]
    i = 0

    # Match from that rotating
    # point
    for k in range(lps[n - 1], m):
        if (b[k] != a[i]):
            return False
        i += 1
    return True

# Driver code
if __name__ == "__main__":

    s1 = "ABACD"
    s2 = "CDABA"
    print("1" if isRotation(s1, s2) else "0")

# This code is contributed by sanjeev2552
```

## C#

```
// C# program to check if
// two strings are rotations
// of each other.
using System;

class GFG
{
public static bool isRotation(string a,
                              string b)
{
    int n = a.Length;
    int m = b.Length;
    if (n != m)
        return false;

    // create lps[] that will
    // hold the longest prefix
    // suffix values for pattern
    int []lps = new int[n];

    // length of the previous
    // longest prefix suffix
    int len = 0;
    int i = 1;

    // lps[0] is always 0
    lps[0] = 0;

    // the loop calculates
    // lps[i] for i = 1 to n-1
    while (i < n)
    {
        if (a[i] == b[len])
        {
            lps[i] = ++len;
            ++i;
        }
        else
        {
            if (len == 0)
            {
                lps[i] = 0;
                ++i;
            }
            else
            {
                len = lps[len - 1];
            }
        }
    }

    i = 0;

    // match from that
    // rotating point
    for (int k = lps[n - 1]; k < m; ++k)
    {
        if (b[k] != a[i++])
            return false;
    }
    return true;
}

// Driver code
public static void Main()
{
    string s1 = "ABACD";
    string s2 = "CDABA";

    Console.WriteLine(isRotation(s1, s2) ?
                                     "1" : "0");
}
}

// This code is contributed
// by anuj_67.
```

## java 描述语言

```
<script>

// javascript program to check if two strings are rotations
// of each other.
function isRotation(a, b)
{
    var n = a.length;
    var m = b.length;
    if (n != m)
        return false;

    // create lps that will hold the longest
    // prefix suffix values for pattern
    var lps = Array.from({length: n}, (_, i) => 0);

    // length of the previous longest prefix suffix
    var len = 0;
    var i = 1;
    lps[0] = 0; // lps[0] is always 0

    // the loop calculates lps[i] for i = 1 to n-1
    while (i < n) {
        if (a.charAt(i) == b.charAt(len)) {
            lps[i] = ++len;
            ++i;
        }
        else {
            if (len == 0) {
                lps[i] = 0;
                ++i;
            }
            else {
                len = lps[len - 1];
            }
        }
    }

    i = 0;

    // match from that rotating point
    for (k = lps[n - 1]; k < m; ++k) {
        if (b.charAt(k) != a.charAt(i++))
            return false;
    }
    return true;
}

// Driver code
var s1 = "ABACD";
var s2 = "CDABA";
document.write(isRotation(s1, s2) ? "1" : "0");

// This code is contributed by shikhasingrajput.
</script>
```

**输出:**

```
1
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)