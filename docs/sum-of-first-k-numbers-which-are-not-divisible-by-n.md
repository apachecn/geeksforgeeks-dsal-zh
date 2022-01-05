# 不能被 N 整除的前 K 个数之和

> 原文:[https://www . geeksforgeeks . org/不可被 n 整除的第一 k 个数字之和/](https://www.geeksforgeeks.org/sum-of-first-k-numbers-which-are-not-divisible-by-n/)

给定两个数字 **N** 和 **K** ，任务是找出第一个 **K** 不能被 **N** 整除的数字的和。

**示例:**

> **输入:** N = 5，K = 10
> **输出:** 63
> **说明:**的{ 1，2，3，4，6，7，8，9，11，12 }之和为 63。
> 
> **输入:** N = 3，k = 13
> **输出:** 127
> **说明:**{ 1，2，4，5，7，8，10，11，13，14，16，17，19 }之和为 127。

**方法:**为了解决这个问题，我们需要遵循以下步骤:

*   用**(K/(N-1))* N**计算 **N** 的最后倍数
*   计算**K %(N–1)**。如果余数为 0，**(K/(N-1))* N-1**给出不能被 N 整除的最后一个值，否则需要将余数加到**(K/(N-1))* N**上。
*   计算上一步得到的最后一个不能被 N 整除的值的总和。
*   计算 N 的倍数之和，从上一步计算的和中减去，得到想要的结果。

下面的代码是上述方法的实现:

## C++

```
// C++ Program to calculate
// the sum of first K
// numbers not divisible by N

#include <bits/stdc++.h>
using namespace std;

// Function to find the sum
int findSum(int n, int k)
{
    // Find the last multiple of N
    int val = (k / (n - 1)) * n;

    int rem = k % (n - 1);

    // Find the K-th non-multiple of N
    if (rem == 0) {
        val = val - 1;
    }
    else {
        val = val + rem;
    }

    // Calculate the  sum of
    // all elements from 1 to val
    int sum = (val * (val + 1)) / 2;

    // Calculate the sum of
    // all multiples of N
    // between 1 to val
    int x = k / (n - 1);
    int sum_of_multiples
        = (x
           * (x + 1) * n)
          / 2;
    sum -= sum_of_multiples;

    return sum;
}

// Driver code
int main()
{
    int n = 7, k = 13;
    cout << findSum(n, k)
         << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate
// the sum of first K numbers
// not divisible by N
import java.util.*;

class GFG {

// Function to find the sum
static int findSum(int n, int k)
{

    // Find the last multiple of N
    int val = (k / (n - 1)) * n;

    int rem = k % (n - 1);

    // Find the K-th non-multiple of N
    if (rem == 0)
    {
        val = val - 1;
    }
    else
    {
        val = val + rem;
    }

    // Calculate the sum of
    // all elements from 1 to val
    int sum = (val * (val + 1)) / 2;

    // Calculate the sum of
    // all multiples of N
    // between 1 to val
    int x = k / (n - 1);
    int sum_of_multiples = (x * (x + 1) * n) / 2;
    sum -= sum_of_multiples;

    return sum;
}

// Driver code
public static void main(String[] args)
{
    int n = 7, k = 13;

    System.out.println(findSum(n, k));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 Program to calculate
# the sum of first K
# numbers not divisible by N

# Function to find the sum
def findSum(n, k):

    # Find the last multiple of N
    val = (k // (n - 1)) * n;

    rem = k % (n - 1);

    # Find the K-th non-multiple of N
    if (rem == 0):
        val = val - 1;

    else:
        val = val + rem;

    # Calculate the sum of
    # all elements from 1 to val
    sum = (val * (val + 1)) // 2;

    # Calculate the sum of
    # all multiples of N
    # between 1 to val
    x = k // (n - 1);
    sum_of_multiples = (x * (x + 1) * n) // 2;
    sum -= sum_of_multiples;

    return sum;

# Driver code
n = 7; k = 13;
print(findSum(n, k))

# This code is contributed by Code_Mech
```

## C#

```
// C# program to calculate
// the sum of first K numbers
// not divisible by N
using System;

class GFG{

// Function to find the sum
static int findSum(int n, int k)
{

    // Find the last multiple of N
    int val = (k / (n - 1)) * n;

    int rem = k % (n - 1);

    // Find the K-th non-multiple of N
    if (rem == 0)
    {
        val = val - 1;
    }
    else
    {
        val = val + rem;
    }

    // Calculate the sum of
    // all elements from 1 to val
    int sum = (val * (val + 1)) / 2;

    // Calculate the sum of
    // all multiples of N
    // between 1 to val
    int x = k / (n - 1);
    int sum_of_multiples = (x * (x + 1) * n) / 2;
    sum -= sum_of_multiples;

    return sum;
}

// Driver code
public static void Main(String[] args)
{
    int n = 7, k = 13;

    Console.WriteLine(findSum(n, k));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript Program to calculate
// the sum of first K
// numbers not divisible by N

// Function to find the sum
function findSum(n, k)
{

    // Find the last multiple of N
    var val = parseInt(k / (n - 1)) * n;

    var rem = k % (n - 1);

    // Find the K-th non-multiple of N
    if (rem == 0)
    {
        val = val - 1;
    }
    else
    {
        val = val + rem;
    }

    // Calculate the  sum of
    // all elements from 1 to val
    var sum = parseInt((val * (val + 1)) / 2);

    // Calculate the sum of
    // all multiples of N
    // between 1 to val
    var x = parseInt(k / (n - 1));
    var sum_of_multiples = parseInt(
        (x * (x + 1) * n) / 2);

    sum -= sum_of_multiples;

    return sum;
}

// Driver code
var n = 7, k = 13;

document.write(findSum(n, k))

// This code is contributed by rrrtnx

</script>
```

**Output:** 

```
99
```

**时间复杂度:***O(1)*
T5】辅助空间复杂度: *O(1)*