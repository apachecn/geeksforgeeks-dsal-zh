# 斐波那契三角形第 Kth 层的数字总和

> 原文:[https://www . geesforgeks . org/第 k 层斐波那契三角中的数字总和/](https://www.geeksforgeeks.org/sum-of-numbers-in-the-kth-level-of-a-fibonacci-triangle/)

给定一个数字 **K** ，任务是在[斐波那契三角](https://www.geeksforgeeks.org/program-print-fibonacci-triangle/)的 **Kth** 级找到数字的和。
**举例:**

```
Input: K = 3
Output: 10
Explanation: 
Fibonacci triangle till level 3:
  0
 1 1
2 3 5
Sum at 3rd level = 2 + 3 + 5 = 10

Input: K = 2
Output: 2
Explanation: 
Fibonacci triangle till level 3:
  0
 1 1
Sum at 3rd level = 1 + 1 = 2 
```

**进场:**

1.  直到第 Kt 级，即从第[1，K-1]级开始，已经使用的斐波那契数的计数可以计算为:

```
cnt = N(Level 1) + N(Level 2)
      + N(Level 3) + ... 
      + N(Level K-1)
    = 1 + 2 + 3 + ... + (K-1)
    = K*(K-1)/2
```

2.  此外，我们知道 Kth 级别将包含 K 个斐波那契数。
3.  因此我们可以在 **[(cnt + 1)，(cnt + 1 + K)]** 的范围内，将第 Kth 级的数字作为斐波那契数找到。
4.  我们可以用比奈公式求出 O(1)时间内一个范围内的斐波那契数的[和。](https://www.geeksforgeeks.org/sum-of-fibonacci-numbers-in-a-range/)

**以下是上述方法的实施:**

## C++

```
// C++ implementation to find
// the Sum of numbers in the
// Kth level of a Fibonacci triangle

#include <bits/stdc++.h>
using namespace std;
#define MAX 1000000

// Function to return
// the nth Fibonacci number
int fib(int n)
{
    double phi = (1 + sqrt(5)) / 2;
    return round(pow(phi, n) / sqrt(5));
}

// Function to return
// the required sum of the array
int calculateSum(int l, int r)
{

    // Using our deduced result
    int sum = fib(r + 2) - fib(l + 1);

    return sum;
}

// Function to return the sum of
// fibonacci in the Kth array
int sumFibonacci(int k)
{
    // Count of fibonacci which are in
    // the arrays from 1 to k - 1
    int l = (k * (k - 1)) / 2;
    int r = l + k;

    int sum = calculateSum(l, r - 1);

    return sum;
}

// Driver code
int main()
{

    int k = 3;

    cout << sumFibonacci(k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find
// the Sum of numbers in the
// Kth level of a Fibonacci triangle
import java.util.*;

class GFG
{

// Function to return
// the nth Fibonacci number
static int fib(int n)
{
    double phi = (1 + Math.sqrt(5)) / 2;
    return (int)Math.round(Math.pow(phi, n) / Math.sqrt(5));
}

// Function to return
// the required sum of the array
static int calculateSum(int l, int r)
{

    // Using our deduced result
    int sum = fib(r + 2) - fib(l + 1);

    return sum;
}

// Function to return the sum of
// fibonacci in the Kth array
static int sumFibonacci(int k)
{
    // Count of fibonacci which are in
    // the arrays from 1 to k - 1
    int l = (k * (k - 1)) / 2;
    int r = l + k;

    int sum = calculateSum(l, r - 1);

    return sum;
}

// Driver code
public static void main(String args[])
{

    int k = 3;

    System.out.println(sumFibonacci(k));
}
}

// This code is contributed by AbhiThakur
```

## 蟒蛇 3

```
# Python3 implementation to find
# the Sum of numbers in the
# Kth level of a Fibonacci triangle

import math
MAX = 1000000

# Function to return
# the nth Fibonacci number
def fib(n):

    phi = (1 + math.sqrt(5)) / 2
    return round(pow(phi, n) / math.sqrt(5))

# Function to return
# the required sum of the array
def calculateSum(l, r):

    # Using our deduced result
    sum = fib(r + 2) - fib(l + 1)

    return sum

# Function to return the sum of
# fibonacci in the Kth array
def sumFibonacci(k) :
    # Count of fibonacci which are in
    # the arrays from 1 to k - 1
    l = (k * (k - 1)) / 2
    r = l + k

    sum = calculateSum(l, r - 1)

    return sum

# Driver code
k = 3

print(sumFibonacci(k))

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# implementation to find
// the Sum of numbers in the
// Kth level of a Fibonacci triangle
using System;

class GFG 
{

// Function to return
// the nth Fibonacci number
static int fib(int n)
{
    double phi = (1 + Math.Sqrt(5)) / 2;
    return (int)Math.Round(Math.Pow(phi, n) / Math.Sqrt(5));
}

// Function to return
// the required sum of the array
static int calculateSum(int l, int r)
{

    // Using our deduced result
    int sum = fib(r + 2) - fib(l + 1);

    return sum;
}

// Function to return the sum of
// fibonacci in the Kth array
static int sumFibonacci(int k)
{
    // Count of fibonacci which are in
    // the arrays from 1 to k - 1
    int l = (k * (k - 1)) / 2;
    int r = l + k;

    int sum = calculateSum(l, r - 1);

    return sum;
}

// Driver code
public static void Main() 
{ 

    int k = 3;

    Console.Write(sumFibonacci(k));
}
}

// This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>

// Javascript implementation to find
// the Sum of numbers in the
// Kth level of a Fibonacci triangle

    // Function to return
    // the nth Fibonacci number
    function fib(n) {
        var phi = (1 + Math.sqrt(5)) / 2;
        return parseInt( Math.round
        (Math.pow(phi, n) / Math.sqrt(5)));
    }

    // Function to return
    // the required sum of the array
    function calculateSum(l , r) {

        // Using our deduced result
        var sum = fib(r + 2) - fib(l + 1);

        return sum;
    }

    // Function to return the sum of
    // fibonacci in the Kth array
    function sumFibonacci(k)
    {
        // Count of fibonacci which are in
        // the arrays from 1 to k - 1
        var l = (k * (k - 1)) / 2;
        var r = l + k;

        var sum = calculateSum(l, r - 1);

        return sum;
    }

    // Driver code

        var k = 3;

        document.write(sumFibonacci(k));

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
10
```

时间复杂度:O((log n) + (n <sup>1/2</sup> )

辅助空间:0(1)