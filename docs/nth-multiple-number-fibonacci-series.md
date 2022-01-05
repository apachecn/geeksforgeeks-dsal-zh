# 斐波那契数列中一个数的第 n 倍

> 原文:[https://www . geesforgeks . org/n-多数-斐波那契数列/](https://www.geeksforgeeks.org/nth-multiple-number-fibonacci-series/)

给定两个整数 n 和 K，找到 K 在[斐波那契数列中的第 n 倍位置。](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)

**示例:**

```
Input : k = 2, n = 3
Output : 9
3'rd multiple of 2 in Fibonacci Series is 34 
which appears at position 9.

Input  : k = 4, n = 5 
Output : 30
4'th multiple of 5 in Fibonacci Series is 832040 
which appears at position 30.
```

斐波那契数列(F) : 1，1，2，3，5，8，13，21，34，55，89，144，233，377，610，987，1597，2584，4181，6765，10946，17711，28657，46368，75025，121393，196418，317811，555
一个**简单的解决方案**是从第一个数字开始遍历斐波那契数。遍历时，记录 k 的倍数的计数。每当计数变为 n 时，返回位置。
一种**高效解决方案**基于以下有趣的特性。
在模表示下，斐波那契数列总是周期的。以下是一些例子。

```
F (mod 2) = 1,1,0,1,1,0,1,1,0,1,1,0,1,1,0,
            1,1,0,1,1,0,1,1,0,1,1,0,1,1,0 
Here 0 is repeating at every 3rd index and 
the cycle repeats at every 3rd index. 

F (mod 3) = 1,1,2,0,2,2,1,0,1,1,2,0,2,2,1,0
            ,1,1,2,0,2,2,1,0,1,1,2,0,2,2
Here 0 is repeating at every 4th index and 
the cycle repeats at every 8th index.

F (mod 4) = 1,1,2,3,1,0,1,1,2,3,1,0,1,1,2,3,
           1,0,1,1,2,3,1,0,1,1,2,3,1,0 
Here 0 is repeating at every 6th index and 
the cycle repeats at every 6th index.

F (mod 5) = 1,1,2,3,0,3,3,1,4,0,4,4,3,2,0,
            2,2,4,1,0,1,1,2,3,0,3,3,1,4,0
Here 0 is repeating at every 5th index and
the cycle repeats at every 20th index.

F (mod 6) = 1,1,2,3,5,2,1,3,4,1,5,0,5,5,4,
            3,1,4,5,3,2,5,1,0,1,1,2,3,5,2
Here 0 is repeating at every 12th index and 
the cycle repeats at every 24th index.

F (mod 7) = 1,1,2,3,5,1,6,0,6,6,5,4,2,6,1,
            0,1,1,2,3,5,1,6,0,6,6,5,4,2,6 
Here 0 is repeating at every 8th index and 
the cycle repeats at every 16th index.

F (mod 8) = 1,1,2,3,5,0,5,5,2,7,1,0,1,1,2,
            3,5,0,5,5,2,7,1,0,1,1,2,3,5,0 
Here 0 is repeating at every 6th index and 
the cycle repeats at every 12th index.

F (mod 9) = 1,1,2,3,5,8,4,3,7,1,8,0,8,8,7,
            6,4,1,5,6,2,8,1,0,1,1,2,3,5,8 
Here 0 is repeating at every 12th index and 
the cycle repeats at every 24th index.

F (mod 10) = 1,1,2,3,5,8,3,1,4,5,9,4,3,7,0,
             7,7,4,1,5,6,1,7,8,5,3,8,1,9,0.
Here 0 is repeating at every 15th index and
the cycle repeats at every 60th index.
```

**为什么斐波那契数列在模下是周期的？**
在模表示下，我们知道每个斐波那契数都会被表示为一些残数 0？F (mod m) < m。因此，对于任何给定的 F (mod m)，只有 m 个可能的值，因此 m*m =序列内连续项的 m^2 可能对。由于 m^2 是有限的，我们知道某些项对最终会重复出现。此外，由于斐波那契数列中的任何一对项决定了数列的其余部分，我们看到斐波那契数列模 m 必须在某个点重复，因此必须是周期性的。
来源:[https://www . Whitman . edu/Documents/academic/Mathematics/Clancy . pdf](https://www.whitman.edu/Documents/Academics/Mathematics/clancy.pdf)
基于以上事实，我们只需找到第一个倍数，就可以快速找到 K 的第 n 倍的位置。如果第一个倍数的位置是 I，我们返回 n*i 的位置
下面是实现:

## C++

```
// C++ program to find position
// of n'th multiple of a number
// k in Fibonacci Series
# include <bits/stdc++.h>
using namespace std;

const int MAX = 1000;

// Returns position of n'th multiple
// of k in Fibonacci Series
int findPosition(int k, int n)
{
    // Iterate through all
    // fibonacci numbers
    unsigned long long int f1 = 0,
                           f2 = 1,
                           f3;
    for (int i = 2; i <= MAX; i++)
    {
        f3 = f1 + f2;
        f1 = f2;
        f2 = f3;

        // Found first multiple of
        // k at position i
        if (f2 % k == 0)

        // n'th multiple would be at
        // position n*i using Periodic
        // property of Fibonacci numbers
        // under modulo.
        return n * i;
    }
}

// Driver Code
int main ()
{
    int n = 5, k = 4;
    cout << "Position of n'th multiple of k"
        <<" in Fibonacci Series is "
        << findPosition(k, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find position
// of n'th multiple of a number
// k in Fibonacci Series

class GFG
{
    public static int findPosition(int k,
                                   int n)
    {
        long f1 = 0, f2 = 1, f3;
        int i = 2;

        while(i != 0)
        {
            f3 = f1 + f2;
            f1 = f2;
            f2 = f3;

            if(f2 % k == 0)
            {
                return n * i;
            }

            i++;
        }
        return 0;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Multiple no.
        int n = 5;

        // Number of whose multiple
        // we are finding
        int k = 4;

        System.out.print("Position of n'th multiple" +
                     " of k in Fibonacci Series is ");

        System.out.println(findPosition(k, n));
    }
}

// This code is contributed
// by Mohit Gupta_OMG
```

## 蟒蛇 3

```
# Python Program to find position
# of n'th multiple of a number k
# in Fibonacci Series

def findPosition(k, n):
    f1 = 0
    f2 = 1
    i = 2;
    while i != 0:
        f3 = f1 + f2;
        f1 = f2;
        f2 = f3;

        if f2 % k == 0:
            return n * i

        i += 1

    return

# Multiple no.
n = 5;
# Number of whose multiple
# we are finding
k = 4;

print("Position of n'th multiple of k in"
      "Fibonacci Seires is", findPosition(k, n));

# This code is contributed
# by Mohit Gupta_OMG
```

## C#

```
// C# Program to find position of
// n'th multiple of a number k in
// Fibonacci Series
using System;

class GFG
{
    static int findPosition(int k, int n)
    {
        long f1 = 0, f2 = 1, f3;
        int i = 2;

        while(i!=0)
        {
            f3 = f1 + f2;
            f1 = f2;
            f2 = f3;

            if(f2 % k == 0)
            {
              return n * i;
            }

            i++;
        }
        return 0;
    }

    // Driver code
    public static void Main()
    {
        // Multiple no.
        int n = 5;

        // Number of whose multiple
        // we are finding
        int k = 4;

        Console.Write("Position of n'th multiple " + 
                      "of k in Fibonacci Series is ");

        // Function calling
        Console.WriteLine(findPosition(k, n));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find position
// of n'th multiple of a number
// k in Fibonacci Series
$MAX = 1000;

// Returns position of n'th multiple
// of k in Fibonacci Series
function findPosition($k, $n)
{
    global $MAX;

    // Iterate through all
    // fibonacci numbers
    $f1 = 0; $f2 = 1; $f3;
    for ($i = 2; $i <= $MAX; $i++)
    {
        $f3 = $f1 + $f2;
        $f1 = $f2;
        $f2 = $f3;

        // Found first multiple of
        // k at position i
        if ($f2 % $k == 0)

        // n'th multiple would be at
        // position n*i using Periodic
        // property of Fibonacci numbers
        // under modulo
        return $n * $i;
    }
}

// Driver Code
$n = 5; $k = 4;
echo("Position of n'th multiple of k" .
           " in Fibonacci Series is " .
                 findPosition($k, $n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
    // Javascript program to find position
// of n'th multiple of a number
// k in Fibonacci Series
let MAX = 1000;

// Returns position of n'th multiple
// of k in Fibonacci Series
function findPosition(k, n)
{

    // Iterate through all
    // fibonacci numbers
    let f1 = 0;
    let f2 = 1;
    let f3;
    for (let i = 2; i <= MAX; i++)
    {
        f3 = f1 + f2;
        f1 = f2;
        f2 = f3;

        // Found first multiple of
        // k at position i
        if (f2 % k == 0)

        // n'th multiple would be at
        // position n*i using Periodic
        // property of Fibonacci numbers
        // under modulo
        return n * i;
    }
}

// Driver Code
let n = 5;
let k = 4;
document.write("Position of n'th multiple of k" +
        " in Fibonacci Series is " +
                findPosition(k, n));

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
Position of n'th multiple of k in Fibonacci Series is 30
```

本文由**基什莱·维尔马**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息