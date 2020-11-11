# 具有可被 K 整除的所有对的绝对差的最长子序列的长度

> 原文：[https://www.geeksforgeeks.org/length-of-longest-subsequence-having-absolute-difference-of-all-pairs-divisible-by-k/](https://www.geeksforgeeks.org/length-of-longest-subsequence-having-absolute-difference-of-all-pairs-divisible-by-k/)

给定[数组](https://www.geeksforgeeks.org/array-data-structure/)，`arr[]`的大小`N`和整数`K`，任务是[找到来自给定数组的最长子序列](https://www.geeksforgeeks.org/array-data-structure/)，使得子序列中每对的绝对差可被`K`整除。

**示例**：

> **输入**：`arr[] = {10, 12, 16, 20, 32, 15}, K = 4`
>
> **输出**：4
>
> **说明**：
>
> 最长子序列，其中每对可被`K = 4`整除的绝对差为`{12, 26, 20, 32}`。
>
> 因此，所需的输出是 4
> 
> **输入**：`arr[] = {12, 3, 13, 5, 21, 11}, K = 3`
>
> **输出**：3

**朴素的方法**：解决此问题的最简单方法是[生成给定数组的所有可能的子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)，并打印最长的子序列的长度，每对子序列的绝对差值可乘以`K`。

**时间复杂度**：`O(2 ^ N)`

**辅助空间**：`O(n)`

**高效方法**：为了优化上述方法，其思想是基于以下观察结果使用[散列](https://www.geeksforgeeks.org/hashing-data-structure/)：

> 必须将`arr[i] % K`的值相等的子集的所有可能对的绝对差值除以 K。
> 
> **数学证明**：
>
> 如果`arr[i] % K = arr[j] % K`
>
> `abs(arr[i] – arr[j]) % K`必须为 0。

请按照以下步骤解决问题：

*   初始化一个数组，例如说`hash[K]`，以存储`arr[i] % K`的频率。

*   [遍历`hash[]`数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[在`hash[]`数组中找到最大元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)。

*   最后，打印`hash[]`数组的最大元素。

下面是上述方法的实现：

## C++ 14

```

// C++14 program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the length
// of subsequence that satisfy
// the given condition
int maxLenSub(int arr[],
              int N, int K)
{
    // Store the frequencies
    // of arr[i] % K
    int hash[K];

    // Initilize hash[] array
    memset(hash, 0, sizeof(hash));

    // Traverse the given array
    for (int i = 0; i < N; i++) {

        // Update frequency of
        // arr[i] % K
        hash[arr[i] % K]++;
    }

    // Stores the length of
    // the longest subsequence that
    // satisfy the given condition
    int LenSub = 0;

    // Find the maximum element
    // in hash[] array
    for (int i = 0; i < K; i++) {
        LenSub = max(LenSub, hash[i]);
    }
}

// Driver Code
int main()
{
    int arr[] = { 12, 3, 13, 5, 21, 11 };
    int K = 3;
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << maxLenSub(arr, N, K);
}

```

## Java

```java

// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Function to find the length
// of subsequence that satisfy
// the given condition
static int maxLenSub(int arr[],
                     int N, int K)
{
  // Store the frequencies
  // of arr[i] % K
  int []hash = new int[K];

  // Traverse the given array
  for (int i = 0; i < N; i++) 
  {
    // Update frequency of
    // arr[i] % K
    hash[arr[i] % K]++;
  }

  // Stores the length of
  // the longest subsequence that
  // satisfy the given condition
  int LenSub = 0;

  // Find the maximum element
  // in hash[] array
  for (int i = 0; i < K; i++) 
  {
    LenSub = Math.max(LenSub, 
                      hash[i]);
  }

  return LenSub;
}

// Driver Code
public static void main(String[] args)
{
  int arr[] = {12, 3, 13, 5, 21, 11};
  int K = 3;
  int N = arr.length;
  System.out.print(maxLenSub(arr, N, K));
}
}

// This code is contributed by Rajput-Ji

```

## Python3

```py

# Python3 program to implement
# the above approach

# Function to find the length
# of subsequence that satisfy
# the given condition
def maxLenSub(arr, N, K):

    # Store the frequencies
    # of arr[i] % K
    hash = [0] * K

    # Traverse the given array
    for i in range(N):

        # Update frequency of
        # arr[i] % K
        hash[arr[i] % K] += 1

    # Stores the length of the
    # longest subsequence that
    # satisfy the given condition
    LenSub = 0

    # Find the maximum element
    # in hash[] array
    for i in range(K):
        LenSub = max(LenSub, hash[i])

    return LenSub    

# Driver Code
if __name__ == '__main__':

    arr = [ 12, 3, 13, 5, 21, 11 ]
    K = 3
    N = len(arr)

    print(maxLenSub(arr, N, K))

# This code is contributed by mohit kumar 29

```

## C#

```cs

// C# program to implement
// the above approach
using System;
class GFG{

// Function to find the length
// of subsequence that satisfy
// the given condition
static int maxLenSub(int []arr,
                     int N, int K)
{
  // Store the frequencies
  // of arr[i] % K
  int []hash = new int[K];

  // Traverse the given array
  for (int i = 0; i < N; i++) 
  {
    // Update frequency of
    // arr[i] % K
    hash[arr[i] % K]++;
  }

  // Stores the length of
  // the longest subsequence that
  // satisfy the given condition
  int LenSub = 0;

  // Find the maximum element
  // in hash[] array
  for (int i = 0; i < K; i++) 
  {
    LenSub = Math.Max(LenSub, 
                      hash[i]);
  }

  return LenSub;
}

// Driver Code
public static void Main(String[] args)
{
  int []arr = {12, 3, 13, 
               5, 21, 11};
  int K = 3;
  int N = arr.Length;
  Console.Write(maxLenSub(arr, N, K));
}
}

// This code is contributed by Amit Katiyar

```

**输出**：

```
3
```

**时间复杂度**：`O(n)`

**辅助空间**：`O(K)`



* * *

* * *



