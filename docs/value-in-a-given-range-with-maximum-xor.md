# 给定范围内最大异或的值

> 原文:[https://www . geesforgeks . org/给定范围内的值与最大值异或/](https://www.geeksforgeeks.org/value-in-a-given-range-with-maximum-xor/)

给定正整数 n，l 和 r，我们必须找到 N ⊕ X 的最大值，其中 X ∈ [L，R]。
**例:**

> **输入:** N = 7
> L = 2
> R = 23
> **输出:** 23
> 解释:当 X = 16 时，我们得到 7 ⊕ 16 = 23，这是所有 x 的最大值∈2，23。
> **输入:**n = 10
> l = 5
> r = 12
> **输出:** 15
> 解释:当 X = 5 时，我们得到 10 ⊕ 5 = 15，这是所有 x 的最大值∈ [5，12]。

**蛮力法**:我们可以使用蛮力法来解决这个问题，方法是循环[L，R]范围内的所有整数，并与 N 进行异或运算，同时记录到目前为止遇到的最大结果。该算法的复杂度为 O(R–L)，当输入变量接近高值如 10 <sup>9</sup> 时不可行。
**高效方法**:由于两个位的异或是 1，当且仅当它们互补时，我们需要 X 与 N 有互补位才能有最大值。我们将从最大位(log <sub>2</sub> (R) <sup>第</sup>位)迭代到最低位(0 <sup>第</sup>位)。每个位可能出现以下两种情况:

1.  如果该位没有设置，即 0，我们将尝试将其设置在 X 中。如果将该位设置为 1 导致 X 超过 R，则我们不会将其设置。

2.  如果该位被设置，即 1，那么我们将尝试在 X 中将其取消设置。如果 X 的当前值已经大于或等于 L，那么我们可以安全地取消设置该位。在另一种情况下，我们将检查设置所有接下来的位是否足以保持 X >= L。如果不是，那么我们需要设置当前位。请注意，设置所有下一位相当于添加(1<< *b*)–1，其中 *b* 是当前位。

这种方法的时间复杂度为 O(log <sub>2</sub> (R))。

## C++

```
// CPP program to find the x in range [l, r]
// such that x ^ n is maximum.
#include <cmath>
#include <iostream>
using namespace std;

// Function to calculate the maximum value of
// N ^ X, where X is in the range [L, R]
int maximumXOR(int n, int l, int r)
{
    int x = 0;
    for (int i = log2(r); i >= 0; --i)
    {
        if (n & (1 << i))  // Set bit
        {
            if (x + (1 << i) - 1 < l)
                x ^= (1 << i);
        }
        else // Unset bit
        {
            if ((x ^ (1 << i)) <= r)
                x ^= (1 << i);
        }
    }
    return n ^ x;
}

// Driver Code
int main()
{
    int n = 7, l = 2, r = 23;
    cout << "The output is " << maximumXOR(n, l, r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the x in range [l, r]
// such that x ^ n is maximum.

import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{
// Function to calculate the maximum value of
// N ^ X, where X is in the range [L, R]
static int maximumXOR(int n, int l, int r)
{
    int x = 0;
    for (int i = (int)(Math.log(r)/Math.log(2)); i >= 0; --i)
    {
        if ((n & (1 << i))>0) // Set bit
        {
            if  (x + (1 << i) - 1 < l)
                x ^= (1 << i);
        }
        else // Unset bit
        {
            if ((x ^ (1 << i)) <= r)
                x ^= (1 << i);
        }
    }
    return n ^ x;
}

// Driver function
public static void main(String args[])
{
    int n = 7, l = 2, r = 23;
    System.out.println( "The output is " + maximumXOR(n, l, r));

}
}

// This code is Contributed by tufan_gupta2000
```

## 蟒蛇 3

```
# Python program to find the
# x in range [l, r] such that
# x ^ n is maximum.
import math

# Function to calculate the
# maximum value of N ^ X,
# where X is in the range [L, R]
def maximumXOR(n, l, r):
    x = 0
    for i in range(int(math.log2(r)), -1, -1):
        if (n & (1 << i)): # Set bit
            if  (x + (1 << i) - 1 < l):
                x ^= (1 << i)
        else: # Unset bit
            if (x ^ (1 << i)) <= r:
                x ^= (1 << i)
    return n ^ x

# Driver code
n = 7
l = 2
r = 23
print("The output is",
       maximumXOR(n, l, r))

# This code was contributed
# by VishalBachchas
```

## C#

```
// C# program to find the x in range
// [l, r] such that x ^ n is maximum.
using System;

class GFG
{

// Function to calculate the
// maximum value of N ^ X,
// where X is in the range [L, R]
public static int maximumXOR(int n,
                             int l, int r)
{
    int x = 0;
    for (int i = (int)(Math.Log(r) /
                       Math.Log(2)); i >= 0; --i)
    {
        if ((n & (1 << i)) > 0) // Set bit
        {
            if (x + (1 << i) - 1 < l)
            {
                x ^= (1 << i);
            }
        }
        else // Unset bit
        {
            if ((x ^ (1 << i)) <= r)
            {
                x ^= (1 << i);
            }
        }
    }
    return n ^ x;
}

// Driver Code
public static void Main(string[] args)
{
    int n = 7, l = 2, r = 23;
    Console.WriteLine("The output is " +
                   maximumXOR(n, l, r));
}
}

// This code is contributed
// by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the x in range
// [l, r] such that x ^ n is maximum.

// Function to calculate the maximum
// value of N ^ X, where X is in the
// range [L, R]
function maximumXOR($n, $l, $r)
{
    $x = 0;
    for ($i = log($r, 2); $i >= 0; --$i)
    {
        if ($n & (1 << $i))
        {  
            // Set bit
            if ($x + (1 << $i) - 1 < $l)
                $x ^= (1 << $i);
        }
        else
        {
            // Unset bit
            if (($x ^ (1 << $i)) <= $r)
                $x ^= (1 << $i);
        }
    }
    return $n ^ $x;
}

// Driver Code
$n = 7;
$l = 2;
$r = 23;
echo "The output is " ,
      maximumXOR($n, $l, $r);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to find
// the x in range [l, r]
// such that x ^ n is maximum.

// Function to calculate the maximum value of
// N ^ X, where X is in the range [L, R]
function maximumXOR(n, l, r)
{
    let x = 0;
    for (let i =
    parseInt(Math.log(r) / Math.log(2)); i >= 0; --i)
    {
        if (n & (1 << i))  // Set bit
        {
            if (x + (1 << i) - 1 < l)
                x ^= (1 << i);
        }
        else // Unset bit
        {
            if ((x ^ (1 << i)) <= r)
                x ^= (1 << i);
        }
    }
    return n ^ x;
}

// Driver Code
    let n = 7, l = 2, r = 23;
    document.write("The output is " + maximumXOR(n, l, r));

</script>
```

**Output**

```
The output is 23
```