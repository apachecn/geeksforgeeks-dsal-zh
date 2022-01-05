# 两个 n 位数的最小和最大值

> 原文:[https://www . geesforgeks . org/最小和最大两位数之和/](https://www.geeksforgeeks.org/smallest-and-largest-sum-of-two-n-digit-numbers/)

给定一个整数 **N ≥ 1** ，任务是求两个 **N** 位数的最小和最大。
**例:**

> **输入:** N = 1
> **输出:**
> 最大= 18
> 最小= 0
> 最大 1 位数为 9 和 9 + 9 = 18
> 最小 1 位数为 0 和 0 + 0 = 0
> **输入:** N = 2
> **输出:**
> 最大= 198
> 最小= 20

**进场:**

*   **最大:**答案将是**2 *(10<sup>N</sup>–1)**，因为两个 **n** 数字的和序列将像 **2 * 9、2 * 99、2 * 999、…** 一样继续
*   **最小:**
    *   如果 **N = 1** ，则答案为 **0** 。
    *   如果 **N > 1** 那么答案将是**2 *(10<sup>N–1</sup>)**，因为两个 **n** 数字的和的数列将会像 **0、20、200、2000、…** 一样继续下去

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the smallest sum
// of 2 n-digit numbers
int smallestSum(int n)
{
    if (n == 1)
        return 0;
    return (2 * pow(10, n - 1));
}

// Function to return the largest sum
// of 2 n-digit numbers
int largestSum(int n)
{
    return (2 * (pow(10, n) - 1));
}

// Driver code
int main()
{
    int n = 4;
    cout << "Largest = " << largestSum(n) << endl;
    cout << "Smallest = " << smallestSum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the smallest sum
    // of 2 n-digit numbers
    static int smallestSum(int n)
    {
        if (n == 1)
            return 0;
        return (2 * (int)Math.pow(10, n - 1));
    }

    // Function to return the largest sum
    // of 2 n-digit numbers
    static int largestSum(int n)
    {
        return (2 * ((int)Math.pow(10, n) - 1));
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 4;
        System.out.println("Largest = " + largestSum(n));
        System.out.print("Smallest = " + smallestSum(n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the smallest sum
# of 2 n-digit numbers
def smallestSum(n):

    if (n == 1):
        return 0
    return (2 * pow(10, n - 1))

# Function to return the largest sum
# of 2 n-digit numbers
def largestSum(n):
    return (2 * (pow(10, n) - 1))

# Driver code
n = 4
print("Largest = ", largestSum(n))
print("Smallest = ", smallestSum(n))
```

## C#

```
// C# implementation of the approach
using System;
class GFG {

    // Function to return the smallest sum
    // of 2 n-digit numbers
    static int smallestSum(int n)
    {
        if (n == 1)
            return 0;
        return (2 * (int)Math.Pow(10, n - 1));
    }

    // Function to return the largest sum
    // of 2 n-digit numbers
    static int largestSum(int n)
    {
        return (2 * ((int)Math.Pow(10, n) - 1));
    }

    // Driver code
    public static void Main()
    {
        int n = 4;
        Console.WriteLine("Largest = " + largestSum(n));
        Console.Write("Smallest = " + smallestSum(n));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the smallest sum
// of 2 n-digit numbers
function smallestSum($n)
{
    if ($n == 1)
        return 0;
    return (2 * pow(10, $n - 1));
}

// Function to return the largest sum
// of 2 n-digit numbers
function largestSum($n)
{
    return 2 * ( pow(10, $n) - 1 );
}

// Driver code
$n = 4;
echo "Largest = " . largestSum($n) . "\n";
echo "Smallest = " . smallestSum($n);
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the smallest sum
// of 2 n-digit numbers
function smallestSum(n)
{
    if (n == 1)
        return 0;
    return (2 * Math.pow(10, n - 1));
}

// Function to return the largest sum
// of 2 n-digit numbers
function largestSum(n)
{
    return (2 * (Math.pow(10, n) - 1));
}

// Driver code
var n = 4;
document.write("Largest = " + largestSum(n) + "<br>");
document.write("Smallest = " + smallestSum(n));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
Largest = 19998
Smallest = 2000
```