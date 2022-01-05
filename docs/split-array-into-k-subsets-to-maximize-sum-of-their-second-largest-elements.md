# 将数组拆分成 K 个子集，最大化其第二大元素的和

> 原文:[https://www . geeksforgeeks . org/将数组拆分成 k 个子集，以最大化其第二大元素的总和/](https://www.geeksforgeeks.org/split-array-into-k-subsets-to-maximize-sum-of-their-second-largest-elements/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】】**，任务是将数组拆分为 **K** 个子集( **N % K = 0** )，使得所有子集的第二大元素之和最大化。

**示例:**

> **输入:** arr[] = {1，3，1，5，1，3}，K = 2
> **输出:** 4
> **解释:**将数组拆分为子集{1，1，3}和{1，3，5}最大化两个数组中第二大元素的总和。
> 
> **输入:** arr[] = {1，2，5，8，6，4，3，4，9}，K = 3
> **输出:** 17

**方法:**思路是[对数组](https://www.geeksforgeeks.org/sorting-algorithms/)进行排序，在[反向遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)时，每遇到一个第二元素，就不断增加，从数组中第二个最大的[元素开始，精确到 **K** 次。按照以下步骤解决问题:](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)

*   [按升序排列数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   [反方向穿越阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**。
*   初始化**I = N–1**。
*   迭代 **K** 次，将**arr【I–1】**相加，将 **i** 减少 **2** 。
*   最后，打印得到的总和。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to split array into
// K subsets having maximum
// sum of their second maximum elements
void splitArray(int arr[], int n, int K)
{
    // Sort the array
    sort(arr, arr + n);

    int i = n - 1;

    // Stores the maximum possible
    // sum of second maximums
    int result = 0;

    while (K--) {

        // Add second maximum
        // of current subset
        result += arr[i - 1];

        // Proceed to the second
        // maximum of next subset
        i -= 2;
    }

    // Print the maximum
    // sum obtained
    cout << result;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 3, 1, 5, 1, 3 };

    // Size of array
    int N = sizeof(arr)
            / sizeof(arr[0]);

    int K = 2;

    // Function Call
    splitArray(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.Arrays;

class GFG
{

// Function to split array into
// K subsets having maximum
// sum of their second maximum elements
static void splitArray(int arr[], int n, int K)
{
    // Sort the array
    Arrays.sort(arr);

    int i = n - 1;

    // Stores the maximum possible
    // sum of second maximums
    int result = 0;

    while (K-- != 0)
    {

        // Add second maximum
        // of current subset
        result += arr[i - 1];

        // Proceed to the second
        // maximum of next subset
        i -= 2;
    }

    // Print the maximum
    // sum obtained
    System.out.print(result);
}

// Drive Code
public static void main(String[] args)
{
    // Given array arr[]
    int[] arr = { 1, 3, 1, 5, 1, 3 };

    // Size of array
    int N = arr.length;

    int K = 2;

    // Function Call
    splitArray(arr, N, K);
}
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to split array into K
# subsets having maximum sum of
# their second maximum elements
def splitArray(arr, n, K):

    # Sort the array
    arr.sort()

    i = n - 1

    # Stores the maximum possible
    # sum of second maximums
    result = 0

    while (K > 0):

        # Add second maximum
        # of current subset
        result += arr[i - 1]

        # Proceed to the second
        # maximum of next subset
        i -= 2
        K -= 1

    # Print the maximum
    # sum obtained
    print(result)

# Driver Code
if __name__ == "__main__":

    # Given array arr[]
    arr = [ 1, 3, 1, 5, 1, 3 ]

    # Size of array
    N = len(arr)

    K = 2

    # Function Call
    splitArray(arr, N, K)

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

// Function to split array into
// K subsets having maximum
// sum of their second maximum elements
static void splitArray(int []arr, int n, int K)
{
    // Sort the array
    Array.Sort(arr);

    int i = n - 1;

    // Stores the maximum possible
    // sum of second maximums
    int result = 0;

    while (K-- != 0)
    {

        // Add second maximum
        // of current subset
        result += arr[i - 1];

        // Proceed to the second
        // maximum of next subset
        i -= 2;
    }

    // Print the maximum
    // sum obtained
    Console.Write(result);
}

// Drive Code
public static void Main(String[] args)
{
    // Given array []arr
    int[] arr = { 1, 3, 1, 5, 1, 3 };

    // Size of array
    int N = arr.Length;

    int K = 2;

    // Function Call
    splitArray(arr, N, K);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to split array into
// K subsets having maximum
// sum of their second maximum elements
function splitArray(arr, n, K)
{

    // Sort the array
    arr.sort();

    let i = n - 1;

    // Stores the maximum possible
    // sum of second maximums
    let result = 0;

    while (K-- != 0)
    {

        // Add second maximum
        // of current subset
        result += arr[i - 1];

        // Proceed to the second
        // maximum of next subset
        i -= 2;
    }

    // Print the maximum
    // sum obtained
    document.write(result);
}

// Driver code

// Given array arr[]
let arr = [ 1, 3, 1, 5, 1, 3 ];

// Size of array
let N = arr.length;

let K = 2;

// Function Call
splitArray(arr, N, K);

// This code is contributed by avijitmondal1998

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N logN)*
***辅助空间:** O(N)*