# 计算没有连续 1 的二进制字符串的数量

> 原文:[https://www . geesforgeks . org/count-number-binary-strings-不带连续-1s/](https://www.geeksforgeeks.org/count-number-binary-strings-without-consecutive-1s/)

给定一个正整数 N，计算长度为 N 的所有可能的不同二进制字符串，使得没有连续的 1

示例:

```
Input:  N = 2
Output: 3
// The 3 strings are 00, 01, 10

Input: N = 3
Output: 5
// The 5 strings are 000, 001, 010, 100, 101
```

这个问题可以用动态规划来解决。设 a[i]是长度为 I 的二进制字符串的数目，这些字符串不包含任何两个连续的 1，并且以 0 结尾。同样，让 b[i]是以 1 结尾的这种字符串的数目。我们可以向以 0 结尾的字符串追加 0 或 1，但只能向以 1 结尾的字符串追加 0。这产生了递归关系:

```
a[i] = a[i - 1] + b[i - 1]
b[i] = a[i - 1] 
```

上述递归的基本情况是 a[1] = b[1] = 1。长度为 I 的字符串总数仅为 a[i] + b[i]。
以下是上述解决方案的实现。在下面的实现中，索引从 0 开始。因此 a[i]代表输入长度为 i+1 的二进制字符串的数量。类似地，b[i]代表输入长度为 i+1 的二进制字符串。

## C++

```
// C++ program to count all distinct binary strings
// without two consecutive 1's
#include <iostream>
using namespace std;

int countStrings(int n)
{
    int a[n], b[n];
    a[0] = b[0] = 1;
    for (int i = 1; i < n; i++)
    {
        a[i] = a[i-1] + b[i-1];
        b[i] = a[i-1];
    }
    return a[n-1] + b[n-1];
}

// Driver program to test above functions
int main()
{
    cout << countStrings(3) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class Subset_sum
{
    static  int countStrings(int n)
    {
        int a[] = new int [n];
        int b[] = new int [n];
        a[0] = b[0] = 1;
        for (int i = 1; i < n; i++)
        {
            a[i] = a[i-1] + b[i-1];
            b[i] = a[i-1];
        }
        return a[n-1] + b[n-1];
    }
    /* Driver program to test above function */
    public static void main (String args[])
    {
          System.out.println(countStrings(3));
    }
}/* This code is contributed by Rajat Mishra */
```

## 蟒蛇 3

```
# Python program to count
# all distinct binary strings
# without two consecutive 1's

def countStrings(n):

    a=[0 for i in range(n)]
    b=[0 for i in range(n)]
    a[0] = b[0] = 1
    for i in range(1,n):
        a[i] = a[i-1] + b[i-1]
        b[i] = a[i-1]

    return a[n-1] + b[n-1]

# Driver program to test
# above functions

print(countStrings(3))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to count all distinct binary
// strings without two consecutive 1's
using System;

class Subset_sum
{
    static int countStrings(int n)
    {
        int []a = new int [n];
        int []b = new int [n];
        a[0] = b[0] = 1;
        for (int i = 1; i < n; i++)
        {
            a[i] = a[i-1] + b[i-1];
            b[i] = a[i-1];
        }
        return a[n-1] + b[n-1];
    }

    // Driver Code
    public static void Main ()
    {
        Console.Write(countStrings(3));
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count all distinct
// binary stringswithout two
// consecutive 1's

function countStrings($n)
{
    $a[$n] = 0;
    $b[$n] = 0;
    $a[0] = $b[0] = 1;
    for ($i = 1; $i < $n; $i++)
    {
        $a[$i] = $a[$i - 1] +
                 $b[$i - 1];
        $b[$i] = $a[$i - 1];
    }
    return $a[$n - 1] +
           $b[$n - 1];
}

    // Driver Code
    echo countStrings(3) ;

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>

// JavaScript program to count all
// distinct binary strings
// without two consecutive 1's
function countStrings(n)
{
    let a = [];
    let b = [];
    a[0] = b[0] = 1;

    for(let i = 1; i < n; i++)
    {
        a[i] = a[i - 1] + b[i - 1];
        b[i] = a[i - 1];
    }
    return a[n - 1] + b[n - 1];
}

// Driver code
document.write(countStrings(3));

// This code is contributed by rohan07

</script>
```

**输出:**

```
5
```

**时间复杂度:** O(N)

**辅助空间:** O(N)
**来源:**
[courses . csail . MIT . edu/6.006/old quicks/sols/Q2-f 2009-sol . pdf](http://courses.csail.mit.edu/6.006/oldquizzes/solutions/q2-f2009-sol.pdf)
如果我们仔细看一下图案，可以观察到计数实际上是(N+2)’第 N 个斐波那契数为 n > = 1。[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)是 0，1，1，2，3，5，8，13，21，34，55，89，141，…。

```
n = 1, count = 2  = fib(3)
n = 2, count = 3  = fib(4)
n = 3, count = 5  = fib(5)
n = 4, count = 8  = fib(6)
n = 5, count = 13 = fib(7)
................
```

因此，我们也可以使用方法 5来计算 O(Log n)时间中的字符串。

**相关帖子:**
[二进制表示中没有连续 1 的 1 到 n 位数字。](https://www.geeksforgeeks.org/1-to-n-bit-numbers-with-no-consecutive-1s-in-binary-representation/)
本文由 **Rahul Jain** 供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息