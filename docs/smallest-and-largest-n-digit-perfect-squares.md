# 最小和最大的 N 位数完美正方形

> 原文:[https://www . geesforgeks . org/最小和最大 n 位数完美方块/](https://www.geeksforgeeks.org/smallest-and-largest-n-digit-perfect-squares/)

给定一个整数 N，任务是找出最小和最大的 N 位数，它们也是完美的正方形。
**例:**

> **输入:** N = 2
> **输出:** 16 81
> 16 和 18 是最小和最大的两位完美正方形。
> **输入:** N = 3
> **输出:** 100 961

**方式:**从 **N = 1** 开始增加 **N** 的数值，系列会像 **9、81、961、9801、…..**为**最大的 N 位数完美平方**，其**第 N 项**为**幂(ceil(sqrt(pow(10，N)))–1，2)** 。
和 **1，16，100，1024，…..**为**最小的 N 位数完美平方**，其**第 N 项**为**幂(ceil(sqrt(pow(10，N-1)))、2)** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the largest and
// the smallest n-digit perfect squares
void nDigitPerfectSquares(int n)
{

    // Smallest n-digit perfect square
    cout << pow(ceil(sqrt(pow(10, n - 1))), 2) << " ";

    // Largest n-digit perfect square
    cout << pow(ceil(sqrt(pow(10, n))) - 1, 2);
}

// Driver code
int main()
{
    int n = 4;
    nDigitPerfectSquares(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to print the largest and
    // the smallest n-digit perfect squares
    static void nDigitPerfectSquares(int n)
    {
        // Smallest n-digit perfect square
        int smallest = (int)Math.pow(Math.ceil(Math.sqrt(Math.pow(10, n - 1))), 2);
        System.out.print(smallest + " ");

        // Largest n-digit perfect square
        int largest = (int)Math.pow(Math.ceil(Math.sqrt(Math.pow(10, n))) - 1, 2);
        System.out.print(largest);
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 4;
        nDigitPerfectSquares(n);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math

# Function to print the largest and
# the smallest n-digit perfect squares
def nDigitPerfectSquares(n):

    # Smallest n-digit perfect square
    print(pow(math.ceil(math.sqrt(pow(10, n - 1))), 2),
                                            end = " ");

    # Largest n-digit perfect square
    print(pow(math.ceil(math.sqrt(pow(10, n))) - 1, 2));

# Driver code
n = 4;
nDigitPerfectSquares(n);

# This code is contributed by mits
```

## C#

```
// C# implementation of the approach
using System;
public class GFG {

    // Function to print the largest and
    // the smallest n-digit perfect squares
    static void nDigitPerfectSquares(int n)
    {
        // Smallest n-digit perfect square
        int smallest = (int)Math.Pow(Math.Ceiling(Math.Sqrt(Math.Pow(10, n - 1))), 2);
        Console.Write(smallest + " ");

        // Largest n-digit perfect square
        int largest = (int)Math.Pow(Math.Ceiling(Math.Sqrt(Math.Pow(10, n))) - 1, 2);
        Console.Write(largest);
    }

    // Driver code
    public static void Main(String []args)
    {
        int n = 4;
        nDigitPerfectSquares(n);
    }
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to print the largest and
// the smallest n-digit perfect squares
function nDigitPerfectSquares($n)
{

    // Smallest n-digit perfect square
    echo pow(ceil(sqrt(pow(10, $n - 1))), 2), " ";

    // Largest n-digit perfect square
    echo pow(ceil(sqrt(pow(10, $n))) - 1, 2);
}

// Driver code
$n = 4;
nDigitPerfectSquares($n);

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to print the largest and
// the smallest n-digit perfect squares
function nDigitPerfectSquares(n)
{

    // Smallest n-digit perfect square
    document.write(Math.pow(Math.ceil(Math.sqrt(Math.pow(10, n - 1))), 2) + " ");

    // Largest n-digit perfect square
    document.write(Math.pow(Math.ceil(Math.sqrt(Math.pow(10, n))) - 1, 2));
}

// Driver code
var n = 4;
nDigitPerfectSquares(n);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
1024 9801
```