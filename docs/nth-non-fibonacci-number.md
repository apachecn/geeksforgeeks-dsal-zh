# 非斐波那契数

> 原文:[https://www.geeksforgeeks.org/nth-non-fibonacci-number/](https://www.geeksforgeeks.org/nth-non-fibonacci-number/)

给定正整数 n，任务是打印第 n 个非[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。斐波那契数列定义为:

```
Fib(0) = 0
Fib(1) = 1
for n >1, Fib(n) = Fib(n-1) + Fib(n-2)
```

前几个斐波那契数是 0，1，1，2，3，5，8，13，21，34，55，89，141，…..
**例:**

```
Input : n = 2
Output : 6

Input : n = 5
Output : 10
```

一个**天真的解决方案**是找到找到的斐波那契数，然后打印前 n 个没有出现在找到的斐波那契数中的数。
一个**更好的解决方案**是使用斐波那契数的公式，并不断增加两个连续的斐波那契数之间的差距。差距和的值是迄今为止看到的非斐波那契数的计数。下面是上述想法的实现。

## C++

```
// C++ program to find n'th Fibonacci number
#include<bits/stdc++.h>
using namespace std;

// Returns n'th Non-Fibonacci number
int nonFibonacci(int n)
{
    // curr is to keep track of current fibonacci
    // number, prev is previous, prevPrev is
    // previous of previous.
    int prevPrev=1, prev=2, curr=3;

    // While count of non-fibonacci numbers
    // doesn't become negative or zero
    while (n > 0)
    {
        // Simple Fibonacci number logic
        prevPrev = prev;
        prev = curr;
        curr = prevPrev + prev;

        // (curr - prev - 1) is count of
        // non-Fibonacci numbers between curr
        // and prev.
        n = n - (curr - prev - 1);
    }

    // n might be negative now. Make sure it
    // becomes positive by removing last added
    // gap.
    n = n + (curr - prev - 1);

    // n must be now positive and less than or equal
    // to gap between current and previous, i.e.,
    // (curr - prev - 1);

    // Now add the positive n to previous Fibonacci
    // number to find the n'th non-fibonacci.
    return prev + n;
}

// Driver code
int main()
{
   cout << nonFibonacci(5);
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// n'th Fibonacci number
import java.io.*;

class GFG
{
    // Returns n'th Non-
    // Fibonacci number
    static int nonFibonacci(int n)
    {

    // curr is to keep track of
    // current fibonacci number,
    // prev is previous, prevPrev
    // is previous of previous.
    int prevPrev = 1, prev = 2, curr = 3;

    // While count of non-fibonacci
    // numbers doesn't become
    // negative or zero
    while (n > 0)
    {
        // Simple Fibonacci number logic
        prevPrev = prev;
        prev = curr;
        curr = prevPrev + prev;

        // (curr - prev - 1) is count
        // of non-Fibonacci numbers
        // between curr and prev.
        n = n - (curr - prev - 1);
    }

    // n might be negative now. Make
    // sure it becomes positive by
    // removing last added gap.
    n = n + (curr - prev - 1);

    // n must be now positive and less
    // than or equal to gap between
    // current and previous, i.e.,
    // (curr - prev - 1);

    // Now add the positive n to
    // previous Fibonacci number
    // to find the n'th non-fibonacci.
    return prev + n;
    }

    // Driver Code
    public static void main (String args[])
    {
        System.out.println(nonFibonacci(5));
    }
}

// This code is contributed by aj_36
```

## 计算机编程语言

```
# Python program to find n'th
# Fibonacci number

# Returns n'th Non-Fibonacci
# number
def nonFibonacci(n):

    # curr is to keep track of
    # current fibonacci number,
    # prev is previous, prevPrev
    # is previous of previous.
    prevPrev = 1
    prev = 2
    curr = 3

    # While count of non-fibonacci
    # numbers doesn't become
    # negative or zero
    while n > 0:
        prevPrev = prev
        prev = curr
        curr = prevPrev + prev

        # (curr - prev - 1) is
        # count of non-Fibonacci
        # numbers between curr
        # and prev.
        n = n - (curr - prev - 1)

    # n might be negative now.
    # Make sure it becomes positive
    # by removing last added gap.
    n = n + (curr - prev - 1)

    # n must be now positive and
    # less than or equal to gap
    # between current and previous,
    # i.e., (curr - prev - 1)

    # Now add the positive n to
    # previous Fibonacci number to
    # find the n'th non-fibonacci.
    return prev + n

# Driver code
print(nonFibonacci(5))

# This code is contributed by anuj_67.
```

## C#

```
// C# program to find
// n'th Fibonacci number
using System;

class GFG
{
    // Returns n'th Non-
    // Fibonacci number
    static int nonFibonacci (int n)
    {

    // curr is to keep track of
    // current fibonacci number,
    // prev is previous, prevPrev
    // is previous of previous.
    int prevPrev = 1, prev = 2, curr = 3;

    // While count of non-fibonacci
    // numbers doesn't become
    // negative or zero
    while (n > 0)
    {
        // Simple Fibonacci number logic
        prevPrev = prev;
        prev = curr;
        curr = prevPrev + prev;

        // (curr - prev - 1) is count
        // of non-Fibonacci numbers
        // between curr and prev.
        n = n - (curr - prev - 1);
    }

    // n might be negative now. Make
    // sure it becomes positive by
    // removing last added gap.
    n = n + (curr - prev - 1);

    // n must be now positive and less
    // than or equal to gap between 
    // current and previous, i.e.,
    // (curr - prev - 1);

    // Now add the positive n to
    // previous Fibonacci number
    // to find the n'th non-fibonacci.
    return prev + n;
    }

    // Driver Code
    public static void Main ()
    {
    Console.WriteLine (nonFibonacci(5));
    }
}

//This code is contributed by aj_36
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// n'th Fibonacci number

// Returns n'th Non-
// Fibonacci number
function nonFibonacci($n)
{
    // curr is to keep track of
    // current fibonacci number,
    // prev is previous, prevPrev
    // is previous of previous.
    $prevPrev = 1;
    $prev = 2;
    $curr = 3;

    // While count of non-fibonacci
    // numbers doesn't become
    // negative or zero
    while ($n > 0)
    {
        // Simple Fibonacci
        // number logic
        $prevPrev = $prev;
        $prev = $curr;
        $curr = $prevPrev + $prev;

        // (curr - prev - 1) is count
        // of non-Fibonacci numbers
        // between curr and prev.
        $n = $n - ($curr - $prev - 1);
    }

    // n might be negative now. Make
    // sure it becomes positive by
    // removing last added gap.
    $n = $n + ($curr - $prev - 1);

    // n must be now positive and
    // less than or equal to gap
    // between current and previous, 
    // i.e., (curr - prev - 1);

    // Now add the positive n to
    // previous Fibonacci number
    // to find the n'th non-fibonacci.
    return $prev + $n;
}

// Driver code
echo nonFibonacci(5);

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>

// Javascript program to find n'th Fibonacci number

// Returns n'th Non-Fibonacci number
function nonFibonacci(n)
{
    // curr is to keep track of current fibonacci
    // number, prev is previous, prevPrev is
    // previous of previous.
    let prevPrev=1, prev=2, curr=3;

    // While count of non-fibonacci numbers
    // doesn't become negative or zero
    while (n > 0)
    {
        // Simple Fibonacci number logic
        prevPrev = prev;
        prev = curr;
        curr = prevPrev + prev;

        // (curr - prev - 1) is count of
        // non-Fibonacci numbers between curr
        // and prev.
        n = n - (curr - prev - 1);
    }

    // n might be negative now. Make sure it
    // becomes positive by removing last added
    // gap.
    n = n + (curr - prev - 1);

    // n must be now positive and less than or equal
    // to gap between current and previous, i.e.,
    // (curr - prev - 1);

    // Now add the positive n to previous Fibonacci
    // number to find the n'th non-fibonacci.
    return prev + n;
}

// Driver code

    document.write(nonFibonacci(5));

// This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
10
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)
以上问题及解决方法由**赫蒙萨卡尔**贡献。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。