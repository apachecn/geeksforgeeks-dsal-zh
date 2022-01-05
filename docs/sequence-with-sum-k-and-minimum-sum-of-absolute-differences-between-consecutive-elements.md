# 连续元素间绝对差之和 K 和最小的序列

> 原文:[https://www . geeksforgeeks . org/序列与连续元素之间的 k 和最小绝对差之和/](https://www.geeksforgeeks.org/sequence-with-sum-k-and-minimum-sum-of-absolute-differences-between-consecutive-elements/)

给定两个整数 **N** 和 **K** ，任务是找到一个长度为 **N** 的整数序列，使得该序列的所有元素之和为 **K** ，并且所有连续元素之间的绝对差之和最小。打印这个最小化的总和。

**示例:**

> **输入:** N = 3，K = 56
> **输出:** 1
> 序列为{19，19，18}，所有连续元素的绝对
> 差之和为
> | 19–19 |+| 19–18 | = 0+1 = 1，这是最小可能。
> 
> **输入:** N = 12，K = 48
> **输出:** 0
> 顺序为{4，4，4，4，4，4，4，4，4，4，4，4，4，4，4，4，4，4，4，4，4，4}。

**进场:**可以有两种情况:

1.  当 **K % N = 0** 时，答案将是 **0** ，因为 **K** 可以被均匀地分成 **N** 个部分，即序列的每个元素都是相等的。
2.  当 **K % N！= 0** 那么答案将是 **1** ，因为序列可以按如下方式排列:
    *   **(K –( K % N))**可被 **N** 整除，因此可以在所有 **N** 零件之间平均分配。
    *   剩余的 **(K % N)** 值可以这样划分，以使连续的绝对差最小化，即将 **1** 添加到第一个或最后一个 **(K % N)** 元素，序列将是类型 **{x，x，x，x，y，y，y，y}** ，产生最小和作为 **1** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the minimized sum
int minimum_sum(int n, int k)
{

    // If k is divisible by n
    // then the answer will be 0
    if (k % n == 0)
        return 0;

    // Else the answer will be 1
    return 1;
}

// Driver code
int main()
{
    int n = 3, k = 56;

    cout << minimum_sum(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to return the minimized sum
static int minimum_sum(int n, int k)
{

    // If k is divisible by n
    // then the answer will be 0
    if (k % n == 0)
        return 0;

    // Else the answer will be 1
    return 1;
}

// Driver code
public static void main (String[] args)
{

    int n = 3, k = 56;
    System.out.println (minimum_sum(n, k));
}
}

// This code is contributed By @ajit_23
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimized sum
def minimum_sum(n, k):

    # If k is divisible by n
    # then the answer will be 0
    if (k % n == 0):
        return 0;

    # Else the answer will be 1
    return 1

# Driver code

n = 3
k = 56

print(minimum_sum(n, k))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the minimized sum
static int minimum_sum(int n, int k)
{

    // If k is divisible by n
    // then the answer will be 0
    if (k % n == 0)
        return 0;

    // Else the answer will be 1
    return 1;
}

// Driver code
static public void Main ()
{
    int n = 3, k = 56;
    Console.Write(minimum_sum(n, k));
}
}

// This code is contributed By Tushil
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the minimized sum
function minimum_sum(n, k)
{

    // If k is divisible by n
    // then the answer will be 0
    if (k % n == 0)
        return 0;

    // Else the answer will be 1
    return 1;
}

// Driver code
let n = 3, k = 56;

document.write(minimum_sum(n, k));

// This code is contributed by rishavmahato348

</script>
```

**Output:** 

```
1
```