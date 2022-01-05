# 晴天号

> 原文:[https://www.geeksforgeeks.org/sunny-number/](https://www.geeksforgeeks.org/sunny-number/)

给定一个正整数 **N** ，任务是检查给定的数字 **N** 是否为晴天数。

> 如果 **N + 1** 是[完美方块](https://www.geeksforgeeks.org/check-if-a-number-is-perfect-square-without-finding-square-root/)，那么数字 **N** 就是晴天。

**示例:**

> **输入:** N = 8
> **输出:**是
> **说明:**
> 既然 9 是一个完美的正方形。因此 8 是一个阳光明媚的数字。
> 
> **输入:** N = 11
> **输出:**否
> **说明:**
> 既然 12 不是一个完美的正方形。因此，8 不是一个阳光灿烂的数字。

**进场:**思路是检查 **(N + 1)** 是否为[完美方块](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)。
以下是上述方法的实现:

## C++

```
// C++ program for the above approach

#include "bits/stdc++.h"
using namespace std;

// Function check whether x is a
// perfect square or not
bool isPerfectSquare(long double x)
{

    // Find floating point value of
    // square root of x.
    long double sr = sqrt(x);

    // If square root is an integer
    return((sr - floor(sr)) == 0);
}

// Function to check Sunny Number
void checkSunnyNumber(int N)
{

    // Check if (N + 1) is a perfect
    // square or not
    if (isPerfectSquare(N + 1)) {
        cout << "Yes\n";
    }

    // If (N+1) is not a perfect square
    else {
        cout << "No\n";
    }
}

// Driver Code
int main()
{

    // Given Number
    int N = 8;

    // Function call
    checkSunnyNumber(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

// Function check whether x is a
// perfect square or not
static boolean isPerfectSquare(double x)
{

    // Find floating point value of
    // square root of x.
    double sr = Math.sqrt(x);

    // If square root is an integer
    return((sr - Math.floor(sr)) == 0);
}

// Function to check Sunny Number
static void checkSunnyNumber(int N)
{

    // Check if (N + 1) is a perfect
    // square or not
    if (isPerfectSquare(N + 1))
    {
        System.out.println("Yes");
    }

    // If (N+1) is not a perfect square
    else
    {
        System.out.println("No");
    }
}

// Driver code
public static void main(String[] args)
{

    // Given Number
    int N = 8;

    // Function call
    checkSunnyNumber(N);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import *

# Function check whether x is a
# perfect square or not
def isPerfectSquare(x):

    # Find floating point value of
    # square root of x.
    sr = sqrt(x)

    # If square root is an integer
    return((sr - floor(sr)) == 0)

# Function to check Sunny Number
def checkSunnyNumber(N):

    # Check if (N + 1) is a perfect
    # square or not
    if (isPerfectSquare(N + 1)):
        print("Yes")

    # If (N+1) is not a perfect square
    else:
        print("No")

# Driver Code
if __name__ == '__main__':

    # Given Number
    N = 8

    # Function call
    checkSunnyNumber(N)

# This code is contributed by Bhupendra_Singh
```

## C#

```
// C# program for the above approach
using System;

class GFG {

// Function check whether x is
// a perfect square or not
static bool isPerfectSquare(double x)
{

    // Find floating point value of
    // square root of x.
    double sr = Math.Sqrt(x);

    // If square root is an integer
    return((sr - Math.Floor(sr)) == 0);
}

// Function to check sunny number
static void checkSunnyNumber(int N)
{

    // Check if (N + 1) is a perfect
    // square or not
    if (isPerfectSquare(N + 1))
    {
        Console.WriteLine("Yes");
    }

    // If (N+1) is not a perfect square
    else
    {
        Console.WriteLine("No");
    }
}

// Driver code
public static void Main(String[] args)
{

    // Given Number
    int N = 8;

    // Function call
    checkSunnyNumber(N);
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function check whether x is a
// perfect square or not
function isPerfectSquare(x)
{

    // Find floating point value of
    // square root of x.
    var sr = Math.sqrt(x);

    // If square root is an integer
    return((sr - Math.floor(sr)) == 0);
}

// Function to check Sunny Number
function checkSunnyNumber(N)
{

    // Check if (N + 1) is a perfect
    // square or not
    if (isPerfectSquare(N + 1)) {
        document.write( "Yes");
    }

    // If (N+1) is not a perfect square
    else {
        document.write( "No");
    }
}

// Driver Code
// Given Number
var N = 8;

// Function call
checkSunnyNumber(N);

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(1)

**辅助空间:** O(1)