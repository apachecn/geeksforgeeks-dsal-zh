# 无回文子串的长度为 N 的串数

> 原文:[https://www . geesforgeks . org/number-string-length-n-no-回文-子字符串/](https://www.geeksforgeeks.org/number-string-length-n-no-palindromic-sub-string/)

给定两个正整数 **N，M** 。任务是在大小为 M 的字母表集合下找到长度为 N 的字符串的数量，使得大小大于 1 的子字符串都不会被回文。
示例:

```
Input : N = 2, M = 3
Output : 6
In this case, set of alphabet are 3, say {A, B, C}
All possible string of length 2, using 3 letters are:
{AA, AB, AC, BA, BB, BC, CA, CB, CC}
Out of these {AA, BB, CC} contain palindromic substring, 
so our answer will be 
8 - 2 = 6.

Input : N = 2, M = 2
Output : 2
Out of {AA, BB, AB, BA}, only {AB, BA} contain 
non-palindromic substrings.
```

首先，观察一下，如果一个字符串没有任何长度为 2 和 3 的回文子串，那么这个字符串就不包含任何回文子串，因为所有长度较大的回文串都包含至少一个长度为 2 或 3 的回文子串，基本上在中间。
那么，以下是真的:

*   有 M 种方法可以选择字符串的第一个符号。
*   然后有(M–1)种方法来选择字符串的第二个符号。基本上不应该等于第一个。
*   然后有(M–2)种方法来选择下一个符号。基本上，它不应该与前面的符号重合，这些符号是不相等的。

知道了这一点，我们可以通过以下方式来评估答案:

*   如果 N = 1，那么答案就是 m。
*   如果 N = 2，那么答案是 M *(M–1)。
*   如果 N >= 3，则 M *(M–1)*(M–2)<sup>N-2</sup>。

以下是上述思路的实现:

## C++

```
// CPP program to count number of strings of
// size m such that no substring is palindrome.
#include <bits/stdc++.h>
using namespace std;

// Return the count of strings with
// no palindromic substring.
int numofstring(int n, int m)
{   
    if (n == 1)
        return m;

    if (n == 2)
        return m * (m - 1);

    return m * (m - 1) * pow(m - 2, n - 2);
}

// Driven Program
int main()
{   
    int n = 2, m = 3;
    cout << numofstring(n, m) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of strings of
// size m such that no substring is palindrome.
import java.io.*;

class GFG {

    // Return the count of strings with
    // no palindromic substring.
    static int numofstring(int n, int m)
    {
        if (n == 1)
            return m;

        if (n == 2)
            return m * (m - 1);

        return m * (m - 1) * (int)Math.pow(m - 2, n - 2);
    }

    // Driven Program
    public static void main (String[] args)
    {
        int n = 2, m = 3;
        System.out.println(numofstring(n, m));
    }
}

// This code is contributed by ajit.
```

## 蟒蛇 3

```
# Python3 program to count number of strings of
# size m such that no substring is palindrome

# Return the count of strings with
# no palindromic substring.
def numofstring(n, m):
    if n == 1:
        return m

    if n == 2:
        return m * (m - 1)

    return m * (m - 1) * pow(m - 2, n - 2)

# Driven Program
n = 2
m = 3
print (numofstring(n, m))

# This code is contributed
# by Shreyanshi Arun.
```

## C#

```
// C# program to count number of strings of
// size m such that no substring is palindrome.
using System;

class GFG {

    // Return the count of strings with
    // no palindromic substring.
    static int numofstring(int n, int m)
    {
        if (n == 1)
            return m;

        if (n == 2)
            return m * (m - 1);

        return m * (m - 1) * (int)Math.Pow(m - 2,
                                           n - 2);
    }

    // Driver Code
    public static void Main ()
    {
        int n = 2, m = 3;
        Console.Write(numofstring(n, m));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number
// of strings of size m such
// that no substring is palindrome.

// Return the count of strings with
// no palindromic substring.
function numofstring($n, $m)
{
    if ($n == 1)
        return $m;

    if ($n == 2)
        return $m * ($m - 1);

    return $m * ($m - 1) *
           pow($m - 2, $n - 2);
}

// Driver Code
{
    $n = 2; $m = 3;
    echo numofstring($n, $m) ;
    return 0;
}

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
// JavaScript program to count number of strings of
// size m such that no substring is palindrome.

    // Return the count of strings with
    // no palindromic substring.
    function numofstring(n, m)
    {
        if (n == 1)
            return m;

        if (n == 2)
            return m * (m - 1);

        return m * (m - 1) * Math.pow(m - 2, n - 2);
    }

// Driver Code

        let n = 2, m = 3;
        document.write(numofstring(n, m));

// This code is contributed by code_hunt.
</script>
```

**输出**T2】

```
6
```