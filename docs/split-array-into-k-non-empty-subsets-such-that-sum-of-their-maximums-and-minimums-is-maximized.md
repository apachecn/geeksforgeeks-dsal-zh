# 将数组拆分成 K 个非空子集，使其最大值和最小值之和最大

> 原文:[https://www . geesforgeks . org/split-array-in-k-non-empty-subset-这样它们的最大值和最小值之和最大化/](https://www.geeksforgeeks.org/split-array-into-k-non-empty-subsets-such-that-sum-of-their-maximums-and-minimums-is-maximized/)

给定由 **N** 和 **K** 整数组成的两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和**S【】**，任务是在将数组拆分为 **K** 子集后，找出每个子集的最小值和最大值的最大值和，使得每个子集的[大小等于数组中的一个元素**S【】**。](https://www.geeksforgeeks.org/print-subsets-given-size-set/)

**示例:**

> **输入:** arr[] = {1，13，7，17}，S[] = {1，3}
> **输出:** 48
> **解释:**考虑将数组拆分为{17}、{1，7，13}，这样子集的大小分别为 1 和 3，数组 S[]。
> 每个子集的最大值和最小值之和为(17 + 17 + 1 + 13) = 48。
> 
> **输入:** arr[ ] = {5，1，-30，0，11，20，19}，S[] = {4，1，2}
> **输出:** 45

**方法:**给定的问题可以使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)解决，思路是在每个组中插入第一个 **K** 最大元素，然后开始先用更大的元素填充较小的组。按照以下步骤解决问题:

*   初始化一个变量，比如说 **ans** 为 **0** ，存储所有子集的最大值和最小值之和。
*   [按降序排列数组**arr[]**](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)。
*   [按升序排列阵列](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)**【S】**。
*   求数组的第一个 **K** 元素的[和，存储在变量 **ans** 中，将**S【】**的所有元素递减 **1** 。](https://www.geeksforgeeks.org/find-maximum-minimum-sum-subarray-size-k/)
*   初始化一个变量，比如说**计数器**为**K–1**，存储每个子集的最小元素的索引。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **S[]** ，通过 **S[i]** 递增计数器，并将 **arr【计数器】**的值添加到 **ans** 中。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function find maximum sum of
// minimum and maximum of K subsets
int maximumSum(int arr[], int S[],
               int N, int K)
{
    // Stores the result
    int ans = 0;

    // Sort the array arr[] in
    // decreasing order
    sort(arr, arr + N, greater<int>());

    // Traverse the range [0, K]
    for (int i = 0; i < K; i++)
        ans += arr[i];

    // Sort the array S[] in
    // ascending order
    sort(S, S + K);

    // Traverse the array S[]
    for (int i = 0; i < K; i++) {

        // If S{i] is 1
        if (S[i] == 1)
            ans += arr[i];

        S[i]--;
    }

    // Stores the index of the minimum
    // element of the i-th subset
    int counter = K - 1;

    // Traverse the array S[]
    for (int i = 0; i < K; i++) {

        // Update the counter
        counter = counter + S[i];

        if (S[i] != 0)
            ans += arr[counter];
    }

    // Return the resultant sum
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 1, 13, 7, 17 };
    int S[] = { 1, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = sizeof(S) / sizeof(S[0]);
    cout << maximumSum(arr, S, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function find maximum sum of
// minimum and maximum of K subsets
static int maximumSum(int arr[], int S[],
                      int N, int K)
{

    // Stores the result
    int ans = 0;

    // Sort the array arr[] in
    // decreasing order
    Arrays.sort(arr);
    for(int i = 0; i < N / 2; i++)
    {
        int temp = arr[i];
        arr[i] = arr[N - 1 - i];
        arr[N - 1 - i] = temp;
    }

    // Traverse the range [0, K]
    for(int i = 0; i < K; i++)
        ans += arr[i];

    // Sort the array S[] in
    // ascending order
    Arrays.sort(S);

    // Traverse the array S[]
    for(int i = 0; i < K; i++)
    {

        // If S{i] is 1
        if (S[i] == 1)
            ans += arr[i];

        S[i]--;
    }

    // Stores the index of the minimum
    // element of the i-th subset
    int counter = K - 1;

    // Traverse the array S[]
    for(int i = 0; i < K; i++)
    {

        // Update the counter
        counter = counter + S[i];

        if (S[i] != 0)
            ans += arr[counter];
    }

    // Return the resultant sum
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 13, 7, 17 };
    int S[] = { 1, 3 };
    int N = arr.length;
    int K = S.length;

    System.out.println(maximumSum(arr, S, N, K));
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function find maximum sum of
# minimum and maximum of K subsets
def maximumSum(arr, S, N, K):

    # Stores the result
    ans = 0

    # Sort the array arr[] in
    # decreasing order
    arr = sorted(arr)[::-1]

    # Traverse the range [0, K]
    for i in range(K):
        ans += arr[i]

    # Sort the array S[] in
    # ascending order
    S = sorted(S)

    # Traverse the array S[]
    for i in range(K):

        # If S{i] is 1
        if (S[i] == 1):
            ans += arr[i]

        S[i] -= 1

    # Stores the index of the minimum
    # element of the i-th subset
    counter = K - 1

    # Traverse the array S[]
    for i in range(K):

        # Update the counter
        counter = counter + S[i]

        if (S[i] != 0):
            ans += arr[counter]

    # Return the resultant sum
    return ans

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 13, 7, 17 ]
    S = [ 1, 3 ]
    N = len(arr)
    K = len(S)

    print (maximumSum(arr, S, N, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function find maximum sum of
    // minimum and maximum of K subsets
    static int maximumSum(int[] arr, int[] S, int N, int K)
    {

        // Stores the result
        int ans = 0;

        // Sort the array arr[] in
        // decreasing order
        Array.Sort(arr);
        for (int i = 0; i < N / 2; i++) {
            int temp = arr[i];
            arr[i] = arr[N - 1 - i];
            arr[N - 1 - i] = temp;
        }

        // Traverse the range [0, K]
        for (int i = 0; i < K; i++)
            ans += arr[i];

        // Sort the array S[] in
        // ascending order
        Array.Sort(S);

        // Traverse the array S[]
        for (int i = 0; i < K; i++) {

            // If S{i] is 1
            if (S[i] == 1)
                ans += arr[i];

            S[i]--;
        }

        // Stores the index of the minimum
        // element of the i-th subset
        int counter = K - 1;

        // Traverse the array S[]
        for (int i = 0; i < K; i++) {

            // Update the counter
            counter = counter + S[i];

            if (S[i] != 0)
                ans += arr[counter];
        }

        // Return the resultant sum
        return ans;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int[] arr = { 1, 13, 7, 17 };
        int[] S = { 1, 3 };
        int N = arr.Length;
        int K = S.Length;

        Console.WriteLine(maximumSum(arr, S, N, K));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function find maximum sum of
// minimum and maximum of K subsets
function maximumSum(arr, S, N, K)
{
    // Stores the result
    var ans = 0;
    var i;
    // Sort the array arr[] in
    // decreasing order
    arr.sort((a, b) => b - a);

    // Traverse the range [0, K]
    for (i = 0; i < K; i++)
        ans += arr[i];

    // Sort the array S[] in
    // ascending order
    S.sort();
    // S.reverse();
    // Traverse the array S[]
    for (i = 0; i < K; i++) {

        // If S{i] is 1
        if (S[i] == 1)
            ans += arr[i];

        S[i] -= 1;
    }

    // Stores the index of the minimum
    // element of the i-th subset
    var counter = K - 1;

    // Traverse the array S[]
    for (i = 0; i < K; i++) {

        // Update the counter
        counter = counter + S[i];

        if (S[i] != 0)
            ans += arr[counter];
    }

    // Return the resultant sum
    return ans;
}

// Driver Code
    var arr = [1, 13, 7, 17];
    var S = [1, 3];
    var N = arr.length;
    var K = S.length;
    document.write(maximumSum(arr, S, N, K));

</script>
```

**Output:** 

```
48
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)