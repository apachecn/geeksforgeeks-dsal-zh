# 计算从 1 到 N 的所有整数之和，不包括 2 的完美幂

> 原文:[https://www . geeksforgeeks . org/计算从 1 到 n 的所有整数之和-排除-2 的完美幂/](https://www.geeksforgeeks.org/calculate-sum-of-all-integers-from-1-to-n-excluding-perfect-power-of-2/)

给定一个正整数 **N** ，任务是计算从 **1 到 N** 的所有整数之和，但不包括 2 的完美幂。
**例:**

> **输入:** N = 2
> **输出:** 0
> **输入:** N = 1000000000
> **输出:**4999999998352516354

**天真法:**
天真法是迭代从 **1 到 N** 的每一个数，通过排除是 2 的完美幂的数来计算变量中的和。但是要计算数字 **10^9** 的总和，上述方法会给出[时限误差](https://www.geeksforgeeks.org/overcome-time-limit-exceedtle/)。
**时间复杂度:** O(N)
**高效方法:**
要找到期望的和，以下是步骤:

1.  使用 **O(1)** 时间中的[这篇](https://www.geeksforgeeks.org/program-find-sum-first-n-natural-numbers/)文章中讨论的公式，求出直到 **N** 的所有数字的和。
2.  因为 2 的所有完美幂的和形成了一个几何级数。因此，小于 N 的 2 的所有幂的和由以下公式计算:

> 2 的完美幂小于 N 的元素数由 **log <sub>2</sub> N** ，
> Let**r**= log<sub>2</sub>N
> 给出，所有 2 的完美幂的数之和由**2<sup>r</sup>–1**给出。

2.  从第一个 **N** 数的和中减去上面计算的 **2** 的所有完美幂的和，得到结果。

以下是上述方法的实现:

## C++

```
// C++ implementation of the
// approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the required
// summation
void findSum(int N)
{
    // Find the sum of first N
    // integers using the formula
    int sum = (N) * (N + 1) / 2;

    int r = log2(N) + 1;

    // Find the sum of numbers
    // which are exact power of
    // 2 by using the formula
    int expSum = pow(2, r) - 1;   

    // Print the final Sum
    cout << sum - expSum << endl;
}

// Driver's Code
int main()
{
    int N = 2;

    // Function to find the
    // sum
    findSum(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.lang.Math;

class GFG{

// Function to find the required
// summation
public static void findSum(int N)
{

    // Find the sum of first N
    // integers using the formula
    int sum = (N) * (N + 1) / 2;

    int r = (int)(Math.log(N) /
                  Math.log(2)) + 1;

    // Find the sum of numbers
    // which are exact power of
    // 2 by using the formula
    int expSum = (int)(Math.pow(2, r)) - 1;    

    // Print the final Sum
    System.out.println(sum - expSum);
}

// Driver Code
public static void main(String[] args)
{
    int N = 2;

    // Function to find the sum
    findSum(N);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python 3 implementation of the
# approach
from math import log2,pow

# Function to find the required
# summation
def findSum(N):
    # Find the sum of first N
    # integers using the formula
    sum = (N) * (N + 1) // 2

    r = log2(N) + 1

    # Find the sum of numbers
    # which are exact power of
    # 2 by using the formula
    expSum = pow(2, r) - 1

    # Print the final Sum
    print(int(sum - expSum))

# Driver's Code
if __name__ == '__main__':
    N = 2

    # Function to find the
    # sum
    findSum(N)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

// Function to find the required
// summation
public static void findSum(int N)
{

    // Find the sum of first N
    // integers using the formula
    int sum = (N) * (N + 1) / 2;

    int r = (int)(Math.Log(N) /
                  Math.Log(2)) + 1;

    // Find the sum of numbers
    // which are exact power of
    // 2 by using the formula
    int expSum = (int)(Math.Pow(2, r)) - 1;

    // Print the final Sum
    Console.Write(sum - expSum);
}

// Driver Code
public static void Main(string[] args)
{
    int N = 2;

    // Function to find the sum
    findSum(N);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to find the required
// summation
function findSum(N)
{

    // Find the sum of first N
    // integers using the formula
    var sum = (N) * (N + 1) / 2;

    var r = (Math.log(N) /
             Math.log(2)) + 1;

    // Find the sum of numbers
    // which are exact power of
    // 2 by using the formula
    var expSum = (Math.pow(2, r)) - 1;    

    // Print the final Sum
    document.write(sum - expSum);
}

// Driver code
var N = 2;

// Function to find the sum
findSum(N);

// This code is contributed by Kirti

</script>
```

**Output:** 

```
0
```

**时间复杂度:** O(1)

**辅助空间:** O(1)