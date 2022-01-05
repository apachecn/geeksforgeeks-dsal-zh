# 从给定的 N 个点到所有其他点的距离总和最小的点找到 X 轴上的点

> 原文:[https://www . geeksforgeeks . org/从给定的 n 个点中找到 x 轴上的点，这些点与所有其他点的距离总和最小/](https://www.geeksforgeeks.org/find-the-point-on-x-axis-from-given-n-points-having-least-sum-of-distances-from-all-other-points/)

给定一个由 **N** 整数组成的数组**arr【】**，表示位于 **X 轴**上的 **N** 点，任务是找到与所有其他点的距离之和**最小的点。**

**示例:**

> **输入:** arr[] = {4，1，5，10，2}
> **输出:** (4， 0)
> **说明:**
> 4 与其余元素的距离= | 4–1 |+| 4–5 |+| 4–10 |+| 4–2 | = 12**1**与其余元素的距离= | 1–4 |+| 1–5 |+| 1–10 |+| 1–2 | = 17
> 5 与其余元素的距离 +| 5–4 |+| 5–2 |+| 5–10 | = 13
> 10 与其余元素的距离= | 10–1 |+| 10–2 |+| 10–5 |+| 10–4 | = 28**2**与其余元素的距离= | 2–1 |+| 2–4 |+| 2–5 |+| 2–10 | = 14
> T22

**天真方法:**
任务是迭代数组，对于每个数组元素，计算其与所有其他数组元素的绝对差之和。最后，打印差异总和最大的数组元素。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效途径:**优化上述途径，思路是找到数组的[中值](https://www.geeksforgeeks.org/median/)。数组的中值与数组中其他元素的总距离最小。对于具有偶数个元素的数组，有两个可能的中间值，两个中间值的总距离相同，返回索引较低的中间值，因为它更接近原点。

按照以下步骤解决问题:

*   给定数组排序。
*   如果 **N** 为**奇数**，则返回 **(N + 1 / 2) <sup>第</sup>** 元素。
*   否则，返回 **(N / 2) <sup>第</sup>个**元素。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find median of the array
int findLeastDist(int A[], int N)
{
    // Sort the given array
    sort(A, A + N);

    // If number of elements are even
    if (N % 2 == 0) {

        // Return the first median
        return A[(N - 1) / 2];
    }

    // Otherwise
    else {
        return A[N / 2];
    }
}

// Driver Code
int main()
{

    int A[] = { 4, 1, 5, 10, 2 };
    int N = sizeof(A) / sizeof(A[0]);
    cout << "(" << findLeastDist(A, N)
         << ", " << 0 << ")";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find median of the array
static int findLeastDist(int A[], int N)
{

    // Sort the given array
    Arrays.sort(A);

    // If number of elements are even
    if (N % 2 == 0)
    {

        // Return the first median
        return A[(N - 1) / 2];
    }

    // Otherwise
    else
    {
        return A[N / 2];
    }
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 4, 1, 5, 10, 2 };
    int N = A.length;

    System.out.print("(" + findLeastDist(A, N) +
                    ", " + 0 + ")");
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find median of the array
def findLeastDist(A, N):

    # Sort the given array
    A.sort();

    # If number of elements are even
    if (N % 2 == 0):

        # Return the first median
        return A[(N - 1) // 2];

    # Otherwise
    else:
        return A[N // 2];

# Driver Code
A = [4, 1, 5, 10, 2];
N = len(A);

print("(" , findLeastDist(A, N),
      ", " , 0 , ")");

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to find median of the array
static int findLeastDist(int []A, int N)
{

    // Sort the given array
    Array.Sort(A);

    // If number of elements are even
    if (N % 2 == 0)
    {

        // Return the first median
        return A[(N - 1) / 2];
    }

    // Otherwise
    else
    {
        return A[N / 2];
    }
}

// Driver Code
public static void Main(string[] args)
{
    int []A = { 4, 1, 5, 10, 2 };
    int N = A.Length;

    Console.Write("(" + findLeastDist(A, N) +
                 ", " + 0 + ")");
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

// Function to find median of the array
function findLeastDist(A, N)
{
    // Sort the given array
    A.sort((a,b) => a-b);

    console.log(A);

    // If number of elements are even
    if ((N % 2) == 0) {

        // Return the first median
        return A[parseInt((N - 1) / 2)];
    }

    // Otherwise
    else {
        return A[parseInt(N / 2)];
    }
}

// Driver Code
var A = [ 4, 1, 5, 10, 2 ];
var N = A.length;
document.write( "(" + findLeastDist(A, N)
     + ", " + 0 + ")");

</script>
```

**Output:** 

```
(4, 0)
```

***时间复杂度:** O(Nlog(N))*
***辅助空间:** O(1)*