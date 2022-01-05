# 自然数的组成数

> 原文:[https://www . geesforgeks . org/number-compositions-natural-number/](https://www.geeksforgeeks.org/number-compositions-natural-number/)

给定一个自然数 n，找出当考虑顺序时，n 可以表示为自然数之和的方法。两个术语顺序不同的序列定义了它们总和的不同组成。
**例:**

```
Input :  4
Output : 8
Explanation  
All 8 position composition are:
4, 1+3, 3+1, 2+2, 1+1+2, 1+2+1, 2+1+1
and 1+1+1+1

Input :  8
Output : 128
```

一个简单的解决方法是[生成所有成分](https://www.geeksforgeeks.org/print-all-combinations-of-points-that-can-compose-a-given-number/)并计数。
使用组合学的概念，可以证明当考虑顺序时，任何自然数 n 将具有 **2^(n-1)不同的组成**。

> 一种直接看到答案为什么是 2^(n-1 的方法是把 n 写成 1 的和:
> n = 1 + 1 + 1 +…+ 1 (n 次)。
> 全 1 之间有(n-1)个加号。对于每个加号，我们可以选择在该点拆分(通过放一个括号)或不拆分。因此答案是 2^(n-1).
> 例如， n = 4
> 无拆分
> 4 = 1 + 1 + 1 + 1【我们写成单个 4】
> 不同的方式拆分一次
> 4 = (1) + (1 + 1 + 1)【我们写成 1+3】
> 4 =(1+1)+(1+1)【我们写成 2+2】
> 4 =(1+1+1)+(1)【我们写成 3 + 1】
> 拆分两次的不同方式
> 4 =(1)+(1+1)+(1)[我们写成 1+2+1]
> 4 =(1+1)+(1)+(1)[我们写成 2+1+1]
> 4 =(1)+(1)+(1+1)+(1+1)[我们写成 1 + 1 + 2]
> 拆分三次的不同方式
> 4 = (1) + (1) + (1) + (1) 【我们写为 1+1+1+1】
> 因为在 n 个 1 之间有 **(n-1)** 加号，所以有 2^(n-1)的方法来选择在哪里分割总和，从而 2^(n-1)可能的总和。

## C++

```
// C++ program to find the total number of
// compositions of a natural number
#include<iostream>
using namespace std;

#define ull unsigned long long

ull countCompositions(ull n)
{
    // Return 2 raised to power (n-1)
    return (1L) << (n-1);
}

// Driver Code
int main()
{
    ull n = 4;
    cout << countCompositions(n) << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// the total number of
// compositions of a
// natural number
import java.io.*;
import java.util.*;

class GFG
{
public static int countCompositions(int n)
{
    // Return 2 raised
    // to power (n-1)
    return 1 << (n - 1);
}

// Driver Code
public static void main(String args[])
{
    int n = 4;
    System.out.print(countCompositions(n));
}
}

// This code is contributed by
// Akanksha Rai(Abby_akku)
```

## 计算机编程语言

```
# Python code to find the total number of
# compositions of a natural number
def countCompositions(n):

    # function to return the total number
    # of composition of n
    return (2**(n-1))

# Driver Code
print(countCompositions(4))
```

## C#

```
// C# program to find the
// total number of compositions
// of a natural number
using System;

class GFG
{
public static int countCompositions(int n)
{
    // Return 2 raised
    // to power (n-1)
    return 1 << (n - 1);
}

// Driver Code
public static void Main()
{
    int n = 4;
    Console.Write(countCompositions(n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// total number of compositions
// of a natural number

function countCompositions($n)
{
    // Return 2 raised
    // to power (n-1)
    return ((1) << ($n - 1));
}

// Driver Code
$n = 4;
echo countCompositions($n), "\n";

// This code is contributed
// by ajit
?>
```

## java 描述语言

```
<script>

// javascript program to find
// the total number of
// compositions of a
// natural number

function countCompositions(n)
{
    // Return 2 raised
    // to power (n-1)
    return 1 << (n - 1);
}

// Driver Code

    var n = 4;
    document.write(countCompositions(n));

// This code is contributed by 29AjayKumar
</script>
```

**输出:**

```
8
```

本文由 **Sruti Rai** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。