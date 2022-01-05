# 根据给定条件

检查两个字符串是否相等

> 原文:[https://www . geeksforgeeks . org/check-two-string-根据给定条件是否等效/](https://www.geeksforgeeks.org/check-whether-two-strings-are-equivalent-or-not-according-to-given-condition/)

给定两根同等大小的弦 **A** 和 **B** 。两个字符串相等以下任一条件成立:
1)它们都相等。或者，
2)如果我们把字符串 A 分成两个大小相同的连续子字符串 A <sub>1</sub> 和 A <sub>2</sub> ，把字符串 B 分成两个大小相同的连续子字符串 B <sub>1</sub> 和 B <sub>2</sub> ，那么下面的一个应该是正确的:

*   A <sub>1</sub> 递归等价于 B <sub>1</sub> ，A <sub>2</sub> 递归等价于 B <sub>2</sub>
*   A <sub>1</sub> 递归等价于 B <sub>2</sub> ，A <sub>2</sub> 递归等价于 B <sub>1</sub>

检查给定的字符串是否等价。打印是或否
**示例:**

> **输入:**A =“aaba”，B =“abaa”
> **输出:** YES
> **说明:**由于条件 1 不成立，我们可以把字符串 A 分成“aaba”=“aa”+“ba”，把字符串 B 分成“abaa”=“ab”+“aa”。这里，2 <sup>nd</sup> 子条件成立，其中 A <sub>1</sub> 等于 B <sub>2</sub> ，A <sub>2</sub> 递归等于 B <sub>1</sub>
> **输入:**A =“AABB”，B =“abab”
> **输出:** NO

