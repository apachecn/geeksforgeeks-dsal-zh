# 包括负整数的 K 大小的最小乘积子阵列

> 原文:[https://www . geeksforgeeks . org/最小产品尺寸子阵列 k-包括负整数/](https://www.geeksforgeeks.org/minimum-product-subarray-of-size-k-including-negative-integers/)

给定一个长度为 **N、**的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到包含负整数的数组的大小为 **K** 的[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的最小乘积。

**示例:**

> **输入:** arr = [2，3，-1，-5，4，0]，K = 3
> **输出:** -6
> **说明:**子阵列{2，3，-1}的乘积是-6，这是最小可能的。
> 
> **输入:** arr = [-2，-4，0，1，5，-6，9]，K =4
> **输出:** -270
> **说明:**子阵{1，5，-6，9}的乘积是-270，这是最小可能。

如果数组仅由正数组成，则可以仅使用滑动窗口技术来有效地解决该问题，如这里所讨论的。

**方法:**给定的问题可以使用[两点技巧](https://www.geeksforgeeks.org/two-pointers-technique/)和[滑动窗口](https://www.geeksforgeeks.org/window-sliding-technique/)方法来解决。可以遵循以下步骤来解决问题:

*   [迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/) **arr** 直到**K–1**，将每一个非零数字相乘，找到乘积，并计算子数组中的零的数量。
*   [迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/) **arr** 从 **K** 直到数组结束，每次迭代:
    *   如果当前元素不是零，则将其乘以乘积，否则增加零的计数
    *   如果当前滑动窗口左侧的元素不是零，则用该元素除积，否则减少零的计数
    *   如果滑动窗口中的零数为 0 ，则用当前产品更新结果，否则用零更新
*   返回结果 **res** 。

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// product of subarray of size K
int minProdK(vector<int>& arr, int K)
{

    // Initialize prod to 1
    // and zeros to 0
    int prod = 1, zeros = 0;

    // Initialize length of the array
    int N = arr.size();

    // Iterate the array arr till K - 1
    for (int i = 0; i < K; i++) {

        // If current element is 0
        // then increment zeros
        if (arr[i] == 0)
            zeros++;

        // Else multiply current
        // element to prod
        else
            prod *= arr[i];
    }

    // Initialize prod to 0 if zeros > 0
    // else to prod
    int res = zeros == 0 ? prod : 0;

    // Iterate the array arr
    // from K till the end
    for (int right = K; right < N; right++) {

        // If current element is 0
        // then increment zeros
        if (arr[right] == 0)
            zeros++;

        // Else multiply arr[right]
        // to prod
        else
            prod *= arr[right];

        // If leftmost element in
        // the sliding window is 0
        // then decrement zeros
        if (arr[right - K] == 0)
            zeros--;

        // Else divide prod by arr[right-K]
        else
            prod /= arr[right - K];

        // If zeros == 0 then update
        // res by taking minimum value
        // of res and prod
        if (zeros == 0)
            res = min(res, prod);

        // If zeros > 0 and res > 0
        // then initialize res to 0
        else if (res > 0)
            res = 0;
    }

    // Return the answer as res
    return res;
}

// Driver code
int main()
{

    // Initialize the array
    vector<int> arr = { 2, 3, -1, -5, 4, 0 };

    // Initialize the value of K
    int K = 3;

    // Call the function and
    // print the result
    cout << minProdK(arr, K);

    return 0;
}

    // This code is contributed by rakeshsahni
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to find the minimum
    // product of subarray of size K
    public static int minProdK(
        int arr[], int K)
    {

        // Initialize prod to 1
        // and zeros to 0
        int prod = 1, zeros = 0;

        // Initialize length of the array
        int N = arr.length;

        // Iterate the array arr till K - 1
        for (int i = 0; i < K; i++) {

            // If current element is 0
            // then increment zeros
            if (arr[i] == 0)
                zeros++;

            // Else multiply current
            // element to prod
            else
                prod *= arr[i];
        }

        // Initialize prod to 0 if zeros > 0
        // else to prod
        int res = zeros == 0 ? prod : 0;

        // Iterate the array arr
        // from K till the end
        for (int right = K; right < N; right++) {

            // If current element is 0
            // then increment zeros
            if (arr[right] == 0)
                zeros++;

            // Else multiply arr[right]
            // to prod
            else
                prod *= arr[right];

            // If leftmost element in
            // the sliding window is 0
            // then decrement zeros
            if (arr[right - K] == 0)
                zeros--;

            // Else divide prod by arr[right-K]
            else
                prod /= arr[right - K];

            // If zeros == 0 then update
            // res by taking minimum value
            // of res and prod
            if (zeros == 0)
                res = Math.min(res, prod);

            // If zeros > 0 and res > 0
            // then initialize res to 0
            else if (res > 0)
                res = 0;
        }

        // Return the answer as res
        return res;
    }

    // Driver code
    public static void main(String[] args)
    {

        // Initialize the array
        int[] arr = { 2, 3, -1, -5, 4, 0 };

        // Initialize the value of K
        int K = 3;

        // Call the function and
        // print the result
        System.out.println(minProdK(arr, K));
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation for the above approach

# Function to find the minimum
# product of subarray of size K
def minProdK(arr, K):

    # Initialize prod to 1
    # and zeros to 0
    prod = 1
    zeros = 0

    # Initialize length of the array
    N = len(arr)

    # Iterate the array arr till K - 1
    for i in range(K):
        # If current element is 0
        # then increment zeros
        if (arr[i] == 0):
            zeros += 1

        # Else multiply current
        # element to prod
        else:
            prod *= arr[i]

    # Initialize prod to 0 if zeros > 0
    # else to prod
    if zeros == 0:
        res = prod
    else:
        res = 0

    # Iterate the array arr
    # from K till the end
    for right in range(K,  N):

        # If current element is 0
        # then increment zeros
        if (arr[right] == 0):
            zeros += 1

        # Else multiply arr[right]
        # to prod
        else:
            prod *= arr[right]

        # If leftmost element in
        # the sliding window is 0
        # then decrement zeros
        if (arr[right - K] == 0):
            zeros -= 1

        # Else divide prod by arr[right-K]
        else:
            prod //= arr[right - K]

        # If zeros == 0 then update
        # res by taking minimum value
        # of res and prod
        if (zeros == 0):
            res = min(res, prod)

        # If zeros > 0 and res > 0
        # then initialize res to 0
        elif (res > 0):
            res = 0

    # Return the answer as res
    return res

# Driver code
if __name__ == "__main__":

    # Initialize the array
    arr = [2, 3, -1, -5, 4, 0]

    # Initialize the value of K
    K = 3

    # Call the function and
    # print the result
    print(minProdK(arr, K))

    # This code is contributed by ukasp.
```

## C#

```
// C# implementation for the above approach
using System;
class GFG
{
    // Function to find the minimum
    // product of subarray of size K
    public static int minProdK(
        int []arr, int K)
    {

        // Initialize prod to 1
        // and zeros to 0
        int prod = 1, zeros = 0;

        // Initialize length of the array
        int N = arr.Length;

        // Iterate the array arr till K - 1
        for (int i = 0; i < K; i++) {

            // If current element is 0
            // then increment zeros
            if (arr[i] == 0)
                zeros++;

            // Else multiply current
            // element to prod
            else
                prod *= arr[i];
        }

        // Initialize prod to 0 if zeros > 0
        // else to prod
        int res = zeros == 0 ? prod : 0;

        // Iterate the array arr
        // from K till the end
        for (int right = K; right < N; right++) {

            // If current element is 0
            // then increment zeros
            if (arr[right] == 0)
                zeros++;

            // Else multiply arr[right]
            // to prod
            else
                prod *= arr[right];

            // If leftmost element in
            // the sliding window is 0
            // then decrement zeros
            if (arr[right - K] == 0)
                zeros--;

            // Else divide prod by arr[right-K]
            else
                prod /= arr[right - K];

            // If zeros == 0 then update
            // res by taking minimum value
            // of res and prod
            if (zeros == 0)
                res = Math.Min(res, prod);

            // If zeros > 0 and res > 0
            // then initialize res to 0
            else if (res > 0)
                res = 0;
        }

        // Return the answer as res
        return res;
    }

    // Driver code
    public static void Main()
    {

        // Initialize the array
        int[] arr = { 2, 3, -1, -5, 4, 0 };

        // Initialize the value of K
        int K = 3;

        // Call the function and
        // print the result
        Console.Write(minProdK(arr, K));
    }
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript implementation for the above approach

// Function to find the minimum
// product of subarray of size K
function minProdK(arr, K) {

    // Initialize prod to 1
    // and zeros to 0
    let prod = 1, zeros = 0;

    // Initialize length of the array
    let N = arr.length;

    // Iterate the array arr till K - 1
    for (let i = 0; i < K; i++) {

        // If current element is 0
        // then increment zeros
        if (arr[i] == 0)
            zeros++;

        // Else multiply current
        // element to prod
        else
            prod *= arr[i];
    }

    // Initialize prod to 0 if zeros > 0
    // else to prod
    let res = zeros == 0 ? prod : 0;

    // Iterate the array arr
    // from K till the end
    for (let right = K; right < N; right++) {

        // If current element is 0
        // then increment zeros
        if (arr[right] == 0)
            zeros++;

        // Else multiply arr[right]
        // to prod
        else
            prod *= arr[right];

        // If leftmost element in
        // the sliding window is 0
        // then decrement zeros
        if (arr[right - K] == 0)
            zeros--;

        // Else divide prod by arr[right-K]
        else
            prod /= arr[right - K];

        // If zeros == 0 then update
        // res by taking minimum value
        // of res and prod
        if (zeros == 0)
            res = Math.min(res, prod);

        // If zeros > 0 and res > 0
        // then initialize res to 0
        else if (res > 0)
            res = 0;
    }

    // Return the answer as res
    return res;
}

// Driver code

// Initialize the array
let arr = [2, 3, -1, -5, 4, 0];

// Initialize the value of K
let K = 3;

// Call the function and
// print the result
document.write(minProdK(arr, K));

// This code is contributed by Saurabh Jaiswal
</script>
```

**Output**

```
-6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)