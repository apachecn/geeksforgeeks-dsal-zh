# 将数组拆分成最大可能的子集，其长度与最大元素的乘积至少为 K

> 原文:[https://www . geeksforgeeks . org/将数组拆分为最大可能的子集-长度乘积至少为-k 的最大元素/](https://www.geeksforgeeks.org/split-array-into-maximum-possible-subsets-having-product-of-their-length-with-the-maximum-element-at-least-k/)

给定一个由 **N** 个整数和一个正整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是通过将数组元素划分为不相交的子集，最大化其大小与其[最大元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)之积的子集的数量。

**示例:**

> **输入:** N = 5，K = 4，arr[] = {1，5，4，2，3}
> **输出:** 3
> **解释:**
> 数组可以拆分为 3 个可能的子集{1，2}、{4，3}和{5}，这些子集的最大元素与其大小的乘积至少为 K(= 4)。因此，这种子集的计数是 3。
> 
> **输入:** N = 4，K = 81，arr[] = {12，8，14，20 }
> T3】输出: 0

**方法:**给定的问题可以通过观察至少是**K**的元素可以单独形成一个合适的群来解决。为了提取元素不大于等于 **K** 的组的最大数量，想法是从数组的[最小元素](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/)**arr【】**开始包含元素，然后继续移动到更大的元素，直到形成合适的组。按照以下步骤解决问题:

*   初始化一个变量，比如说**计数**为 **0** ，存储子集的结果计数，而**预**为 **1** 存储组的初始大小。
*   [按升序排列给定数组**arr[]**](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   [使用变量迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，说出 **i** ，并执行以下步骤:
    *   如果 **arr[i] * pre** 的值至少为**K**，则将**计数**的值增加 **1** ，并将 **pre** 的值设置为 **1** 。
    *   否则，用 **1** 增加**前**的值。
*   执行上述步骤后，打印**计数**的值作为子集的结果计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum
// number of subsets into which
// the array can be split
void countOfSubsets(int arr[], int N,
                    int K)
{
    // Stores the maximum number of
    // subsets
    int count = 0;
    int pre = 1;

    // Sort the given array
    sort(arr, arr + N);

    // Iterate over the range [0, N]
    for (int i = 0; i < N; i++) {

        // If current subset satisfies
        // the given condition
        if (arr[i] * pre >= K) {
            count++;
            pre = 1;
        }

        // Otherwise, increment pre
        else {
            pre++;
        }
    }

    cout << count;
}

// Driver Code
int main()
{
    int arr[] = { 1, 5, 4, 2, 3 };
    int K = 2;
    int N = sizeof(arr) / sizeof(arr[0]);

    countOfSubsets(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.util.*;

class GFG {
    // Function to find the maximum
    // number of subsets into which
    // the array can be split
    public static void countOfSubsets(int[] arr, int N,
                                      int K)
    {
        // Stores the maximum number of
        // subsets
        int count = 0;
        int pre = 1;

        // Sort the given array
        Arrays.sort(arr);

        // Iterate over the range [0, N]
        for (int i = 0; i < N; i++) {

            // If current subset satisfies
            // the given condition
            if (arr[i] * pre >= K) {
                count++;
                pre = 1;
            }

            // Otherwise, increment pre
            else {
                pre++;
            }
        }

        System.out.println(count);
    }

    public static void main(String[] args)
    {
        int[] arr = { 1, 5, 4, 2, 3 };
        int K = 2;
        int N = 5;

        countOfSubsets(arr, N, K);
    }
}
```

## 蟒蛇 3

```
# Function to find the maximum
# number of subsets into which
# the array can be split
def countOfSubsets(arr, N, K):

    # Stores the maximum number of
    # subsets
    count = 0
    pre = 1

    # Sort the given array
    arr.sort()

    # Iterate over the range [0, N]
    for i in range(N):

        # If current subset satisfies
        # the given condition
        if arr[i] * pre >= K:
            count = count + 1
            pre = 1

        # Otherwise, increment pre
        else:
            pre = pre + 1
    print(count)

# Driver code
arr = [1, 5, 4, 2, 3]
N = 5
K = 2
countOfSubsets(arr, N, K)

# This code is contributed by maddler.
```

## C#

```
// C# program for the above approach

using System;
using System.Collections.Generic;

class GFG{

// Function to find the maximum
// number of subsets into which
// the array can be split
static void countOfSubsets(int []arr, int N,
                    int K)
{
    // Stores the maximum number of
    // subsets
    int count = 0;
    int pre = 1;

    // Sort the given array
    Array.Sort(arr);

    // Iterate over the range [0, N]
    for (int i = 0; i < N; i++) {

        // If current subset satisfies
        // the given condition
        if (arr[i] * pre >= K) {
            count++;
            pre = 1;
        }

        // Otherwise, increment pre
        else {
            pre++;
        }
    }

    Console.Write(count);
}

// Driver Code
public static void Main()
{
    int []arr = { 1, 5, 4, 2, 3 };
    int K = 2;
    int N = arr.Length;
    countOfSubsets(arr, N, K);
}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach;

        // Function to find the maximum
        // number of subsets into which
        // the array can be split
        function countOfSubsets(arr, N,
            K) {
            // Stores the maximum number of
            // subsets
            let count = 0;
            let pre = 1;

            // Sort the given array
            arr.sort(function (a, b) { return a - b });

            // Iterate over the range [0, N]
            for (let i = 0; i < N; i++) {

                // If current subset satisfies
                // the given condition
                if (arr[i] * pre >= K) {
                    count++;
                    pre = 1;
                }

                // Otherwise, increment pre
                else {
                    pre++;
                }
            }

            document.write(count);
        }

        // Driver Code

        let arr = [1, 5, 4, 2, 3];
        let K = 2;
        let N = arr.length;

        countOfSubsets(arr, N, K);

   // This code is contributed by Potta Lokesh

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*