# 计数超过前 K 个元素之和的数组元素

> 原文:[https://www . geeksforgeeks . org/count-array-elements-over-sum-before-k-elements/](https://www.geeksforgeeks.org/count-array-elements-exceeding-sum-of-preceding-k-elements/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，以及一个整数 **K** ，任务是找出大于**(arr[I–1]+arr[I–2]+…+arr[I–K])**的数组元素 **arr[i]** 的个数。

**示例:**

> **输入:** arr[] = {2，3，8，10，-2，7，5，5，9，15}，K = 2
> **输出:** 2
> **解释:**
> arr[2](>arr[1]+arr[0])和 arr[9]( > arr[8] + arr[7])是超过前面 K(= 2)个元素之和的两个数组元素。
> 
> **输入:** arr[] = {17，-2，16，-8，19，11，5，15，-9，24}，K = 3
> **输出:** 2

**方法:**按照以下步骤解决问题:

1.  计算并存储给定数组的 [**前缀和**](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/) 。
2.  [遍历索引**【K，N-1】**中的数组元素](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。
3.  对于每个数组元素，检查 **arr[i]** 是否超过**(arr[I–1]+arr[I–2]+…+arr[I–K])**。因此，任务是检查 **arr[i]** 是否超过**前缀【I–1】–前缀【I –( K+1)】**对于 **K > i > N** 或者 **arr[i]** 是否超过**前缀【I–1】**对于 **i = K** 。
4.  对满足上述条件的数组元素增加**计数**。最后，打印所需的**计数**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count array elements
// exceeding sum of preceding K elements
int countPrecedingK(int a[], int n, int K)
{
    int prefix[n];
    prefix[0] = a[0];

    // Iterate over the array
    for (int i = 1; i < n; i++) {

        // Update prefix sum
        prefix[i]
            = prefix[i - 1] + a[i];
    }

    int ctr = 0;

    // Check if arr[K] >
    // arr[0] + .. + arr[K - 1]
    if (prefix[K - 1] < a[K])

        // Increment count
        ctr++;

    for (int i = K + 1; i < n; i++) {
        // Check if arr[i] >
        // arr[i - K - 1] + .. + arr[i - 1]
        if (prefix[i - 1] - prefix[i - K - 1]
            < a[i])

            // Increment count
            ctr++;
    }

    return ctr;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 2, 3, 8, 10, -2,
                  7, 5, 5, 9, 15 };

    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 2;

    cout << countPrecedingK(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to count array elements
// exceeding sum of preceding K elements
static int countPrecedingK(int a[], int n,
                           int K)
{
    int []prefix = new int[n];
    prefix[0] = a[0];

    // Iterate over the array
    for(int i = 1; i < n; i++)
    {

        // Update prefix sum
        prefix[i] = prefix[i - 1] + a[i];
    }

    int ctr = 0;

    // Check if arr[K] >
    // arr[0] + .. + arr[K - 1]
    if (prefix[K - 1] < a[K])

        // Increment count
        ctr++;

    for(int i = K + 1; i < n; i++)
    {

        // Check if arr[i] >
        // arr[i - K - 1] + .. + arr[i - 1]
        if (prefix[i - 1] -
            prefix[i - K - 1] < a[i])

            // Increment count
            ctr++;
    }
    return ctr;
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 2, 3, 8, 10, -2,
                  7, 5, 5, 9, 15 };

    int N = arr.length;
    int K = 2;

    System.out.print(countPrecedingK(arr, N, K));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count array elements
# exceeding sum of preceding K elements
def countPrecedingK(a, n, K):

    prefix = [0] * n
    prefix[0] = a[0]

    # Iterate over the array
    for i in range(1, n):

        # Update prefix sum
        prefix[i] = prefix[i - 1] + a[i]

    ctr = 0

    # Check if arr[K] >
    # arr[0] + .. + arr[K - 1]
    if (prefix[K - 1] < a[K]):

        # Increment count
        ctr += 1

    for i in range(K + 1, n):

        # Check if arr[i] >
        # arr[i - K - 1] + .. + arr[i - 1]
        if (prefix[i - 1] -
            prefix[i - K - 1] < a[i]):

            # Increment count
            ctr += 1

    return ctr

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [ 2, 3, 8, 10, -2,
            7, 5, 5, 9, 15 ]

    N = len(arr)
    K = 2

    print(countPrecedingK(arr, N, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function to count array elements
// exceeding sum of preceding K elements
static int countPrecedingK(int []a,
                           int n, int K)
{
  int []prefix = new int[n];
  prefix[0] = a[0];

  // Iterate over the array
  for(int i = 1; i < n; i++)
  {
    // Update prefix sum
    prefix[i] = prefix[i - 1] + a[i];
  }

  int ctr = 0;

  // Check if arr[K] >
  // arr[0] + .. + arr[K - 1]
  if (prefix[K - 1] < a[K])

    // Increment count
    ctr++;

  for(int i = K + 1; i < n; i++)
  {
    // Check if arr[i] >
    // arr[i - K - 1] + .. + arr[i - 1]
    if (prefix[i - 1] -
        prefix[i - K - 1] < a[i])

      // Increment count
      ctr++;
  }
  return ctr;
}

// Driver Code
public static void Main(String[] args)
{
  // Given array
  int []arr = {2, 3, 8, 10, -2,
               7, 5, 5, 9, 15};

  int N = arr.Length;
  int K = 2;

  Console.Write(countPrecedingK(arr, N, K));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to count array elements
// exceeding sum of preceding K elements
function countPrecedingK(a, n, K)
{
    let prefix = new Array(n).fill(0);
    prefix[0] = a[0];

    // Iterate over the array
    for(let i = 1; i < n; i++)
    {

        // Update prefix sum
        prefix[i] = prefix[i - 1] + a[i];
    }

    let ctr = 0;

    // Check if arr[K] >
    // arr[0] + .. + arr[K - 1]
    if (prefix[K - 1] < a[K])

        // Increment count
        ctr++;

    for(let i = K + 1; i < n; i++)
    {

        // Check if arr[i] >
        // arr[i - K - 1] + .. + arr[i - 1]
        if (prefix[i - 1] -
            prefix[i - K - 1] < a[i])

            // Increment count
            ctr++;
    }
    return ctr;
}

// Driver Code

     // Given array
    let arr = [ 2, 3, 8, 10, -2,
                  7, 5, 5, 9, 15 ];

    let N = arr.length;
    let K = 2;

    document.write(countPrecedingK(arr, N, K));

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)