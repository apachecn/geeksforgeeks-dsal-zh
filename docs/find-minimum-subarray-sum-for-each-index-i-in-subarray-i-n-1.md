# 求子阵列[i，N-1]

中每个索引 I 的最小子阵列和

> 原文:[https://www . geesforgeks . org/find-minimum-subarray-sum-for-in-index-I-n-1/](https://www.geeksforgeeks.org/find-minimum-subarray-sum-for-each-index-i-in-subarray-i-n-1/)

给定一个大小为 **N、**的[阵列](https://www.geeksforgeeks.org/arrays-in-c-cpp/) **arr[]** ，任务是为**【0，N-1】中的所有 **i** 找到[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)**【I，N-1】**中的**最小** [子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)和。**

**示例:**

> **输入:** arr[ ] = {3，-1，-2}
> **输出:** 3 -3 -2
> **解释:**
> 对于(i = 1)即{3，-1，-2}，对于{-1，-2}最小子阵和为-3。
> 对于(i = 2)即{-1，-2}，对于{-1，-2}，最小子阵和为-3。
> 对于(i = 3)即{-2}，对于{-2}，最小子阵和为-2。
> 
> **输入:** arr[ ] = {5，-3，-2，9，4}
> **输出:** -5 -5 -2 4 4

**方法:**使用标准的[卡丹最大子阵和](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)算法可以解决这个问题。按照以下步骤解决此问题:

*   [反转数组**arr【】**的元素](https://www.geeksforgeeks.org/how-to-invert-the-elements-of-a-boolean-array-in-python/)，即将**正**号更改为**负**号，反之亦然。
*   [使用变量 **i** : 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代
    *   使用[卡丹算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)求[子阵](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)T4】arr【I，N-1】的[最大子阵和](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)。
    *   [再次将**结果**反相](https://www.geeksforgeeks.org/how-to-invert-the-elements-of-a-boolean-array-in-python/)，打印**结果**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Kadane's Algorithm to find max
// sum subarray
int kadane(int arr[], int start, int end)
{
    int currMax = arr[start];
    int maxSoFar = arr[start];

    // Iterating from start to end
    for (int i = start + 1; i < end + 1; i++) {

        currMax = max(arr[i], arr[i] + currMax);
        maxSoFar = max(maxSoFar, currMax);
    }

    // Returning maximum sum
    return maxSoFar;
}

// Function to find the minimum subarray
// sum for each suffix
void minSubarraySum(int arr[], int n)
{

    // Inverting all the elements of
    // array arr[].
    for (int i = 0; i < n; i++) {
        arr[i] = -arr[i];
    }

    // Finding the result for each
    // subarray
    for (int i = 0; i < n; i++) {

        // Finding the max subarray sum
        int result = kadane(arr, i, n - 1);

        // Inverting the result
        result = -result;

        // Print the result
        cout << result << " ";
    }
}

// Driver code
int main()
{

    // Given Input
    int n = 5;
    int arr[] = { 5, -3, -2, 9, 4 };

    // Function Call
    minSubarraySum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Kadane's Algorithm to find max
// sum subarray
static int kadane(int arr[], int start, int end)
{
    int currMax = arr[start];
    int maxSoFar = arr[start];

    // Iterating from start to end
    for(int i = start + 1; i < end + 1; i++)
    {
        currMax = Math.max(arr[i], arr[i] + currMax);
        maxSoFar = Math.max(maxSoFar, currMax);
    }

    // Returning maximum sum
    return maxSoFar;
}

// Function to find the minimum subarray
// sum for each suffix
static void minSubarraySum(int arr[], int n)
{

    // Inverting all the elements of
    // array arr[].
    for(int i = 0; i < n; i++)
    {
        arr[i] = -arr[i];
    }

    // Finding the result for each
    // subarray
    for(int i = 0; i < n; i++)
    {

        // Finding the max subarray sum
        int result = kadane(arr, i, n - 1);

        // Inverting the result
        result = -result;

        // Print the result
        System.out.print(result + " ");
    }
}

// Driver code
public static void main(String[] args)
{

    // Given Input
    int n = 5;
    int arr[] = { 5, -3, -2, 9, 4 };

    // Function Call
    minSubarraySum(arr, n);
}
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Kadane's Algorithm to find max
# sum subarray
def kadane(arr, start, end):

    currMax = arr[start]
    maxSoFar = arr[start]

    # Iterating from start to end
    for i in range(start + 1,end + 1, 1):
        currMax = max(arr[i], arr[i] + currMax)
        maxSoFar = max(maxSoFar, currMax)

    # Returning maximum sum
    return maxSoFar

# Function to find the minimum subarray
# sum for each suffix
def minSubarraySum(arr, n):

    # Inverting all the elements of
    # array arr[].
    for i in range(n):
        arr[i] = -arr[i]

    # Finding the result for each
    # subarray
    for i in range(n):

        # Finding the max subarray sum
        result = kadane(arr, i, n - 1)

        # Inverting the result
        result = -result

        # Print the result
        print(result, end = " ")

# Driver code
if __name__ == '__main__':

    # Given Input
    n = 5
    arr = [ 5, -3, -2, 9, 4 ]

    # Function Call
    minSubarraySum(arr, n)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Kadane's Algorithm to find max
// sum subarray
static int kadane(int []arr, int start, int end)
{
    int currMax = arr[start];
    int maxSoFar = arr[start];

    // Iterating from start to end
    for(int i = start + 1; i < end + 1; i++)
    {
        currMax = Math.Max(arr[i], arr[i] + currMax);
        maxSoFar = Math.Max(maxSoFar, currMax);
    }

    // Returning maximum sum
    return maxSoFar;
}

// Function to find the minimum subarray
// sum for each suffix
static void minSubarraySum(int []arr, int n)
{

    // Inverting all the elements of
    // array arr[].
    for(int i = 0; i < n; i++)
    {
        arr[i] = -arr[i];
    }

    // Finding the result for each
    // subarray
    for(int i = 0; i < n; i++)
    {

        // Finding the max subarray sum
        int result = kadane(arr, i, n - 1);

        // Inverting the result
        result = -result;

        // Print the result
        Console.Write(result + " ");
    }
}

// Driver code
public static void Main(String[] args)
{

    // Given Input
    int n = 5;
    int []arr = { 5, -3, -2, 9, 4 };

    // Function Call
    minSubarraySum(arr, n);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Kadane's Algorithm to find max
// sum subarray
function kadane(arr, start, end)
{
    let currMax = arr[start];
    let maxSoFar = arr[start];

    // Iterating from start to end
    for(let i = start + 1; i < end + 1; i++)
    {
        currMax = Math.max(arr[i], arr[i] + currMax);
        maxSoFar = Math.max(maxSoFar, currMax);
    }

    // Returning maximum sum
    return maxSoFar;
}

// Function to find the minimum subarray
// sum for each suffix
function minSubarraySum(arr, n)
{

    // Inverting all the elements of
    // array arr[].
    for(let i = 0; i < n; i++)
    {
        arr[i] = -arr[i];
    }

    // Finding the result for each
    // subarray
    for(let i = 0; i < n; i++)
    {

        // Finding the max subarray sum
        let result = kadane(arr, i, n - 1);

        // Inverting the result
        result = -result;

        // Print the result
        document.write(result + " ");
    }
}

// Driver code

// Given Input
let n = 5;
let arr = [ 5, -3, -2, 9, 4 ];

// Function Call
minSubarraySum(arr, n);

// This code is contributed by gfgking

</script>
```

**Output**

```
-5 -5 -2 4 4 
```

***时间复杂度:** O(N^2)*
***辅助空间:** O(1)*