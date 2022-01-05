# 找到循环数组中前缀和总是非负的索引

> 原文:[https://www . geeksforgeeks . org/find-the-index-in-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a](https://www.geeksforgeeks.org/find-the-index-in-a-circular-array-from-which-prefix-sum-is-always-non-negative/)

给定一个由 **N** 个整数组成的[圆形数组](https://www.geeksforgeeks.org/circular-array/) **arr[]** ，任务是找到圆形数组的起始索引，使得来自该索引的[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)总是非负的。如果没有这样的索引，则打印**-1”**。

**示例:**

> **输入:** arr[] = {3，-6，7，-1，-4，5，-1}
> **输出:** 2
> **解释:**
> 考虑计算给定循环数组前缀和的索引 2，然后前缀和由{9，3，7，6，2，7，6}给出
> 
> **输入:** arr[] = {3，-5，-1}
> **输出:** -1

**方法:**给定的问题可以基于以下观察来解决:

*   如果数组元素的[和为负，则不存在从该点开始前缀和为非负的索引。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
*   否则，该索引是在具有[最小前缀和](https://www.geeksforgeeks.org/minimum-value-to-be-added-to-the-prefix-sums-at-each-array-indices-to-make-them-positive/)的索引之后的索引。

按照以下步骤解决问题:

*   初始化一个变量，比如说 **sum** 为 **0** ，存储数组元素的 [sum。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
*   初始化一个变量，比如说中的**为 **0** ，存储循环遍历的起始索引。**
*   初始化一个变量，说 **min** 为 [**INT_MAX**](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) ，存储数组的最小前缀和 **arr[]** 。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并执行以下步骤:
    *   将**总和**的值更新为**总和**和当前元素**arr【I】**的总和。
    *   如果**和**的值小于**分**，则将**分**更新为**和**，中的**为 **(i + 1)** 。**
*   如果数组的[和为负，则打印 **-1** 。否则，打印**(单位为% N)** 的值作为最终可能的索引。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the starting index
// of the given circular array s.t.
// prefix sum array is non negative
int startingPoint(int A[], int N)
{
    // Stores the sum of the array
    int sum = 0;

    // Stores the starting index
    int in = 0;

    // Stores the minimum prefix
    // sum of A[0..i]
    int min = INT_MAX;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // Update the value of sum
        sum += A[i];

        // If sum is less than min
        if (sum < min) {

            // Update the min as the
            // value of prefix sum
            min = sum;

            // Update in
            in = i + 1;
        }
    }

    // Otherwise, no such index is
    // possible
    if (sum < 0) {
        return -1;
    }

    return in % N;
}

// Driver Code
int main()
{
    int arr[] = { 3, -6, 7, -4, -4, 6, -1 };
    int N = (sizeof(arr) / sizeof(arr[0]));
    cout << startingPoint(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to find the starting index
// of the given circular array s.t.
// prefix sum array is non negative
static int startingPoint(int A[], int N)
{

    // Stores the sum of the array
    int sum = 0;

    // Stores the starting index
    int in = 0;

    // Stores the minimum prefix
    // sum of A[0..i]
    int min = Integer.MAX_VALUE;

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // Update the value of sum
        sum += A[i];

        // If sum is less than min
        if (sum < min)
        {

            // Update the min as the
            // value of prefix sum
            min = sum;

            // Update in
            in = i + 1;
        }
    }

    // Otherwise, no such index is
    // possible
    if (sum < 0)
    {
        return -1;
    }

    return in % N;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 3, -6, 7, -4, -4, 6, -1 };
    int N = arr.length;

    System.out.print(startingPoint(arr, N));
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the starting index
# of the given circular array
# prefix sum array is non negative
import sys

def startingPoint(A, N):

    # Stores the sum of the array
    sum = 0

    # Stores the starting index
    startingindex = 0

    # Stores the minimum prefix
    # sum of A[0..i]
    min = sys.maxsize

    # Traverse the array
    for i in range(0, N):

        # Update the value of sum
        sum += A[i]

        # If sum is less than minimum
        if (sum < min):

            # Update the min as
            # the value of prefix sum
            min = sum

            # Update starting index
            startingindex = i + 1

    # Otherwise no such index is possible
    if (sum < 0):
        return -1

    return startingindex % N

# Driver code
arr = [ 3, -6, 7, -4, -4, 6, -1 ]
N = len(arr)

print(startingPoint(arr,N))

# This code is contributed by Virusbuddah
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the starting index
// of the given circular array s.t.
// prefix sum array is non negative
static int startingPoint(int[] A, int N)
{

    // Stores the sum of the array
    int sum = 0;

    // Stores the starting index
    int ind = 0;

    // Stores the minimum prefix
    // sum of A[0..i]
    int min = Int32.MaxValue;

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // Update the value of sum
        sum += A[i];

        // If sum is less than min
        if (sum < min)
        {

            // Update the min as the
            // value of prefix sum
            min = sum;

            // Update in
            ind = i + 1;
        }
    }

    // Otherwise, no such index is
    // possible
    if (sum < 0)
    {
        return -1;
    }

    return ind % N;
}

// Driver Code
public static void Main()
{
    int[] arr = { 3, -6, 7, -4, -4, 6, -1 };
    int N = arr.Length;

    Console.Write(startingPoint(arr, N));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>
// javascript program for the above approach
    // Function to find the starting index
    // of the given circular array s.t.
    // prefix sum array is non negative
    function startingPoint(A , N) {

        // Stores the sum of the array
        var sum = 0;

        // Stores the starting index
        var it = 0;

        // Stores the minimum prefix
        // sum of A[0..i]
        var min = Number.MAX_VALUE;

        // Traverse the array arr
        for (i = 0; i < N; i++) {

            // Update the value of sum
            sum += A[i];

            // If sum is less than min
            if (sum < min) {

                // Update the min as the
                // value of prefix sum
                min = sum;

                // Update in
                it = i + 1;
            }
        }

        // Otherwise, no such index is
        // possible
        if (sum < 0) {
            return -1;
        }

        return it % N;
    }

    // Driver Code

        var arr = [ 3, -6, 7, -4, -4, 6, -1 ];
        var N = arr.length;

        document.write(startingPoint(arr, N));

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*