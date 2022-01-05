# 字符串中使相邻字符不相等的最少替换次数

> 原文:[https://www . geesforgeks . org/最小替换字符串使相邻字符不相等/](https://www.geeksforgeeks.org/minimum-replacements-in-a-string-to-make-adjacent-characters-unequal/)

给定大小为 **N** 的小写字符串**字符串**。在一次操作中，任何字符都可以变成其他字符。任务是找到最小的操作数，使得相邻的两个字符不相等。
**例:**

> **输入:** Str = "caaab"
> **输出:** 1
> **解释:**
> 把第二个 **a** 改成任何其他字符，我们改成 **b** 。所以弦变成了“卡巴”。并且没有两个相邻的字符相等。所以最小运算次数是 1。
> **输入:** Str = "xxxxxxx"
> **输出:** 3
> **解释:**
> 将索引 1、3 和 5 处的‘x’分别替换为‘a’、‘b’和‘c’。

**方法:**思路类似于实现[滑动窗口](https://www.geeksforgeeks.org/window-sliding-technique/)技术。在这种情况下，我们需要找到所有字符都相同的非重叠子字符串。那么最小运算将是每个子串长度一半的地板的总和。

1.  没有必要直接改变一个角色。相反，考虑从只有一个字符的任何索引开始的所有子字符串。
2.  现在考虑长度为 **l** 的任何子串，使得该子串的所有字符都相等，然后将该子串的 **floor ( l / 2)** 字符更改为其他字符。
3.  所以只要从任意字符 **ch** 开始迭代字符串的所有字符，找出子串的最大长度，这样子串中的所有字符都等于字符 **ch** 。
4.  **求这个子串的长度 l，将 floor ( l / 2)加到 ans** 上。
5.  之后从紧挨着上述子字符串末尾的字符开始。

## C++14

```
// C++ program to find minimum
// replacements in a string to
// make adjacent characters unequal

#include <bits/stdc++.h>
using namespace std;

// Function which counts the minimum
// number of required operations
void count_minimum(string s)
{
    // n stores the length of the string s
    int n = s.length();

    // ans will store the required ans
    int ans = 0;

    // i is the current index in the string
    int i = 0;

    while (i < n) {

        int j = i;

        // Move j until characters s[i] & s[j]
        // are equal or the end of the
        // string is reached
        while (s[j] == s[i] && j < n) {
            j++;
        }

        // diff stores the length of the
        // substring such that all the
        // characters are equal in it
        int diff = j - i;

        // We need atleast diff/2 operations
        // for this substring
        ans += diff / 2;
        i = j;
    }

    cout << ans << endl;
}

// Driver code
int main()
{
    string str = "caaab";
    count_minimum(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum
// replacements in a string to
// make adjacent characters unequal
import java.util.*;

class GFG{

// Function which counts the minimum
// number of required operations
static void count_minimum(String s)
{

    // n stores the length of the string s
    int n = s.length();

    // ans will store the required ans
    int ans = 0;

    // i is the current index in the string
    int i = 0;

    while (i < n)
    {
        int j = i;

        // Move j until characters s[i] & s[j]
        // are equal or the end of the
        // string is reached
        while (j < n && s.charAt(j) ==
                        s.charAt(i))
        {
            j++;
        }

        // diff stores the length of the
        // substring such that all the
        // characters are equal in it
        int diff = j - i;

        // We need atleast diff/2 operations
        // for this substring
        ans += diff / 2;
        i = j;
    }
    System.out.println(ans);
}

// Driver code
public static void main(String[] args)
{
    String str = "caaab";

    count_minimum(str);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to find minimum
# replacements in a string to
# make adjacent characters unequal

# Function which counts the minimum
# number of required operations
def count_minimum(s):

    # n stores the length of the string s
    n = len(s)

    # ans will store the required ans
    ans = 0

    # i is the current index in the string
    i = 0

    while i < n:
        j = i

        # Move j until characters s[i] & s[j]
        # are equal or the end of the
        # string is reached
        while j < n and (s[j] == s[i]):
            j += 1

        # diff stores the length of the
        # substring such that all the
        # characters are equal in it
        diff = j - i

        # We need atleast diff/2 operations
        # for this substring
        ans += diff // 2
        i = j

    print(ans)

# Driver code
if __name__=="__main__":

    str = "caaab"
    count_minimum(str)

# This code is contributed by rutvik_56
```

## C#

```
// C# program to find minimum
// replacements in a string to
// make adjacent characters unequal
using System;

class GFG{

// Function which counts the minimum
// number of required operations
static void count_minimum(string s)
{

    // n stores the length of the string s
    int n = s.Length;

    // ans will store the required ans
    int ans = 0;

    // i is the current index in the string
    int i = 0;

    while (i < n)
    {
        int j = i;

        // Move j until characters s[i] & s[j]
        // are equal or the end of the
        // string is reached
        while (j < n && s[j] == s[i])
        {
            j++;
        }

        // diff stores the length of the
        // substring such that all the
        // characters are equal in it
        int diff = j - i;

        // We need atleast diff/2 operations
        // for this substring
        ans += diff / 2;
        i = j;
    }
    Console.WriteLine(ans);
}

// Driver code
static void Main()
{
    string str = "caaab";

    count_minimum(str);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
      // JavaScript program to find minimum
      // replacements in a string to
      // make adjacent characters unequal

      // Function which counts the minimum
      // number of required operations
      function count_minimum(s) {
        // n stores the length of the string s
        var n = s.length;

        // ans will store the required ans
        var ans = 0;

        // i is the current index in the string
        var i = 0;

        while (i < n) {
          var j = i;

          // Move j until characters s[i] & s[j]
          // are equal or the end of the
          // string is reached
          while (s[j] === s[i] && j < n) {
            j++;
          }

          // diff stores the length of the
          // substring such that all the
          // characters are equal in it
          var diff = j - i;

          // We need atleast diff/2 operations
          // for this substring
          ans += parseInt(diff / 2);
          i = j;
        }

        document.write(ans + "<br>");
      }

      // Driver code
      var str = "caaab";
      count_minimum(str);
    </script>
```

**Output**

```
1
```

***时间复杂度:** O (N)*

***辅助空间:** O (1)*