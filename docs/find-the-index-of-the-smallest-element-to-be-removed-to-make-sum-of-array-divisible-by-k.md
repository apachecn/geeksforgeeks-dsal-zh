# 求要去掉的最小元素的索引，使数组的和能被 K 整除

> 原文:[https://www . geesforgeks . org/find-要移除的最小元素的索引-使数组之和可被 k 整除/](https://www.geeksforgeeks.org/find-the-index-of-the-smallest-element-to-be-removed-to-make-sum-of-array-divisible-by-k/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个正整数 **K** ，任务是找到需要移除的最小数组元素的索引，使剩余数组的和可被 **K** 整除。如果存在多个解决方案，则打印最小的索引。否则，打印 **-1** 。

**示例:**

> **输入:** arr[ ] = {6，7，5，1}，K = 7
> **输出:** 2
> **解释:**
> 从 arr[ ]中移除 arr[0]将 arr[]修改为{ 7，5，1 }。因此，sum = 13
> 从 arr[]中移除 arr[1]会将 arr[]修改为{ 6，5，1 }。因此，sum = 12
> 从 arr[]中移除 arr[2]会将 arr[]修改为{ 6，7，1 }。因此，sum = 14
> 由于 sum (= 14)可被 K(= 7)整除，所以需要的输出是索引 2。
> 
> **输入:** arr[ ] = {14，7，8，2，4}，K = 7
> T3】输出: 1

**天真法:**解决这个问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并通过从数组中移除当前元素来计算和。如果得到的和可被 **K** 整除，则打印当前指数。否则，将移除的元素插入数组。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**方法:**通过预先计算数组的[和，可以优化上述方法。最后，遍历数组，检查**(sum–arr[I])**是否能被 **K** 整除。如果发现为真，则打印当前索引。按照以下步骤解决问题:](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

*   计算数组的[和，并将其存储在一个变量中，比如**和。**](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
*   初始化两个变量，比如说 **res** 和 **mini** 来存储最小元素和元素的索引，这样去掉元素使得总和可以被 **K** 整除。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，检查**(sum–arr[I])**是否可以被 **K** 整除。如果发现为真，则检查 **arr[i]** 是否小于 **mini** 。如果发现为真，则更新 **mini = arr[i]** 和 **res = i** 。
*   最后，打印 **res** 。

下面是上述方法的实现:

## C++14

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find index of the smallest array element
// required to be removed to make sum divisible by K
int findIndex(int arr[], int n, int K)
{

    // Stores sum of array elements
    int sum = 0;

    // Stores index of the smallest element
    // removed from the array to make sum
    // divisible by K
    int res = -1;

    // Stores the smallest element removed
    // from the array to make sum divisible by K
    int mini = 1e9;

    // Traverse the array, arr[]
    for (int i = 0; i < n; i++) {

        // Update sum
        sum += arr[i];
    }

    // Traverse the array arr[]
    for (int i = 0; i < n; i++) {

        // Calculate remaining sum
        int temp = sum - arr[i];

        // If sum is divisible by K
        if (temp % K == 0) {

            // If res ==-1 or mini is greater
            // than arr[i]
            if (res == -1 || mini > arr[i]) {

                // Update res and mini
                res = i + 1;
                mini = arr[i];
            }
        }
    }

    return res;
}

// Driver Code
int main()
{
    int arr[] = { 14, 7, 8, 2, 4 };
    int K = 7;
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << findIndex(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{

// Function to find index of the smallest array element
// required to be removed to make sum divisible by K
static int findIndex(int arr[], int n, int K)
{

    // Stores sum of array elements
    int sum = 0;

    // Stores index of the smallest element
    // removed from the array to make sum
    // divisible by K
    int res = -1;

    // Stores the smallest element removed
    // from the array to make sum divisible by K
    int mini = (int) 1e9;

    // Traverse the array, arr[]
    for (int i = 0; i < n; i++)
    {

        // Update sum
        sum += arr[i];
    }

    // Traverse the array arr[]
    for (int i = 0; i < n; i++)
    {

        // Calculate remaining sum
        int temp = sum - arr[i];

        // If sum is divisible by K
        if (temp % K == 0)
        {

            // If res ==-1 or mini is greater
            // than arr[i]
            if (res == -1 || mini > arr[i])
            {

                // Update res and mini
                res = i + 1;
                mini = arr[i];
            }
        }
    }
    return res;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 14, 7, 8, 2, 4 };
    int K = 7;
    int N = arr.length;
    System.out.print(findIndex(arr, N, K));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find index of the smallest array element
# required to be removed to make sum divisible by K
def findIndex(arr, n, K) :

    # Stores sum of array elements
    sum = 0

    # Stores index of the smallest element
    # removed from the array to make sum
    # divisible by K
    res = -1

    # Stores the smallest element removed
    # from the array to make sum divisible by K
    mini = 1e9

    # Traverse the array, arr[]
    for i in range(n):

        # Update sum
        sum += arr[i]

    # Traverse the array arr[]
    for i in range(n):

        # Calculate remaining sum
        temp = sum - arr[i]

        # If sum is divisible by K
        if (temp % K == 0) :

            # If res ==-1 or mini is greater
            # than arr[i]
            if (res == -1 or mini > arr[i]) :

                # Update res and mini
                res = i + 1
                mini = arr[i]
    return res;

# Driver Code
arr = [ 14, 7, 8, 2, 4 ]
K = 7
N = len(arr)
print(findIndex(arr, N, K))

# This code is contributed by sanjoy_62.
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to find index of the smallest
// array element required to be removed
// to make sum divisible by K
static int findIndex(int[] arr, int n, int K)
{

    // Stores sum of array elements
    int sum = 0;

    // Stores index of the smallest
    // element removed from the array
    // to make sum divisible by K
    int res = -1;

    // Stores the smallest element
    // removed from the array to
    // make sum divisible by K
    int mini = (int)1e9;

    // Traverse the array, arr[]
    for(int i = 0; i < n; i++)
    {

        // Update sum
        sum += arr[i];
    }

    // Traverse the array arr[]
    for(int i = 0; i < n; i++)
    {

        // Calculate remaining sum
        int temp = sum - arr[i];

        // If sum is divisible by K
        if (temp % K == 0)
        {

            // If res ==-1 or mini is greater
            // than arr[i]
            if (res == -1 || mini > arr[i])
            {

                // Update res and mini
                res = i + 1;
                mini = arr[i];
            }
        }
    }
    return res;
}

// Driver code   
static void Main()
{
    int[] arr = { 14, 7, 8, 2, 4 };
    int K = 7;
    int N = arr.Length;

    Console.WriteLine(findIndex(arr, N, K)); 
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find index of the smallest array element
// required to be removed to make sum divisible by K
function findIndex(arr,n,K)
{

    // Stores sum of array elements
    let sum = 0;

    // Stores index of the smallest element
    // removed from the array to make sum
    // divisible by K
    let res = -1;

    // Stores the smallest element removed
    // from the array to make sum divisible by K
    let mini = parseInt( 1e9);

    // Traverse the array, arr[]
    for (let i = 0; i < n; i++)
    {

        // Update sum
        sum += arr[i];
    }

    // Traverse the array arr[]
    for (let i = 0; i < n; i++)
    {

        // Calculate remaining sum
        let temp = sum - arr[i];

        // If sum is divisible by K
        if (temp % K == 0)
        {

            // If res ==-1 or mini is greater
            // than arr[i]
            if (res == -1 || mini > arr[i])
            {

                // Update res and mini
                res = i + 1;
                mini = arr[i];
            }
        }
    }
    return res;
}

// Driver Code

    let arr = [ 14, 7, 8, 2, 4 ];
    let K = 7;
    let N = arr.length;
    document.write(findIndex(arr, N, K));

// This code is contributed by sravan kumar

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)