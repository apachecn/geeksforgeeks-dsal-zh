# 检查一个阵列是否可以拆分成 GCD 超过 K 的子阵列

> 原文:[https://www . geesforgeks . org/check-if-a-array-can-split-in-subarray-gcd-exclusive-k/](https://www.geeksforgeeks.org/check-if-an-array-can-be-split-into-subarrays-with-gcd-exceeding-k/)

给定一个由 **N** 个整数和一个正整数 **K** 组成的数组**arr【】**，任务是检查是否有可能将这个数组拆分成不同的连续子数组，使得每个子数组的所有元素的[最大公约数](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)大于 **K** 。

***注:**每个阵元恰好可以是一个子阵的一部分。*

**示例:**

> **输入:** arr[] = {3，2，4，4，8}，K = 1
> **输出:**是
> **解释:**
> 一个有效的拆分分别是【3】、【2，4】、【4，8】带有 GCD 3，2 和 4。
> 另一个有效拆分是分别带有 GCD 3、2、4 和 8 的[3]、[2、4]、[4]、[8]。
> 因此，给定的阵列可以分成具有 GCD > K 的子阵列
> 
> **输入:** arr[] = {2，4，6，1，8，16}，K = 3
> T3】输出:否

**方法:**这个问题可以通过以下观察来解决:

*   如果发现任何数组元素**小于或等于 K** ，那么答案总是“否”。这是因为包含此数字的子阵列的 GCD 将始终小于或等于 **K** 。
*   如果没有发现任何阵列元素小于或等于 **K** ，那么总是有可能将整个阵列分成 **N** 子阵列，每个子阵列的大小至少为 **1** ，其 GCD 总是大于 **K** 。

因此，从上面的观察来看，想法是[遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，检查数组中是否存在小于或等于 **K** 的元素。如果发现属实，则打印**“否”**。否则打印**“是”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to check if it is possible
// to split an array into subarrays
// having GCD at least K
string canSplitArray(int arr[], int n,
                     int k)
{

    // Iterate over the array arr[]
    for (int i = 0; i < n; i++) {

        // If the current element
        // is less than or equal to k
        if (arr[i] <= k) {
            return "No";
        }
    }

    // If no array element is found
    // to be less than or equal to k
    return "Yes";
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 2, 4, 6, 1, 8, 16 };

    int N = sizeof arr / sizeof arr[0];

    // Given K
    int K = 3;

    // Function Call
    cout << canSplitArray(arr, N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to check if it is possible
// to split an array into subarrays
// having GCD at least K
static String canSplitArray(int arr[],
                            int n, int k)
{

    // Iterate over the array arr[]
    for(int i = 0; i < n; i++)
    {

        // If the current element
        // is less than or equal to k
        if (arr[i] <= k)
        {
            return "No";
        }
    }

    // If no array element is found
    // to be less than or equal to k
    return "Yes";
}

// Driver code
public static void main (String[] args)
{

    // Given array arr[]
    int arr[] = { 2, 4, 6, 1, 8, 16 };

    // Length of the array
    int N = arr.length;

    // Given K
    int K = 3;

    // Function call
    System.out.println(canSplitArray(arr, N, K));
}
}

// This code is contributed by jana_sayantan
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if it is possible
# to split an array into subarrays
# having GCD at least K
def canSplitArray(arr, n, k):

    # Iterate over the array arr[]
    for i in range(n):

        # If the current element
        # is less than or equal to k
        if (arr[i] <= k):
            return "No"

    # If no array element is found
    # to be less than or equal to k
    return "Yes"

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 2, 4, 6, 1, 8, 16 ]

    N = len(arr)

    # Given K
    K = 3

    # Function call
    print(canSplitArray(arr, N, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if it is possible
// to split an array into subarrays
// having GCD at least K
static String canSplitArray(int []arr,
                            int n, int k)
{

    // Iterate over the array []arr
    for(int i = 0; i < n; i++)
    {

        // If the current element
        // is less than or equal to k
        if (arr[i] <= k)
        {
            return "No";
        }
    }

    // If no array element is found
    // to be less than or equal to k
    return "Yes";
}

// Driver code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = { 2, 4, 6, 1, 8, 16 };

    // Length of the array
    int N = arr.Length;

    // Given K
    int K = 3;

    // Function call
    Console.WriteLine(canSplitArray(arr, N, K));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function to check if it is possible
// to split an array into subarrays
// having GCD at least K
function canSplitArray(arr, n, k)
{

    // Iterate over the array arr[]
    for(let i = 0; i < n; i++)
    {

        // If the current element
        // is less than or equal to k
        if (arr[i] <= k)
        {
            return "No";
        }
    }

    // If no array element is found
    // to be less than or equal to k
    return "Yes";
}

// Driver code

    // Given array arr[]
    let arr = [ 2, 4, 6, 1, 8, 16 ];

    // Length of the array
    let N = arr.length;

    // Given K
    let K = 3;

    // Function call
    document.write(canSplitArray(arr, N, K));

    // This code is contributed by code_hunt.
</script>
```

**Output:** 

```
No
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)