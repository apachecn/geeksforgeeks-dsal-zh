# 将数组拆分成 K 个子集，使其最大值和最小值之和最大

> 原文:[https://www . geesforgeks . org/split-array-in-k-subset-to-maximum and-minimum 之和最大化/](https://www.geeksforgeeks.org/split-array-into-k-subsets-to-maximize-their-sum-of-maximums-and-minimums/)

给定一个整数 **K** 和一个长度为 **K** 倍数的数组**A【】**，任务是将给定数组的元素拆分成 **K** 个子集，每个子集具有相等数量的元素，使得每个子集的最大和最小元素之和是可能的最大和。

**示例:**

> **输入:** K = 2，A[ ] = {1，13，7，17，6，5}
> **输出:** 37
> **解释:**
> 第一组:{1，5，17}最大值= 17，最小值= 1
> 第二组:{6，7，13}最大值= 13，最小值= 6
> 因此，最大可能和= 17 + 1 + 13 + 6 = 37
> 
> **输入:** K = 2，A[ ] = {10，10，10，11，11}
> **输出:** 42
> **解释:**
> 第一组:{11，10，10}最大值= 11，最小值= 10
> 第二组:{11，10，10}最大值= 11，最小值= 10
> 因此，最大可能和= 11 + 10 + 11 + 10

**天真方法:**
解决这个问题最简单的方法是生成所有可能的大小为 **N/K** 的 **K** 子集的组，对于每个组，在每个子集中找到最大值和最小值，并计算它们的和。计算出所有组的总和后，打印得出的最大总和。
***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(N)*

**高效方法:**
想法是使用[贪婪技术](https://www.geeksforgeeks.org/greedy-algorithms/)优化上述方法。因为需要每个子集的最大和最小元素的最大和，所以尝试最大化最大元素和最小元素。对于每个子集的最大元素，首先从给定数组中取出 **K** 个最大元素，并将每个元素插入不同的子集。对于每个子集的最小元素，从排序后的数组中，从索引 **0** 开始，在**(N/K)–1**间隔处挑选下一个元素，因为每个子集的大小为 **N / K** ，并且每个元素已经包含一个最大元素。

请遵循以下步骤:

*   计算各组元素的数量，即 **(N/K)** 。
*   将 **A[ ]** 的所有元素非降序排序。
*   对于**最大**元素的总和，将排序数组中所有 **K** 最大的元素相加。
*   对于**最小**元素的和，从索引 **0** 开始，选择 **K** 元素，每个元素都有**(N/K)–1**间隔，并将其相加。
*   最后计算最大和最小元素的和。打印他们各自的总和作为最终答案。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that prints
// the maximum sum possible
void maximumSum(int arr[],
                int n, int k)
{

    // Find elements in each group
    int elt = n / k;

    int sum = 0;

    // Sort all elements in
    // non-descending order
    sort(arr, arr + n);

    int count = 0;
    int i = n - 1;

    // Add K largest elements
    while (count < k) {
        sum += arr[i];
        i--;
        count++;
    }

    count = 0;
    i = 0;

    // For sum of minimum
    // elements from each subset
    while (count < k) {
        sum += arr[i];
        i += elt - 1;
        count++;
    }

    // Printing the maximum sum
    cout << sum << "\n";
}

// Driver Code
int main()
{
    int Arr[] = { 1, 13, 7, 17, 6, 5 };

    int K = 2;

    int size = sizeof(Arr) / sizeof(Arr[0]);

    maximumSum(Arr, size, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.Arrays;

class GFG{

// Function that prints
// the maximum sum possible
static void maximumSum(int arr[],
                       int n, int k)
{

    // Find elements in each group
    int elt = n / k;

    int sum = 0;

    // Sort all elements in
    // non-descending order
    Arrays.sort(arr);

    int count = 0;
    int i = n - 1;

    // Add K largest elements
    while (count < k)
    {
        sum += arr[i];
        i--;
        count++;
    }
    count = 0;
    i = 0;

    // For sum of minimum
    // elements from each subset
    while (count < k)
    {
        sum += arr[i];
        i += elt - 1;
        count++;
    }

    // Printing the maximum sum
    System.out.println(sum);
}

// Driver code
public static void main (String[] args)
{
    int Arr[] = { 1, 13, 7, 17, 6, 5 };

    int K = 2;

    int size = Arr.length;

    maximumSum(Arr, size, K);
}
}

// This code is contributed by Shubham Prakash
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function that prints
# the maximum sum possible
def maximumSum(arr, n, k):

    # Find elements in each group
    elt = n // k;

    sum = 0;

    # Sort all elements in
    # non-descending order
    arr.sort();

    count = 0;
    i = n - 1;

    # Add K largest elements
    while (count < k):
        sum += arr[i];
        i -= 1;
        count += 1;

    count = 0;
    i = 0;

    # For sum of minimum
    # elements from each subset
    while (count < k):
        sum += arr[i];
        i += elt - 1;
        count += 1;

    # Printing the maximum sum
    print(sum);

# Driver code
if __name__ == '__main__':
    Arr = [1, 13, 7, 17, 6, 5];

    K = 2;

    size = len(Arr);

    maximumSum(Arr, size, K);

# This code is contributed by sapnasingh4991
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function that prints
// the maximum sum possible
static void maximumSum(int []arr,
                       int n, int k)
{

    // Find elements in each group
    int elt = n / k;

    int sum = 0;

    // Sort all elements in
    // non-descending order
    Array.Sort(arr);

    int count = 0;
    int i = n - 1;

    // Add K largest elements
    while (count < k)
    {
        sum += arr[i];
        i--;
        count++;
    }
    count = 0;
    i = 0;

    // For sum of minimum
    // elements from each subset
    while (count < k)
    {
        sum += arr[i];
        i += elt - 1;
        count++;
    }

    // Printing the maximum sum
    Console.WriteLine(sum);
}

// Driver code
public static void Main(String[] args)
{
    int []Arr = { 1, 13, 7, 17, 6, 5 };

    int K = 2;

    int size = Arr.Length;

    maximumSum(Arr, size, K);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript program implementation
// of the approach

// Function that prints
// the maximum sum possible
function maximumSum(arr, n, k)
{

    // Find elements in each group
    let elt = (n / k);

    let sum = 0;

    // Sort all elements in
    // non-descending order
    arr.sort((a, b) => a - b);

    let count = 0;
    let i = n - 1;

    // Add K largest elements
    while (count < k)
    {
        sum += arr[i];
        i--;
        count++;
    }
    count = 0;
    i = 0;

    // For sum of minimum
    // elements from each subset
    while (count < k)
    {
        sum += arr[i];
        i += elt - 1;
        count++;
    }

    // Printing the maximum sum
    document.write(sum);
}

// Driver Code

       let Arr = [ 1, 13, 7, 17, 6, 5 ];

    let K = 2;

    let size = Arr.length;

    maximumSum(Arr, size, K);

</script>
```

**Output:** 

```
37
```

***时间复杂度:** O(N*logN)*
***辅助空间:** O(1)*