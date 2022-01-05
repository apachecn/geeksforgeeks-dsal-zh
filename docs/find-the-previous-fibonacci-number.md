# 找到之前的斐波那契数

> 原文:[https://www . geesforgeks . org/find-the-previous-Fibonacci-number/](https://www.geeksforgeeks.org/find-the-previous-fibonacci-number/)

给定一个[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/) **N** ，任务是找到前一个斐波那契数。
**例:**

> **输入:** N = 8
> **输出:** 5
> 5 是 8 之前的前一个斐波那契数。
> **输入:** N = 5
> **输出:** 3

**趋近:**斐波那契数列中相邻两个数的比值迅速趋近 **((1 + sqrt(5)) / 2)** 。所以如果 **N** 除以 **((1 + sqrt(5)) / 2)** 再取整，结果数就是之前的斐波那契数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>

using namespace std;

// Function to return the previous
// fibonacci number
int previousFibonacci(int n)
{
    double a = n / ((1 + sqrt(5)) / 2.0);
    return round(a);
}

// Driver code
int main()
{
    int n = 8;
    cout << (previousFibonacci(n));
}

// This code is contributed by Mohit Kumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to return the previous
// fibonacci number
static int previousFibonacci(int n)
{
    double a = n / ((1 + Math.sqrt(5)) / 2.0);
    return (int)Math.round(a);
}

// Driver code
public static void main (String[] args)
{
    int n = 8;
    System.out.println(previousFibonacci(n));
}
}

// This code is contributed by ajit.
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import *

# Function to return the previous
# fibonacci number
def previousFibonacci(n):
    a = n/((1 + sqrt(5))/2.0)
    return round(a)

# Driver code
n = 8
print(previousFibonacci(n))
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the previous
// fibonacci number
static int previousFibonacci(int n)
{
    double a = n / ((1 + Math.Sqrt(5)) / 2.0);
    return (int)Math.Round(a);
}

// Driver code
public static void Main()
{
    int n = 8;
    Console.Write(previousFibonacci(n));
}
}

// This code is contributed by Akanksha_Rai
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the previous
// fibonacci number
function previousFibonacci(n)
{
    var a = n / ((1 + Math.sqrt(5)) / 2);
    return Math.round(a);
}

// Driver code
var n = 8;
document.write(previousFibonacci(n));

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
5
```