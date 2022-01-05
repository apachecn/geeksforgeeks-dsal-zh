# 检查 N 是否为居中三角形的程序

> 原文:[https://www . geesforgeks . org/program-to-check-if-n-a-centered-triangular-number/](https://www.geeksforgeeks.org/program-to-check-if-n-is-a-centered-triangular-number/)

给定一个整数 **N** ，任务是检查它是否是一个[居中的三角数](https://www.geeksforgeeks.org/centered-triangular-number/)。

> [**居中的三角形数**](https://www.geeksforgeeks.org/centered-triangular-number/) 是一个居中的多边形数，表示一个三角形，在连续的三角形层中，一个点在中心，所有其他点围绕中心。前几个居中的三角形数字是 1，4，10，19，31，46，64，85，109，136，…

**例:**

> **输入:** N = 4
> **输出:**是
> **输入:** 20
> **输出:**否

**进场:**

*   第 K<sup>个居中的三角数可以表示为:
    ![K^{th} Term = \frac{3*K^{2} + 3*K + 2}{2}   ](img/2c40fc5189121d39885c033b87506cd5.png "Rendered by QuickLaTeX.com")</sup> 
*   为了检查给定的数 **N** 是否可以表示为一个居中的三角数，我们需要检查![\frac{-3 + \sqrt{24*N - 15}}{6}   ](img/c522f1dedbf3b985b20749e24f393ce7.png "Rendered by QuickLaTeX.com")是否给出一个整数。

以下是上述方法的实现:

## C++

```
// C++ implementation to check
// whether a given number is a
// Centered triangular number or not
#include <bits/stdc++.h>
using namespace std;

// Function to check if the
// number is a Centered
// Triangular Number
bool isCenteredtriangular(int N)
{
    float K = (-3
               + sqrt(24 * N - 15))
              / 6;

    // Condition for K to be
    // an integer
    return (K - (int)K) == 0;
}

// Driver Code
int main()
{
    int N = 85;
    if (isCenteredtriangular(N)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check that
// a number is a centered triangular
// number or not
import java.lang.Math;

class GFG{

// Function to check that the number
// is a centered triangular number
public static boolean isCenteredTriangular(int N)
{
    double K = (-3 + Math.sqrt(24 * N - 15)) / 6;

    // Condition to check if the number
    // is a centered triangular number
    return (K - (int)K) == 0;
}

// Driver Code
public static void main(String[] args)
{
    int N = 85;

    // Function call
    if (isCenteredTriangular(N))
    {
        System.out.println("Yes");
    }
    else
    {
        System.out.println("No");
    }
}
}

// This code is contributed by ShubhamCoder
```

## 蟒蛇 3

```
# Python3 implementation to check
# whether a given number is a
# Centered triangular number or not
import math

# Function to check if the
# number is a Centered
# Triangular Number
def isCenteredtriangular(N):

    K = (-3 + math.sqrt(24 * N - 15)) / 6

    # Condition for K to be
    # an integer
    if (K - int(K)) == 0:
        return True

    return False

# Driver Code

# Given Number
N = 85

# Function call
if (isCenteredtriangular(N)):
    print("Yes")
else:
    print("No")

# This code is contributed by shubhamsingh10
```

## C#

```
// C# implementation to check whether
// a given number is a centered
// triangular number or not
using System;

class GFG{

// Function to check if the number
// is a centered triangular number
static bool isCenteredtriangular(int N)
{
    double K = (-3 + Math.Sqrt(24 * N - 15)) / 6;

    // Condition for K to be
    // an integer
    return (K - (int)K) == 0;
}

// Driver Code
static public void Main ()
{
    int N = 85;
    if (isCenteredtriangular(N))
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("No");
    }
}
}

// This code is contributed by shubhamsingh10
```

## java 描述语言

```
<script>

// JavaScript implementation to check
// whether a given number is a
// Centered triangular number or not

// Function to check if the
// number is a Centered
// Triangular Number
function isCenteredtriangular(N)
{
    var K = (-3
               + Math.sqrt(24 * N - 15))
              / 6;

    // Condition for K to be
    // an integer
    return (K - parseInt(K)) == 0;
}

// Driver Code
var N = 85;
if (isCenteredtriangular(N)) {
    document.write("Yes");
}
else {
    document.write("No");
}

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*