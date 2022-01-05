# 查找下一个非斐波那契数

> 原文:[https://www . geesforgeks . org/find-the-next-non-Fibonacci-number/](https://www.geeksforgeeks.org/find-the-next-non-fibonacci-number/)

给定一个数字 **N** ，任务是找到下一个[非斐波那契数](https://www.geeksforgeeks.org/nth-non-fibonacci-number/)。
**例:**

> **输入:** N = 4
> **输出:** 6
> 6 是 4
> **之后的下一个非斐波那契数输入:** N = 6
> **输出:** 7

**方法:**作为[斐波那契数列](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)作为
给出

> 0, 1, 1, 2, 3, 5, 8, 13, 21, 34….

可以观察到**不存在任何 2 个连续的斐波那契数**。因此，为了找到下一个非斐波那契数，出现了以下情况:

1.  如果 **N < = 3** ，那么下一个非斐波那契数将是 **4**
2.  如果 **N > 3** ，那么我们将[检查 *(N + 1)* 是否为斐波那契数](https://www.geeksforgeeks.org/check-number-fibonacci-number/)。
    *   如果 **(N + 1)** 是斐波那契数，那么(N + 2)将是下一个非斐波那契数。

    *   否则(N + 1)将是答案

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a
// number is perfect square
bool isPerfectSquare(int x)
{
    int s = sqrt(x);
    return (s * s == x);
}

// Function to check if a
// number is Fibinacci Number
bool isFibonacci(int N)
{
    // N is Fibinacci if either
    // (5*N*N + 4), (5*N*N - 4) or both
    // is a perferct square
    return isPerfectSquare(5 * N * N + 4)
           || isPerfectSquare(5 * N * N - 4);
}

// Function to find
// the next Non-Fibinacci Number
int nextNonFibonacci(int N)
{

    // Case 1
    // If N<=3, then 4 will be
    // next Non-Fibinacci Number
    if (N <= 3)
        return 4;

    // Case 2
    // If N+1 is Fibinacci, then N+2
    // will be next Non-Fibinacci Number
    if (isFibonacci(N + 1))
        return N + 2;

    // If N+1 is Non-Fibinacci, then N+2
    // will be next Non-Fibinacci Number
    else
        return N + 1;
}

// Driver code
int main()
{
    int N = 3;
    cout << nextNonFibonacci(N)
         << endl;

    N = 5;
    cout << nextNonFibonacci(N)
         << endl;

    N = 7;
    cout << nextNonFibonacci(N)
         << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG{

// Function to check if a
// number is perfect square
static boolean isPerfectSquare(int x)
{
    int s = (int) Math.sqrt(x);
    return (s * s == x);
}

// Function to check if a
// number is Fibinacci Number
static boolean isFibonacci(int N)
{
    // N is Fibinacci if either
    // (5*N*N + 4), (5*N*N - 4) or both
    // is a perferct square
    return isPerfectSquare(5 * N * N + 4)
           || isPerfectSquare(5 * N * N - 4);
}

// Function to find
// the next Non-Fibinacci Number
static int nextNonFibonacci(int N)
{

    // Case 1
    // If N<=3, then 4 will be
    // next Non-Fibinacci Number
    if (N <= 3)
        return 4;

    // Case 2
    // If N+1 is Fibinacci, then N+2
    // will be next Non-Fibinacci Number
    if (isFibonacci(N + 1))
        return N + 2;

    // If N+1 is Non-Fibinacci, then N+2
    // will be next Non-Fibinacci Number
    else
        return N + 1;
}

// Driver code
public static void main(String[] args)
{
    int N = 3;
    System.out.print(nextNonFibonacci(N)
         +"\n");

    N = 5;
    System.out.print(nextNonFibonacci(N)
         +"\n");

    N = 7;
    System.out.print(nextNonFibonacci(N)
         +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
from math import sqrt

# Function to check if a
# number is perfect square
def isPerfectSquare(x):
    s = sqrt(x)
    return (s * s == x)

# Function to check if a
# number is Fibinacci Number
def isFibonacci(N):

    # N is Fibinacci if either
    # (5*N*N + 4), (5*N*N - 4) or both
    # is a perferct square
    return isPerfectSquare(5 * N * N + 4) or \
            isPerfectSquare(5 * N * N - 4)

# Function to find
# the next Non-Fibinacci Number
def nextNonFibonacci(N):

    # Case 1
    # If N<=3, then 4 will be
    # next Non-Fibinacci Number
    if (N <= 3):
        return 4

    # Case 2
    # If N+1 is Fibinacci, then N+2
    # will be next Non-Fibinacci Number
    if (isFibonacci(N + 1)):
        return N + 2

    # If N+1 is Non-Fibinacci, then N+2
    # will be next Non-Fibinacci Number
    else:
        return N

# Driver code
if __name__ == '__main__':
    N = 3
    print(nextNonFibonacci(N))
    N = 4
    print(nextNonFibonacci(N))

    N = 7
    print(nextNonFibonacci(N))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG{

// Function to check if a
// number is perfect square
static bool isPerfectSquare(int x)
{
    int s = (int) Math.Sqrt(x);
    return (s * s == x);
}

// Function to check if a
// number is Fibinacci Number
static bool isFibonacci(int N)
{
    // N is Fibinacci if either
    // (5*N*N + 4), (5*N*N - 4) or both
    // is a perferct square
    return isPerfectSquare(5 * N * N + 4)
           || isPerfectSquare(5 * N * N - 4);
}

// Function to find
// the next Non-Fibinacci Number
static int nextNonFibonacci(int N)
{

    // Case 1
    // If N<=3, then 4 will be
    // next Non-Fibinacci Number
    if (N <= 3)
        return 4;

    // Case 2
    // If N+1 is Fibinacci, then N+2
    // will be next Non-Fibinacci Number
    if (isFibonacci(N + 1))
        return N + 2;

    // If N+1 is Non-Fibinacci, then N+2
    // will be next Non-Fibinacci Number
    else
        return N + 1;
}

// Driver code
public static void Main(String[] args)
{
    int N = 3;
    Console.Write(nextNonFibonacci(N)
         +"\n");

    N = 5;
    Console.Write(nextNonFibonacci(N)
         +"\n");

    N = 7;
    Console.Write(nextNonFibonacci(N)
         +"\n");
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to check if a
// number is perfect square
function isPerfectSquare(x)
{
    var s = parseInt(Math.sqrt(x));
    return (s * s == x);
}

// Function to check if a
// number is Fibinacci Number
function isFibonacci(N)
{
    // N is Fibinacci if either
    // (5*N*N + 4), (5*N*N - 4) or both
    // is a perferct square
    return isPerfectSquare(5 * N * N + 4)
           || isPerfectSquare(5 * N * N - 4);
}

// Function to find
// the next Non-Fibinacci Number
function nextNonFibonacci(N)
{

    // Case 1
    // If N<=3, then 4 will be
    // next Non-Fibinacci Number
    if (N <= 3)
        return 4;

    // Case 2
    // If N+1 is Fibinacci, then N+2
    // will be next Non-Fibinacci Number
    if (isFibonacci(N + 1))
        return N + 2;

    // If N+1 is Non-Fibinacci, then N+2
    // will be next Non-Fibinacci Number
    else
        return N + 1;
}

// Driver code
var N = 3;
document.write(nextNonFibonacci(N)+"<br>");
N = 5;
document.write(nextNonFibonacci(N)+"<br>");
N = 7;
document.write(nextNonFibonacci(N)+"<br>");

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
4
6
9
```

时间复杂度:O(n <sup>1/2</sup> )

辅助空间:0(1)