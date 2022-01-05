# 找到一个给定长度的合成数范围

> 原文:[https://www . geesforgeks . org/find-range-composite-numbers-给定长度/](https://www.geeksforgeeks.org/find-range-composite-numbers-given-length/)

给定一个整数 n，我们需要找到一个正整数的范围，使得该范围内的所有数字都是复合的，并且该范围的长度是 n。在多个答案的情况下，您可以打印任何范围。一个复合数是一个正整数，它至少有一个除数而不是 1 和它自己(来源: [wiki](https://en.wikipedia.org/wiki/Composite_number) )

**示例:**

```
Input : 3
Output : [122, 124]
Explanation 122, 123, 124 are all composite numbers
```

解决办法有点棘手。由于有许多可能的答案，我们在这里讨论一个广义的解决方案。

```
Let the length of range be n and range starts 
from a then, a, a+1, a+2, ...., a+n-1 all should 
be composite. So the problem boils down to finding
such 'a'.

If we closely observe p! (where p is a positive 
integers) then we will find that, p! has factors of
2, 3, 4, ..., p-1,
Hence if we add i to p! such that 1 < i < p,
then p! + i has a factor i, so p! + i must be 
composite. So we end up finding p! + 2, p! + 3,
 .... p! + p-1 are all composite and continuous 
integers forming a range [p! + 2, p! + p-1]
The above range consists of p-2 elements.
For a range of n elements we need to consider (n+2)!

If we take a = (n+2)! + 2, 
Then, a + 1 = (n+2)! + 3
Then, a + 2 = (n+2)! + 4
...
Then, a + n-1 = (n+2)! + n+1
Hence,
a = (n+2)! + 2 = 2*3*....*(n+2) + 2
a has 2 as its divisor because (n+2)! and 2 
both divides 2
a + 1 = 2*3*....*(n+2) + 3
a + 1 has 3 as its divisor because (n+2)! 
and 3 both divides 3
...
a + n-1 = 2*3*....*(n+2) + n+1
a + n-1 has n+1 as its divisor because (n+2)! 
and n+1 both divides n+1

Therefore range will be [ (n+2)! + 2, ( (n+2)! + 2 ) + n-1]
```

上述算法的示例

```
n = 3
Then a = (n+2)! + 2
a = 5! + 2
a + 1 = 5! + 3
a + 2 = 5! + 4
Here a is divisible by 2
Here a + 1 is divisible by 3
Here a + 2 is divisible by 4
Hence a, a+1, a+2 are all composites
```

## C++

```
// C++ program to find a range of
// composite numbers of given length
#include <bits/stdc++.h>
using namespace std;

// method to find factorial
// of given number
int factorial (int n)
{
    if (n == 0)
        return 1;

    return n * factorial(n-1);
}

// to print range of length n
// having all composite integers
int printRange(int n)
{
int a = factorial(n + 2) + 2;
int b = a + n - 1;
cout << "[" << a << ", " << b << "]";
return 0;
}

// Driver method
int main()
{
    int n = 3 ;
    printRange(n);
    return 0;
}

// This code is contributed by Anshika Goyal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find a range of composite
// numbers of given length

class Test
{
    // method to find factorial of given number
    static int factorial(int n)
    {
        if (n == 0)
          return 1;

        return n*factorial(n-1);
    }

    // to print range of length n
    //  having all composite integers
    static void printRange(int n)
    {
       int  a = factorial(n + 2) + 2;
       int  b = a + n - 1;
       System.out.println("[" + a + ", " + b + "]");
    }

    // Driver method
    public static void main(String args[]) throws Exception
    {
        int n = 3 ;
        printRange(n);
    }
}
```

## 计算机编程语言

```
# Python program to find a range of composite
# numbers of given length

# function to calculate factorial
def factorial(n):
    a = 1
    for i in range(2, n + 1):
        a *= i
    return a

# to print range of length n
# having all composite integers
def printRange(n):
    a = factorial(n + 2) + 2
    b = a + n - 1
    print("["+str(a)+", "+str(b)+"]")

# driver code to test above functions
n = 3
printRange(n)
```

## C#

```
// C# program to find a range of
// composite numbers of given
// length
using System;

class GFG {

    // method to find factorial
    // of given number
    static int factorial(int n)
    {
        if (n == 0)
        return 1;

        return n*factorial(n-1);
    }

    // to print range of length n
    // having all composite integers
    static void printRange(int n)
    {
    int a = factorial(n + 2) + 2;
    int b = a + n - 1;
    Console.WriteLine("[" + a +
                   ", " + b + "]");
    }

    // Driver method
    public static void Main()
    {
        int n = 3 ;
        printRange(n);
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find a range of
// composite numbers of given length

// method to find factorial
// of given number
function factorial ( $n)
{
    if ($n == 0)
        return 1;

    return $n * factorial($n - 1);
}

// to print range of length n
// having all composite integers
function printRange($n)
{
$a = factorial($n + 2) + 2;
$b = $a + $n - 1;
echo "[" , $a , ", " , $b , "]";
return 0;
}

// Driver Code
$n = 3 ;
printRange($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to find a range of
// composite numbers of given length

// Method to find factorial
// of given number
function factorial(n)
{
    if (n == 0)
        return 1;

    return n * factorial(n - 1);
}

// To print range of length n
// having all composite integers
function printRange(n)
{
    let a = factorial(n + 2) + 2;
    let b = a + n - 1;

    document.write(`[${a}, ${b}]`);

    return 0;
}

// Driver Code
let n = 3;

printRange(n);

// This code is contributed by _saurabh_jaiswal.

</script>
```

**输出:**

```
[122, 124]
```

**以上算法分析**
时间复杂度:O(n)
辅助空间:O(1)

本文由 [**普拉蒂克·查哈尔**](https://pratik-chhajer.github.io/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。