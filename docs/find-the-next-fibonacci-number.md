# 找到下一个斐波那契数

> 原文:[https://www . geesforgeks . org/find-the-next-Fibonacci-number/](https://www.geeksforgeeks.org/find-the-next-fibonacci-number/)

给定一个斐波那契数 **N** ，任务是找到下一个斐波那契数。
**例:**

> **输入:** N = 5
> **输出:** 8
> 8 是 5
> **之后的下一个斐波那契数输入:** N = 3
> **输出:** 5

**趋近:**斐波那契数列中相邻两个数的比值迅速趋近 **((1 + sqrt(5)) / 2)** 。所以如果将 **N** 乘以 **((1 + sqrt(5)) / 2)** ，取整，得到的数就是下一个斐波那契数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the next
// fibonacci number
int nextFibonacci(int n)
{
    double a = n * (1 + sqrt(5)) / 2.0;
    return round(a);
}

// Driver code
int main()
{
    int n = 5;
    cout << nextFibonacci(n);
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the next
    // fibonacci number
    static long nextFibonacci(int n)
    {
        double a = n * (1 + Math.sqrt(5)) / 2.0;
        return Math.round(a);
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 5;
        System.out.println(nextFibonacci(n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import *

# Function to return the next
# fibonacci number
def nextFibonacci(n):
    a = n*(1 + sqrt(5))/2.0
    return round(a)

# Driver code
n = 5
print(nextFibonacci(n))
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the next
    // fibonacci number
    static long nextFibonacci(int n)
    {
        double a = n * (1 + Math.Sqrt(5)) / 2.0;
        return (long)Math.Round(a);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 5;
        Console.WriteLine(nextFibonacci(n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the next
// fibonacci number
function nextFibonacci(n)
{
    let a = n * (1 + Math.sqrt(5)) / 2.0;
    return Math.round(a);
}

// Driver code

    let n = 5;
    document.write(nextFibonacci(n));

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
8
```