# 在等于该数的模 N 下，与具有乘法逆的 N 最近的较小数

> 原文:[https://www . geeksforgeeks . org/最近的较小数对 n 有乘法-求逆-模 n-等于那个数/](https://www.geeksforgeeks.org/nearest-smaller-number-to-n-having-multiplicative-inverse-under-modulo-n-equal-to-that-number/)

给定一个[素数](https://www.geeksforgeeks.org/prime-numbers/) **N** ，任务是找到比 **N** 最近的更小的数，使得[模 N](https://www.geeksforgeeks.org/multiplicative-inverse-under-modulo-m/) 下的数的模乘逆等于数本身。

**示例:**

> **输入:** N = 7
> **输出:** 6
> **说明:**
> 从 1 到小于 N 的所有可能自然数的模乘逆均为:
> 模 N(=7)下模乘逆 1 为 1。
> 模 N(=7)下 2 的模乘逆为 4。
> 模 N(=7)下 3 的模乘逆为 5。
> 模 N(=7)下 4 的模乘逆为 2。
> 模 N(=7)下 5 的模乘逆为 3。
> 模 N(=7)下 6 的模乘逆为 6。
> 因此，模逆等于数本身的 N(= 7)最近的较小数是 6。
> 
> **输入:N**= 11
> T3】输出: 10

**天真法:**解决这个问题最简单的方法是[遍历所有从 1 到 N 的自然数](https://www.geeksforgeeks.org/c-program-to-print-numbers-from-1-to-n-without-using-semicolon/)，找到最大的数，使得[模 N 下数的模乘逆](https://www.geeksforgeeks.org/multiplicative-inverse-under-modulo-m/)等于数本身。

***时间复杂度:** O(N * log N)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，该想法基于以下观察:

> 与 **N** 最接近的较小数字是**(N–1)**，该数字具有与数字本身相等的**模乘逆**。
> 
> **数学证明:**
> 如果 X 和 Y 是两个数字，使得(X * Y) % N = 1 mod(N)，那么 Y 是 X 的模逆。
> 放 X = N–1，然后
> =>((N–1)* Y)% N = 1 mod(N)
> =>(N×Y)% N–Y % N = 1 mod(N)
> =>Y = N–1
> 因此，对于 X = N–1

因此，要解决问题，只需打印**N–1**作为所需答案即可。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the nearest
// smaller number satisfying
// the condition
int clstNum(int N)
{
    return (N - 1);
}

// Driver Code
int main()
{
    int N = 11;
    cout << clstNum(N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;

class GFG{

// Function to find the nearest
// smaller number satisfying
// the condition
static int clstNum(int N){ return (N - 1); }

// Driver Code
public static void main(String[] args)
{
    int N = 11;

    System.out.println(clstNum(N));
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the nearest
# smaller number satisfying
# the condition
def clstNum(N):
  return (N - 1)

# Driver Code
if __name__ == '__main__':

  N = 11

  print(clstNum(N))

# This code is contributed by akhilsaini
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to find the nearest
// smaller number satisfying
// the condition
static int clstNum(int N){ return (N - 1); }

// Driver Code
public static void Main()
{
    int N = 11;

    Console.Write(clstNum(N));
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to find the nearest
// smaller number satisfying
// the condition
function clstNum(N)
{
    return (N - 1);
}

// Driver Code
let N = 11;
document.write(clstNum(N));

// This code is contributed by subham348.
</script>
```

**Output:** 

```
10
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)