**天真解决方案:**一个简单的解决方案是考虑所有可能的场景。首先检查两个字符串是否相等返回“是”，否则将字符串分开，检查是否**A<sub>1</sub>= B<sub>1</sub>T7】和**A<sub>2</sub>= B<sub>2</sub>T13】或**A<sub>1</sub>= B<sub>2</sub>T19】和**A<sub>2</sub>= B<sub>1</sub>T25 这个解决方案的复杂性是 O(n <sup>2</sup> ，其中 n 是字符串的大小。
**高效解决方案:**我们来定义一下对字符串 s 的如下操作，我们可以把它分成两半，如果愿意的话可以互换。此外，我们可以递归地将这个操作应用于它的两个部分。通过仔细观察，我们可以看到，如果在对某个字符串 A 应用操作之后，我们可以得到 B，那么在对 B 应用操作之后，我们可以得到 A，并且对于给定的两个字符串，我们可以递归地找到从它们可以得到的字典序最少的字符串。那些得到的字符串如果相等，答案是肯定的，否则是否定的。例如，“aaba”的最小字典序字符串是“aaab”。“abaa”的最小词典字符串也是“aaab”。因此这两者是等价的。
以下是上述办法的实施情况。******** 

## C++

```
// CPP Program to find whether two strings
// are equivalent or not according to given
// condition
#include <bits/stdc++.h>
using namespace std;

// This function returns the least lexicogr
// aphical string obtained from its two halves
string leastLexiString(string s)
{
    // Base Case - If string size is 1
    if (s.size() & 1)
        return s;

    // Divide the string into its two halves
    string x = leastLexiString(s.substr(0,
                                        s.size() / 2));
    string y = leastLexiString(s.substr(s.size() / 2));

    // Form least lexicographical string
    return min(x + y, y + x);
}

bool areEquivalent(string a, string b)
{
  return (leastLexiString(a) == leastLexiString(b));
}

// Driver Code
int main()
{
    string a = "aaba";
    string b = "abaa";
    if (areEquivalent(a, b))
        cout << "YES" << endl;
    else
        cout << "NO" << endl;

    a = "aabb";
    b = "abab";
    if (areEquivalent(a, b))
        cout << "YES" << endl;
    else
        cout << "NO" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find whether two strings
// are equivalent or not according to given
// condition
class GfG
{

// This function returns the least lexicogr
// aphical String obtained from its two halves
static String leastLexiString(String s)
{
    // Base Case - If String size is 1
    if (s.length() == 1)
        return s;

    // Divide the String into its two halves
    String x = leastLexiString(s.substring(0,
                                        s.length() / 2));
    String y = leastLexiString(s.substring(s.length() / 2));

    // Form least lexicographical String
    return String.valueOf((x + y).compareTo(y + x));
}

static boolean areEquivalent(String a, String b)
{
    return !(leastLexiString(a).equals(leastLexiString(b)));
}

// Driver Code
public static void main(String[] args)
{
    String a = "aaba";
    String b = "abaa";
    if (areEquivalent(a, b))
        System.out.println("Yes");
    else
        System.out.println("No");

    a = "aabb";
    b = "abab";
    if (areEquivalent(a, b))
        System.out.println("Yes");
    else
        System.out.println("No");
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python 3 Program to find whether two strings
# are equivalent or not according to given
# condition

# This function returns the least lexicogr
# aphical string obtained from its two halves
def leastLexiString(s):

    # Base Case - If string size is 1
    if (len(s) & 1 != 0):
        return s

    # Divide the string into its two halves
    x = leastLexiString(s[0:int(len(s) / 2)])
    y = leastLexiString(s[int(len(s) / 2):len(s)])

    # Form least lexicographical string
    return min(x + y, y + x)

def areEquivalent(a,b):
    return (leastLexiString(a) == leastLexiString(b))

# Driver Code
if __name__ == '__main__':
    a = "aaba"
    b = "abaa"
    if (areEquivalent(a, b)):
        print("YES")
    else:
        print("NO")

    a = "aabb"
    b = "abab"
    if (areEquivalent(a, b)):
        print("YES")
    else:
        print("NO")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# Program to find whether two strings
// are equivalent or not according to given
// condition
using System;
class GFG
{

// This function returns the least lexicogr-
// aphical String obtained from its two halves
static String leastLexiString(String s)
{
    // Base Case - If String size is 1
    if (s.Length == 1)
        return s;

    // Divide the String into its two halves
    String x = leastLexiString(s.Substring(0,
                               s.Length / 2));
    String y = leastLexiString(s.Substring(
                               s.Length / 2));

    // Form least lexicographical String
    return ((x + y).CompareTo(y + x).ToString());
}

static Boolean areEquivalent(String a, String b)
{
    return !(leastLexiString(a).Equals(
             leastLexiString(b)));
}

// Driver Code
public static void Main(String[] args)
{
    String a = "aaba";
    String b = "abaa";
    if (areEquivalent(a, b))
        Console.WriteLine("YES");
    else
        Console.WriteLine("NO");

    a = "aabb";
    b = "abab";
    if (areEquivalent(a, b))
        Console.WriteLine("YES");
    else
        Console.WriteLine("NO");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    // Javascript Program to find whether two strings
    // are equivalent or not according to given
    // condition

    // This function returns the least lexicogr-
    // aphical String obtained from its two halves
    function leastLexiString(s)
    {
        // Base Case - If String size is 1
        if (s.length == 1)
            return s;

        // Divide the String into its two halves
        let x = leastLexiString(s.substring(0,
                                   s.length / 2));
        let y = leastLexiString(s.substring(
                                   s.length / 2));

        // Form least lexicographical String
        if((x + y) < (y + x))
        {
            return (x+y);
        }
        else{
            return (y+x);
        }
    }

    function areEquivalent(a, b)
    {
        return (leastLexiString(a) == leastLexiString(b));
    }

    let a = "aaba";
    let b = "abaa";
    if (areEquivalent(a, b))
        document.write("YES" + "</br>");
    else
        document.write("NO" + "</br>");

    a = "aabb";
    b = "abab";
    if (areEquivalent(a, b))
        document.write("YES" + "</br>");
    else
        document.write("NO" + "</br>");

// This code is contributed by decode2207.
</script>
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find whether two strings
// are equivalent or not according to given
// condition

// This function returns the least lexicogr
// aphical string obtained from its two halves
function leastLexiString($s)
{
    // Base Case - If string size is 1
    if (strlen($s) & 1)
        return $s;

    // Divide the string into its two halves
    $x = leastLexiString(substr($s, 0,floor(strlen($s) / 2)));
    $y = leastLexiString(substr($s,floor(strlen($s) / 2),strlen($s)));

    // Form least lexicographical string
    return min($x.$y, $y.$x);
}

function areEquivalent($a, $b)
{
    return (leastLexiString($a) == leastLexiString($b));
}

    // Driver Code
    $a = "aaba";
    $b = "abaa";
    if (areEquivalent($a, $b))
        echo "YES", "\n";
    else
        echo "NO", "\n";

    $a = "aabb";
    $b = "abab";
    if (areEquivalent($a, $b))
        echo "YES", "\n";
    else
        echo "NO","\n";

// This code is contributed by Ryuga
?>
```

**Output:** 

```
YES
NO
```

**时间复杂度:** O(N*logN)，其中 N 是字符串的大小。
**辅助空间:** O(logN)