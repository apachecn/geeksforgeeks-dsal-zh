# 生成一个最大和的数组，使得每个元素超过其左侧或右侧的所有元素

> 原文:[https://www . geeksforgeeks . org/生成一个最大和数组，使得每个元素都超过其左侧或右侧存在的所有元素/](https://www.geeksforgeeks.org/generate-an-array-of-maximum-sum-such-that-each-element-exceeds-all-elements-present-either-on-its-left-or-right/)

给定一个由 **N** 正整数组成的数组 **A[]** ，任务是构造一个大小为 **N** 的数组 **B[]** ，数组元素的最大可能[和满足每个索引 **i** 的以下标准:](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

*   数组元素 **B[i]** 必须小于或等于 **A[i]** 。
*   对于每个索引 **i** ，**B【I】**必须大于其左侧或右侧的所有元素。

**示例:**

> **输入:** A[] = {10，6，8}
> **输出:** 10 6 6
> **解释:**
> 将数组 B[]视为满足给定标准的{10，6，6}，如下所示，具有最大元素和:
> 
> 1.  **对于数组元素 B[0](= 10):** 数组 B[]中索引 0 左右的最大元素分别为-1 和 6，B[0](= 10)小于等于-1。
> 2.  **对于数组元素 B[1](= 6):** 数组 B[]中索引 1 左右的最大元素分别为 10 和 6，B[1](= 6)小于等于 6。
> 3.  **对于数组元素 B[2](= 6):** 数组 B[]中索引 2 左右的最大元素分别为 10 和-1，B[2](= 6)小于等于-1。
> 
> **输入:** A[ ] = {1，2，3，1}
> **输出:** 1 2 3 1

**方法:**通过观察数组中总有一个[最大元素先递增后单调递减](https://www.geeksforgeeks.org/find-the-maximum-element-in-an-array-which-is-first-increasing-and-then-decreasing/)的事实，可以解决给定的问题。因此，想法是将新数组 **B[]** 的每个数组元素逐个最大化，然后检查最大和。按照以下步骤解决给定的问题:

*   初始化数组，比如说 **arrA[]** 和 **ans[]** ，分别存储数组元素 **A[]** 和结果数组。
*   初始化一个变量，比如说 **maxSum** 为 **0** ，存储数组元素的最大和。
*   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**并执行以下步骤:
    *   初始化一个数组，比如 **arrB[]** ，可以存储结果数组。
    *   以单调递增的顺序分配所有数组元素**arrB【I】**，直到每个索引 **i** 。
    *   在随后的范围**【I，N】**内，以单调递减的顺序分配所有数组元素**arrB【I】**。
    *   现在，[求数组](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/) **arrB[]** 的和，如果和大于 **maxSum** ，则更新 **maxSum** 和数组 **ans[]** 为当前和，当前数组 **arrB[]** 被构造。
*   完成上述步骤后，打印数组 **arrB[]** 作为结果数组。

下面是上述方法的实现:

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to construct the array
// having maximum sum satisfying the
// given criteria
void maximumSumArray(int arr[], int N)
{
    // Declaration of the array arrA[]
    // and ans[]
    vector<int> arrA(N), ans(N);

    // Stores the maximum sum of the
    // resultant array
    int maxSum = 0;

    // Initialize the array arrA[]
    for (int i = 0; i < N; i++)
        arrA[i] = arr[i];

    // Traversing the array arrA[]
    for (int i = 0; i < N; i++) {

        // Initialize the array arrB[]
        vector<int> arrB(N);
        int maximum = arrA[i];

        // Assign the maximum element
        // to the current element
        arrB[i] = maximum;

        // Form the first increasing
        // till every index i
        for (int j = i - 1; j >= 0; j--) {
            arrB[j] = min(maximum, arrA[j]);
            maximum = arrB[j];
        }

        // Make the current element
        // as the maximum element
        maximum = arrA[i];

        // Forming decreasing from the
        // index i + 1 to the index N
        for (int j = i + 1; j < N; j++) {
            arrB[j] = min(maximum, arrA[j]);
            maximum = arrB[j];
        }

        // Initialize the sum
        int sum = 0;

        // Find the total sum
        for (int j = 0; j < N; j++)
            sum += arrB[j];

        // Check if the total sum is
        // at least the sum found
        // then make ans as ansB
        if (sum > maxSum) {
            maxSum = sum;
            ans = arrB;
        }
    }

    // Print the final array formed
    for (int val : ans) {
        cout << val << " ";
    }
}

// Driver Code
int main()
{
    int A[] = { 10, 6, 8 };
    int N = sizeof(A) / sizeof(A[0]);
    maximumSumArray(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

// Function to construct the array
// having maximum sum satisfying the
// given criteria
static void maximumSumArray(int arr[], int N)
{
    // Declaration of the array arrA[]
    // and ans[]
    int[] arrA  = new int[(N)];
    int[] ans  = new int[(N)];

    // Stores the maximum sum of the
    // resultant array
    int maxSum = 0;

    // Initialize the array arrA[]
    for (int i = 0; i < N; i++)
        arrA[i] = arr[i];

    // Traversing the array arrA[]
    for (int i = 0; i < N; i++) {

        // Initialize the array arrB[]
        int[] arrB = new int[(N)];
        int maximum = arrA[i];

        // Assign the maximum element
        // to the current element
        arrB[i] = maximum;

        // Form the first increasing
        // till every index i
        for (int j = i - 1; j >= 0; j--) {
            arrB[j] = Math.min(maximum, arrA[j]);
            maximum = arrB[j];
        }

        // Make the current element
        // as the maximum element
        maximum = arrA[i];

        // Forming decreasing from the
        // index i + 1 to the index N
        for (int j = i + 1; j < N; j++) {
            arrB[j] = Math.min(maximum, arrA[j]);
            maximum = arrB[j];
        }

        // Initialize the sum
        int sum = 0;

        // Find the total sum
        for (int j = 0; j < N; j++)
            sum += arrB[j];

        // Check if the total sum is
        // at least the sum found
        // then make ans as ansB
        if (sum > maxSum) {
            maxSum = sum;
            ans = arrB;
        }
    }

    // Print the final array formed
    for (int val : ans) {
        System.out.print(val + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 10, 6, 8 };
    int N = A.length;
    maximumSumArray(A, N);
}
}

// This code is contributed by splevel62.
```

## 蟒蛇 3

```
# Python program for the above approach;

# Function to construct the array
# having maximum sum satisfying the
# given criteria
def maximumSumArray(arr, N):

    # Declaration of the array arrA[]
    # and ans[]
    arrA = [0] * N
    ans = [0] * N

    # Stores the maximum sum of the
    # resultant array
    maxSum = 0;

    # Initialize the array arrA[]
    for i in range(N):
        arrA[i] = arr[i];

    # Traversing the array arrA[]
    for i in range(N):

        # Initialize the array arrB[]
        arrB = [0] * N
        maximum = arrA[i];

        # Assign the maximum element
        # to the current element
        arrB[i] = maximum;

        temp = 0

        # Form the first increasing
        # till every index i
        for j in range(i - 1, -1, -1):
            arrB[j] = min(maximum, arrA[j]);
            maximum = arrB[j];
            temp = j

        # Make the current element
        # as the maximum element
        maximum = arrA[i];

        # Forming decreasing from the
        # index i + 1 to the index N
        for j in range(i + 1, N):
            arrB[j] = min(maximum, arrA[j]);
            maximum = arrB[j];

        # Initialize the sum
        sum = 0;

        # Find the total sum
        for j in range(N):
            sum += arrB[j];

        # Check if the total sum is
        # at least the sum found
        # then make ans as ansB
        if (sum > maxSum):
            maxSum = sum;
            ans = arrB;

    # Print the final array formed
    for val in ans:
        print(val);

# Driver Code
A = [ 10, 6, 8 ];
N = len(A)

maximumSumArray(A, N);

# This code is contributed by _Saurabh_Jaiswal
```

## C#

```
// C# code for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to construct the array
// having maximum sum satisfying the
// given criteria
static void maximumSumArray(int []arr, int N)
{
    // Declaration of the array arrA[]
    // and ans[]
    int []arrA = new int[N];
    int []ans = new int[N];

    // Stores the maximum sum of the
    // resultant array
    int maxSum = 0;

    // Initialize the array arrA[]
    for (int i = 0; i < N; i++)
        arrA[i] = arr[i];

    // Traversing the array arrA[]
    for (int i = 0; i < N; i++) {

        // Initialize the array arrB[]
        int []arrB = new int[N];
        int maximum = arrA[i];

        // Assign the maximum element
        // to the current element
        arrB[i] = maximum;

        // Form the first increasing
        // till every index i
        for (int j = i - 1; j >= 0; j--) {
            arrB[j] = Math.Min(maximum, arrA[j]);
            maximum = arrB[j];
        }

        // Make the current element
        // as the maximum element
        maximum = arrA[i];

        // Forming decreasing from the
        // index i + 1 to the index N
        for (int j = i + 1; j < N; j++) {
            arrB[j] = Math.Min(maximum, arrA[j]);
            maximum = arrB[j];
        }

        // Initialize the sum
        int sum = 0;

        // Find the total sum
        for (int j = 0; j < N; j++)
            sum += arrB[j];

        // Check if the total sum is
        // at least the sum found
        // then make ans as ansB
        if (sum > maxSum) {
            maxSum = sum;
            ans = arrB;
        }
    }

    // Print the final array formed
    foreach (int val in ans) {
        Console.Write(val + " ");
    }
}

// Driver Code
public static void Main()
{
    int []A = { 10, 6, 8 };
    int N = A.Length;
    maximumSumArray(A, N);
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach;

// Function to construct the array
// having maximum sum satisfying the
// given criteria
function maximumSumArray(arr, N)
{

    // Declaration of the array arrA[]
    // and ans[]
    let arrA = new Array(N);
    let ans = new Array(N);

    // Stores the maximum sum of the
    // resultant array
    let maxSum = 0;

    // Initialize the array arrA[]
    for(let i = 0; i < N; i++)
        arrA[i] = arr[i];

    // Traversing the array arrA[]
    for(let i = 0; i < N; i++)
    {

        // Initialize the array arrB[]
        let arrB = new Array(N);
        let maximum = arrA[i];

        // Assign the maximum element
        // to the current element
        arrB[i] = maximum;

        // Form the first increasing
        // till every index i
        for(let j = i - 1; j >= 0; j--)
        {
            arrB[j] = Math.min(maximum, arrA[j]);
            maximum = arrB[j];
        }

        // Make the current element
        // as the maximum element
        maximum = arrA[i];

        // Forming decreasing from the
        // index i + 1 to the index N
        for(let j = i + 1; j < N; j++)
        {
            arrB[j] = Math.min(maximum, arrA[j]);
            maximum = arrB[j];
        }

        // Initialize the sum
        let sum = 0;

        // Find the total sum
        for(let j = 0; j < N; j++)
            sum += arrB[j];

        // Check if the total sum is
        // at least the sum found
        // then make ans as ansB
        if (sum > maxSum)
        {
            maxSum = sum;
            ans = arrB;
        }
    }

    // Print the final array formed
    for(let val of ans)
    {
        document.write(val + " ");
    }
}

// Driver Code
let A = [ 10, 6, 8 ];
let N = A.length;

maximumSumArray(A, N);

// This code is contributed by Potta Lokesh

</script>
```

**Output:** 

```
10 6 6
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*