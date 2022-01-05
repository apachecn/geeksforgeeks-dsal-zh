# 数组中三元组对之间绝对差的最小和

> 原文:[https://www . geeksforgeeks . org/数组三重数对之间的最小绝对差之和/](https://www.geeksforgeeks.org/minimum-sum-of-absolute-differences-between-pairs-of-a-triplet-from-an-array/)

给定一个由正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **A[]** ，任务是从数组中找出任意三元组 **(A[x]，A[y]，A[y]|+| A[y]–A[z]|**(A[x]，A[y]，A[z]) 的最小值。

**示例:**

> **输入:** A[] = { 1，1，2，3 }
> **输出:** 1
> **解释:**
> 对于 x = 0，y = 1，z = 2
> | A[x]–A[y]|+| A[y]–A[z]| = 0+1 = 1，这是最大可能
> 
> **输入:** A[] = { 1，1，1 }
> T3】输出: 0

**接近**:问题可以解决[贪婪的](https://www.geeksforgeeks.org/greedy-algorithms/)。按照以下步骤解决问题:

1.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。
2.  [按升序排列数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
3.  [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)超过索引**【0，N–3】**。对于每个 i <sup>第</sup>个索引，设置 **x = i，y = i + 1，z = i + 2**
4.  计算三联体 **(x，y，z)** 的和。
5.  更新最小可能总和。
6.  打印获得的最小总和。

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum
// sum of absolute differences
// of pairs of a triplet
int minimum_sum(int A[], int N)
{
    // Sort the array
    sort(A, A + N);

    // Stores the minimum sum
    int sum = INT_MAX;

    // Traverse the array
    for (int i = 0; i <= N - 3; i++) {

        // Update the minimum sum
        sum = min(sum,
                  abs(A[i] - A[i + 1]) +
                  abs(A[i + 1] - A[i + 2]));
    }

    // Print the minimum sum
    cout << sum;
}

// Driver Code
int main()
{

    // Input
    int A[] = { 1, 1, 2, 3 };
    int N = sizeof(A) / sizeof(A[0]);

    // Function call to find minimum
    // sum of absolute differences
    // of pairs in a triplet
    minimum_sum(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to find minimum
// sum of absolute differences
// of pairs of a triplet
static int minimum_sum(int []A, int N)
{

    // Sort the array
    Arrays.sort(A);

    // Stores the minimum sum

    int sum = 2147483647;

    // Traverse the array
    for (int i = 0; i <= N - 3; i++) {

        // Update the minimum sum
        sum = Math.min(sum,Math.abs(A[i] - A[i + 1]) + Math.abs(A[i + 1] - A[i + 2]));
    }

    // Print the minimum sum
    return sum;
}

// Driver Code
public static void main(String[] args)
{

    // Input
    int []A = { 1, 1, 2, 3 };
    int N = A.length;

    // Function call to find minimum
    // sum of absolute differences
    // of pairs in a triplet
    System.out.print(minimum_sum(A, N));
}
}

// This code is contributed by splevel62.
```

## 蟒蛇 3

```
# Python 3 Program for the above approach
import sys

# Function to find minimum
# sum of absolute differences
# of pairs of a triplet
def minimum_sum(A, N):

    # Sort the array
    A.sort(reverse = False)

    # Stores the minimum sum
    sum = sys.maxsize

    # Traverse the array
    for i in range(N - 2):

        # Update the minimum sum
        sum = min(sum, abs(A[i] - A[i + 1]) + abs(A[i + 1] - A[i + 2]))

    # Print the minimum sum
    print(sum)

# Driver Code
if __name__ == '__main__':

    # Input
    A = [1, 1, 2, 3]
    N = len(A)

    # Function call to find minimum
    # sum of absolute differences
    # of pairs in a triplet
    minimum_sum(A, N)

    # This code is contributed by ipg2016107
```

## C#

```
// C# Program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

// Function to find minimum
// sum of absolute differences
// of pairs of a triplet
static int minimum_sum(int []A, int N)
{

    // Sort the array
    Array.Sort(A);

    // Stores the minimum sum

    int sum = 2147483647;

    // Traverse the array
    for (int i = 0; i <= N - 3; i++) {

        // Update the minimum sum
        sum = Math.Min(sum,Math.Abs(A[i] - A[i + 1]) + Math.Abs(A[i + 1] - A[i + 2]));
    }

    // Print the minimum sum
    return sum;
}

// Driver Code
public static void Main()
{

    // Input
    int []A = { 1, 1, 2, 3 };
    int N = A.Length;

    // Function call to find minimum
    // sum of absolute differences
    // of pairs in a triplet
    Console.WriteLine(minimum_sum(A, N));
}
}

// This code is contributed by bgangwar59.
```

## java 描述语言

```
<script>

// Javascript Program for the above approach

// Function to find minimum
// sum of absolute differences
// of pairs of a triplet
function minimum_sum( A, N)
{
    // Sort the array
    A.sort();

    // Stores the minimum sum
    var sum = 1000000000;

    // Traverse the array
    for (var i = 0; i <= N - 3; i++) {

        // Update the minimum sum
        sum = Math.min(sum,
                  Math.abs(A[i] - A[i + 1]) +
                  Math.abs(A[i + 1] - A[i + 2]));
    }

    // Print the minimum sum
    document.write(sum);
}

// Driver Code
// Input
var A = [ 1, 1, 2, 3 ];
var N = A.length;
// Function call to find minimum
// sum of absolute differences
// of pairs in a triplet
minimum_sum(A, N);

</script>
```

**Output:** 

```
1
```

***时间复杂度** : O(N * logN)*
***辅助空间** : O(1)*