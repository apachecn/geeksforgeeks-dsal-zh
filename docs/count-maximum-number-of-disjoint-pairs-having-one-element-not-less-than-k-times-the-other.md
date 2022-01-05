# 计算一个元素不小于另一个元素的 K 倍的不相交对的最大数量

> 原文:[https://www . geeksforgeeks . org/count-最大不相交对数-有一个元素-不少于 k 倍-其他/](https://www.geeksforgeeks.org/count-maximum-number-of-disjoint-pairs-having-one-element-not-less-than-k-times-the-other/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 和一个正整数 **K** ，任务是找到不相交对的最大计数 **(arr[i]，arr[j])** ，使得 **arr[j] ≥ K * arr[i]** 。

**示例:**

> **输入:** arr[] = { 1，9，4，7，3 }，K = 2
> **输出:** 2
> **解释:**
> 可以从给定数组中形成 2 个可能的对，即满足给定条件的(4，1)和(7，3)。
> 
> **输入:** arr[] = {2，3，4，5，6，7，8，9}，K = 3
> **输出:** 2

**方法:**给定的问题可以通过使用[双指针方法](https://www.geeksforgeeks.org/two-pointers-technique/)来解决。按照以下步骤解决给定的问题:

1.  [给定数组按递增顺序排序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
2.  将两个变量 **i** 和 **j** 分别初始化为 **0** 和 **(N / 2)** ，并将变量**计数**存储成对结果的最大计数。
3.  [在范围**【0，N/2】**内遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并执行以下步骤:
    *   增加 **j** 的值，直到 **j < N** 和**arr【j】<K * arr【I】**。
    *   如果 **j** 的值小于 **N** ，则通过 **1** 增加对的计数。
    *   将 **j** 的值增加 **1** 。
4.  完成上述步骤后，打印**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum count
// of disjoint pairs such that arr[i]
// is at least K*arr[j]
int maximizePairs(int arr[], int n, int k)
{
    // Sort the array
    sort(arr, arr + n);

    // Initialize the two pointers
    int i = 0, j = n / 2;

    // Stores the total count of pairs
    int count = 0;

    for (i = 0; i < n / 2; i++) {

        // Increment j until a valid
        // pair is found or end of the
        // array is reached
        while (j < n
               && (k * arr[i]) > arr[j])
            j++;

        // If j is not the end of the
        // array, then a valid pair
        if (j < n)
            count++;

        j++;
    }

    // Return the possible count
    return count;
}

// Driver Code
int main()
{
    int arr[] = { 1, 9, 4, 7, 3 };
    int N = sizeof(arr) / sizeof(int);
    int K = 2;
    cout << maximizePairs(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for above approach
import java.util.*;

class GFG{

// Function to find the maximum count
// of disjoint pairs such that arr[i]
// is at least K*arr[j]
static int maximizePairs(int arr[], int n, int k)
{
    // Sort the array
    Arrays.sort(arr);

    // Initialize the two pointers
    int i = 0, j = n / 2;

    // Stores the total count of pairs
    int count = 0;

    for (i = 0; i < n / 2; i++) {

        // Increment j until a valid
        // pair is found or end of the
        // array is reached
        while (j < n
               && (k * arr[i]) > arr[j])
            j++;

        // If j is not the end of the
        // array, then a valid pair
        if (j < n)
            count++;

        j++;
    }

    // Return the possible count
    return count;
}

// Driver Code
public static void main(String[] args)

{
    int arr[] = { 1, 9, 4, 7, 3 };
    int N = arr.length;
    int K = 2;
    System.out.print(maximizePairs(arr, N, K));
}
}

// This code is contributed by avijitmondal1998.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the maximum count
# of disjoint pairs such that arr[i]
# is at least K*arr[j]
def maximizePairs(arr, n, k):

    # Sort the array
    arr.sort()

    # Initialize the two pointers
    i = 0
    j = n // 2

    # Stores the total count of pairs
    count = 0

    for i in range(n//2):

        # Increment j until a valid
        # pair is found or end of the
        # array is reached
        while (j < n and (k * arr[i]) > arr[j]):
            j += 1

        # If j is not the end of the
        # array, then a valid pair
        if (j < n):
            count += 1

        j += 1

    # Return the possible count
    return count

# Driver Code
if __name__ == '__main__':
    arr = [1, 9, 4, 7, 3]
    N = len(arr)
    K = 2
    print(maximizePairs(arr, N, K))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# code for above approach
using System;

class GFG{

// Function to find the maximum count
// of disjoint pairs such that arr[i]
// is at least K*arr[j]
static int maximizePairs(int []arr, int n, int k)
{
    // Sort the array
    Array.Sort(arr);

    // Initialize the two pointers
    int i = 0, j = n / 2;

    // Stores the total count of pairs
    int count = 0;

    for (i = 0; i < n / 2; i++) {

        // Increment j until a valid
        // pair is found or end of the
        // array is reached
        while (j < n
               && (k * arr[i]) > arr[j])
            j++;

        // If j is not the end of the
        // array, then a valid pair
        if (j < n)
            count++;

        j++;
    }

    // Return the possible count
    return count;
}

// Driver Code
public static void Main(String[] args)

{
    int []arr = { 1, 9, 4, 7, 3 };
    int N = arr.Length;
    int K = 2;
    Console.Write(maximizePairs(arr, N, K));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the maximum count
// of disjoint pairs such that arr[i]
// is at least K*arr[j]
function maximizePairs(arr, n, k) {
  // Sort the array
  arr.sort((a, b) => a - b);

  // Initialize the two pointers
  let i = 0,
    j = Math.floor(n / 2);

  // Stores the total count of pairs
  let count = 0;

  for (i = 0; i < Math.floor(n / 2); i++) {
    // Increment j until a valid
    // pair is found or end of the
    // array is reached
    while (j < n && k * arr[i] > arr[j]) j++;

    // If j is not the end of the
    // array, then a valid pair
    if (j < n) count++;

    j++;
  }

  // Return the possible count
  return count;
}

// Driver Code

let arr = [1, 9, 4, 7, 3];
let N = arr.length;
let K = 2;
document.write(maximizePairs(arr, N, K));

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
2
```

**时间复杂度:***O(N * log N)*
T5】辅助空间: *O(N)*