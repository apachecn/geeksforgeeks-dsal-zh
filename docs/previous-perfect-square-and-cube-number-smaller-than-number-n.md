# 以前的完美正方形和小于 N 的立方体数量

> 原文:[https://www . geeksforgeeks . org/previous-perfect-square-and-cube-number-小于 number-n/](https://www.geeksforgeeks.org/previous-perfect-square-and-cube-number-smaller-than-number-n/)

给定一个整数 **N** ，任务是找到比数字 **N** 小的前一个[完美正方形](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)或[完美立方体](https://www.geeksforgeeks.org/perfect-cube/)。
**示例**:

> **输入:** N = 6
> **输出:**
> 完美正方= 4
> 完美正方= 1
> **输入:** N = 30
> **输出:**
> 完美正方= 25
> 完美正方= 27

**方法:**小于 **N** 的前一个完美平方数可以计算如下:

*   求给定数 **N** 的平方根。
*   使用各自语言的[楼层功能](https://www.geeksforgeeks.org/ceil-floor-functions-cpp/)计算其楼层值。
*   然后减去 1，如果 N 已经是一个完美的正方形。
*   打印该数字的平方。

小于 **N** 的前一个完美立方数可以计算如下:

*   求给定 n 的立方根。
*   使用各自语言的[楼层功能](https://www.geeksforgeeks.org/ceil-floor-functions-cpp/)计算其楼层值。
*   然后减去 1，如果 N 已经是一个完美的立方体。
*   打印该数字的立方体。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// previous perfect square and cube
// smaller than the given number

#include <cmath>
#include <iostream>

using namespace std;

// Function to find the previous
// perfect square of the number N
int previousPerfectSquare(int N)
{
    int prevN = floor(sqrt(N));

    // If N is already a perfect square
    // decrease prevN by 1.
    if (prevN * prevN == N)
        prevN -= 1;

    return prevN * prevN;
}

// Function to find the
// previous perfect cube
int previousPerfectCube(int N)
{
    int prevN = floor(cbrt(N));

    // If N is already a perfect cube
    // decrease prevN by 1.
    if (prevN * prevN * prevN == N)
        prevN -= 1;

    return prevN * prevN * prevN;
}

// Driver Code
int main()
{
    int n = 30;
    cout << previousPerfectSquare(n) << "\n";
    cout << previousPerfectCube(n) << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// previous perfect square and cube
// smaller than the given number
import java.util.*;

class GFG{

// Function to find the previous
// perfect square of the number N
static int previousPerfectSquare(int N)
{
    int prevN = (int)Math.floor(Math.sqrt(N));

    // If N is already a perfect square
    // decrease prevN by 1.
    if (prevN * prevN == N)
        prevN -= 1;

    return prevN * prevN;
}

// Function to find the
// previous perfect cube
static int previousPerfectCube(int N)
{
    int prevN = (int)Math.floor(Math.cbrt(N));

    // If N is already a perfect cube
    // decrease prevN by 1.
    if (prevN * prevN * prevN == N)
        prevN -= 1;

    return prevN * prevN * prevN;
}

// Driver Code
public static void main(String[] args)
{
    int n = 30;
    System.out.println(previousPerfectSquare(n));
    System.out.println(previousPerfectCube(n));
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 implementation to find the
# previous perfect square and cube
# smaller than the given number
import math
import numpy as np

# Function to find the previous
# perfect square of the number N
def previousPerfectSquare(N):

    prevN = math.floor(math.sqrt(N));

    # If N is already a perfect square
    # decrease prevN by 1.
    if (prevN * prevN == N):
        prevN -= 1;

    return prevN * prevN;

# Function to find the
# previous perfect cube
def previousPerfectCube(N):

    prevN = math.floor(np.cbrt(N));

    # If N is already a perfect cube
    # decrease prevN by 1.
    if (prevN * prevN * prevN == N):
        prevN -= 1;

    return prevN * prevN * prevN;

# Driver Code
n = 30;

print(previousPerfectSquare(n));
print(previousPerfectCube(n));

# This code is contributed by Code_Mech
```

## C#

```
// C# implementation to find the
// previous perfect square and cube
// smaller than the given number
using System;

class GFG{

// Function to find the previous
// perfect square of the number N
static int previousPerfectSquare(int N)
{
    int prevN = (int)Math.Floor(Math.Sqrt(N));

    // If N is already a perfect square
    // decrease prevN by 1.
    if (prevN * prevN == N)
        prevN -= 1;

    return prevN * prevN;
}

// Function to find the
// previous perfect cube
static int previousPerfectCube(int N)
{
    int prevN = (int)Math.Floor(Math.Cbrt(N));

    // If N is already a perfect cube
    // decrease prevN by 1.
    if (prevN * prevN * prevN == N)
        prevN -= 1;

    return prevN * prevN * prevN;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 30;

    Console.WriteLine(previousPerfectSquare(n));
    Console.WriteLine(previousPerfectCube(n));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>
// JavaScript implementation to find the
// previous perfect square and cube
// smaller than the given number

// Function to find the previous
// perfect square of the number N
function previousPerfectSquare(N)
{
    let prevN = Math.floor(Math.sqrt(N));

    // If N is already a perfect square
    // decrease prevN by 1.
    if (prevN * prevN == N)
        prevN -= 1;

    return prevN * prevN;
}

// Function to find the
// previous perfect cube
function previousPerfectCube(N)
{
    let prevN = Math.floor(Math.cbrt(N));

    // If N is already a perfect cube
    // decrease prevN by 1.
    if (prevN * prevN * prevN == N)
        prevN -= 1;

    return prevN * prevN * prevN;
}

// Driver Code
    let n = 30;
    document.write(previousPerfectSquare(n) + "<br>");
    document.write(previousPerfectCube(n) + "<br>");

// This code is contributed by Manoj.
</script>
```

**Output:** 

```
25
27
```

***时间复杂度:** O(sqrt(n))*

***辅助空间:** O(1)*