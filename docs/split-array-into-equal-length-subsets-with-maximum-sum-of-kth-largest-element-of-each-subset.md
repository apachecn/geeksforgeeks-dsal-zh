# 将数组拆分成长度相等的子集，每个子集的第 k 个最大元素之和最大

> 原文:[https://www . geeksforgeeks . org/将数组拆分为长度相等的子集，每个子集的最大元素总和为 kth/](https://www.geeksforgeeks.org/split-array-into-equal-length-subsets-with-maximum-sum-of-kth-largest-element-of-each-subset/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，两个正整数 **M** 和 **K** ，任务是将数组划分为 **M** 等长的[子集](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)，使得所有这些子集的 **K <sup>第</sup>** 个最大元素之和最大。如果无法将数组划分为 **M** 等长子集，则打印 **-1** 。

**示例:**

> **输入:** arr[] = { 1，2，3，4，5，6 }，M = 2，K = 2
> **输出:** 8
> **说明:**
> 每个子集的长度= (N / M) = 3。
> 数组中可能的子集有:{ {1，3，4}、{2，5，6} }
> 因此，每个子集的第 K 个<sup>最大元素之和= 3 + 5 = 8</sup>
> 
> **输入:** arr[] = {11，20，2，17}，M = 4，K = 1
> **输出:** 50

**方法:**使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。按照以下步骤解决问题:

*   如果 **N** 不能被 **M** 整除，则打印 **-1** 。
*   初始化一个变量，比如 **maxSum** ，通过将数组划分为 **M** 等长子集来存储数组所有子集的最大元素**K<sup>th</sup>T5 的最大可能和。**
*   [按降序排列数组](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)。
*   使用变量 **i** 迭代范围**【1，M】**，并更新**maxSum+= arr[I * K–1]。**
*   最后打印 **maxSum** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum of Kth
// largest element of M equal length partition
int maximumKthLargestsumPart(int arr[], int N,
                             int M, int K)
{
    // Stores sum of K_th largest element
    // of equal length partitions
    int maxSum = 0;

    // If N is not
    // divisible by M
    if (N % M)
        return -1;

    // Stores length of
    // each partition
    int sz = (N / M);

    // If K is greater than
    // length of partition
    if (K > sz)
        return -1;

    // Sort array in
    // descending porder
    sort(arr, arr + N, greater<int>());

    // Traverse the array
    for (int i = 1; i <= M;
         i++) {

        // Update maxSum
        maxSum
            += arr[i * K - 1];
    }

    return maxSum;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int M = 2;
    int K = 1;
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << maximumKthLargestsumPart(arr, N, M, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
import java.util.Collections;

class GFG{

// Function to find the maximum sum of Kth
// largest element of M equal length partition
static int maximumKthLargestsumPart(int[] arr, int N,
                                    int M, int K)
{

    // Stores sum of K_th largest element
    // of equal length partitions
    int maxSum = 0;

    // If N is not
    // divisible by M
    if (N % M != 0)
        return -1;

    // Stores length of
    // each partition
    int sz = (N / M);

    // If K is greater than
    // length of partition
    if (K > sz)
        return -1;

    // Sort array in
    // descending porder
    Arrays.sort(arr);
    int i, k, t;

    for(i = 0; i < N / 2; i++)
    {
        t = arr[i];
        arr[i] = arr[N - i - 1];
        arr[N - i - 1] = t;
    }

    // Traverse the array
    for(i = 1; i <= M; i++)
    {

        // Update maxSum
        maxSum += arr[i * K - 1];
    }
    return maxSum;
}

// Driver code
public static void main(String[] args)
{
    int[] arr = { 1, 2, 3, 4, 5, 6 };
    int M = 2;
    int K = 1;
    int N = arr.length;

    System.out.println(maximumKthLargestsumPart(
        arr, N, M, K));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the maximum sum of Kth
# largest element of M equal length partition
def maximumKthLargestsumPart(arr, N, M, K):

    # Stores sum of K_th largest element
    # of equal length partitions
    maxSum = 0

    # If N is not
    # divisible by M
    if (N % M != 0):
        return -1

    # Stores length of
    # each partition
    sz = (N / M)

    # If K is greater than
    # length of partition
    if (K > sz):
        return -1

    # Sort array in
    # descending porder
    arr = sorted(arr)

    for i in range(0, N // 2):
        t = arr[i]
        arr[i] = arr[N - i - 1]
        arr[N - i - 1] = t

    # Traverse the array
    for i in range(1, M + 1):

        # Update maxSum
        maxSum += arr[i * K - 1]

    return maxSum

# Driver code
if __name__ == '__main__':

    arr = [ 1, 2, 3, 4, 5, 6 ]
    M = 2
    K = 1
    N = len(arr)

    print(maximumKthLargestsumPart(arr, N, M, K))

# This code is contributed by Amit Katiyar
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to find the maximum sum of Kth
// largest element of M equal length partition
static int maximumKthLargestsumPart(int[] arr, int N,
                                    int M, int K)
{

    // Stores sum of K_th largest element
    // of equal length partitions
    int maxSum = 0;

    // If N is not
    // divisible by M
    if (N % M != 0)
        return -1;

    // Stores length of
    // each partition
    int sz = (N / M);

    // If K is greater than
    // length of partition
    if (K > sz)
        return -1;

    // Sort array in
    // descending porder
    Array.Sort(arr);
    Array.Reverse(arr);

    // Traverse the array
    for(int i = 1; i <= M; i++)
    {

        // Update maxSum
        maxSum += arr[i * K - 1];
    }
    return maxSum;
}

// Driver code   
static void Main()
{
    int[] arr = { 1, 2, 3, 4, 5, 6 };
    int M = 2;
    int K = 1;
    int N = arr.Length;

    Console.WriteLine(maximumKthLargestsumPart(
        arr, N, M, K));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach

// Function to find the maximum sum of Kth
// largest element of M equal length partition
function maximumKthLargestsumPart(arr, N,
                                    M, K)
{

    // Stores sum of K_th largest element
    // of equal length partitions
    let maxSum = 0;

    // If N is not
    // divisible by M
    if (N % M != 0)
        return -1;

    // Stores length of
    // each partition
    let sz = (N / M);

    // If K is greater than
    // length of partition
    if (K > sz)
        return -1;

    // Sort array in
    // descending porder
    arr.sort();
    let i, k, t;

    for(i = 0; i < N / 2; i++)
    {
        t = arr[i];
        arr[i] = arr[N - i - 1];
        arr[N - i - 1] = t;
    }

    // Traverse the array
    for(i = 1; i <= M; i++)
    {

        // Update maxSum
        maxSum += arr[i * K - 1];
    }
    return maxSum;
}

// Driver code

    let arr = [ 1, 2, 3, 4, 5, 6 ];
    let M = 2;
    let K = 1;
    let N = arr.length;

    document.write(maximumKthLargestsumPart(
        arr, N, M, K));

    // This code is contributed by splevel62.
</script>
```

**Output:** 

```
11
```

***时间复杂度:**O(N * log(N))*
T5**辅助空间:** O(1)