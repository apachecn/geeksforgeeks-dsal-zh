# 求数列 3、5、33、35、53 的第 N 项的程序。| Set-2

> 原文:[https://www . geesforgeks . org/program-to-find-the-n-term-of-series-3-5-33-35-53-set-2/](https://www.geeksforgeeks.org/program-to-find-the-n-th-term-of-series-3-5-33-35-53-set-2/)

给定一系列仅由数字 3 和 5 组成的数字。系列的前几个数字是:

> 3, 5, 33, 35, 53, 55, …..

**例:**

```
Input: N = 2
Output: 5

Input: N = 5
Output: 53
```

对于 **O(n)** 解，请参考[程序以找到系列 3、5、33、35、53 的第 N 项。](https://www.geeksforgeeks.org/program-to-find-n-th-term-of-series-3-5-33-35-53/)。在这篇文章中，讨论了一个基于以下数字模式的 O(log n)解决方案。数字可见一斑。

```
                 ""
              /      \
            3         5
          /   \     /   \ 
        33    35   53    55
       / \   / \   / \  / \
```

这个想法是从末尾填充所需的数字。我们知道可以观察到，如果 n 是奇数，最后一个数字是 3，如果 n 是偶数，最后一个数字是 5。填充最后一个数字后，我们移动到树中的父节点。如果 n 是奇数，则父节点对应于(n-1)/2。否则父节点对应于(n-2)/2。

## C++

```
// C++ program to find n-th number containing
// only 3 and 5.
#include <bits/stdc++.h>
using namespace std;

string findNthNo(int n)
{
    string res = "";
    while (n >= 1) {
        // If n is odd, append 3 and
        // move to parent
        if (n & 1) {
            res = res + "3";
            n = (n - 1) / 2;
        }

        // If n is even, append 5 and
        // move to parent
        else {
            res = res + "5";
            n = (n - 2) / 2;
        }
    }

    // Reverse res and return.
    reverse(res.begin(), res.end());
    return res;
}

// Driver code
int main()
{
    int n = 5;
    cout << findNthNo(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to find n-th number
// containing only 3 and 5.
public class GFG {

    static String findNthNo(int n)
    {
        String res = "";
        while (n >= 1) {

            // If n is odd, append
            // 3 and move to parent
            if ((n & 1) == 1) {
                res = res + "3";
                n = (n - 1) / 2;
            }

            // If n is even, append
            // 5 and move to parent
            else {
                res = res + "5";
                n = (n - 2) / 2;
            }
        }

        // Reverse res and return.
        StringBuilder sb = new StringBuilder(res);
        sb.reverse();
        return new String(sb);
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 5;

        System.out.print(findNthNo(n));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find
# n-th number containing
# only 3 and 5.
def reverse(s):
    if len(s) == 0:
        return s
    else:
        return reverse(s[1:]) + s[0]

def findNthNo(n):
    res = "";
    while (n >= 1):

        # If n is odd, append
        # 3 and move to parent
        if (n & 1):
            res = res + "3";
            n = (int)((n - 1) / 2);

            # If n is even, append 5
            # and move to parent
        else:
            res = res + "5";
            n = (int)((n - 2) / 2);

    # Reverse res
    # and return.
    return reverse(res);

# Driver code
n = 5;
print(findNthNo(n));
```

## C#

```
// C# program to find n-th number
// containing only 3 and 5.
using System;

class GFG
{
// function to reverse a string
public static string Reverse(string s)
{
    char[] charArray = s.ToCharArray();
    Array.Reverse(charArray);
    return new string(charArray);
}

// function to find nth number
static string findNthNo(int n)
{
    string res = "";
    while (n >= 1)
    {

        // If n is odd, append
        // 3 and move to parent
        if ((n & 1) == 1)
        {
            res = res + "3";
            n = (n - 1) / 2;
        }

        // If n is even, append
        // 5 and move to parent
        else
        {
            res = res + "5";
            n = (n - 2) / 2;
        }
    }

    string sb = Reverse(res) ;
    return sb ;
}

// Driver code
static void Main()
{
    int n = 5;

    Console.WriteLine(findNthNo(n));
}
}

// This code is contributed by ANKITRAI1
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find n-th number
// containing only 3 and 5.

function findNthNo($n)
{
    $res = "";
    while ($n >= 1)
    {
        // If n is odd, append 3
        // and move to parent
        if ($n & 1)
        {
            $res = $res + "3";
            $n = ($n - 1) / 2;
        }

        // If n is even, append 5
        // and move to parent
        else
        {
            $res = $res . "5";
            $n = ($n - 2) / 2;
        }
    }

    // Reverse res and return.
    $res = strrev($res);
    return $res;
}

// Driver code
$n = 5;
echo findNthNo($n);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript program to find n-th number
// containing only 3 and 5.

function reverseString(str) {
    return str.split("").reverse().join("");
}

function findNthNo( n) {
        let res = "";
        while (n >= 1) {

            // If n is odd, append
            // 3 and move to parent
            if ((n & 1) == 1) {
                res = res + "3";
                n = (n - 1) / 2;
            }

            // If n is even, append
            // 5 and move to parent
            else {
                res = res + "5";
                n = (n - 2) / 2;
            }
        }

        // Reverse res and return.
         sb = (res);
        sb =reverseString(sb);
        return (sb);
    }

    // Driver code

        let n = 5;

        document.write(findNthNo(n));

// This code contributed by Princi Singh

</script>
```

**Output:** 

```
53
```