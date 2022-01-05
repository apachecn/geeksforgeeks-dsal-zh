# 计数秩不超过 K 的数组元素

> 原文:[https://www . geeksforgeeks . org/count-array-elements-with-rank-under-k/](https://www.geeksforgeeks.org/count-array-elements-with-rank-not-exceeding-k/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找出排名最多的数组元素的数量 **K** 。

> 相等的数组元素将具有相等的等级。任何数值小于其紧邻的大数组元素的数组元素将比大于它的数组元素总数多一个。

**示例:**

> **输入:** N = 4，arr[] = {100，50，50，25}，K = 3
> **输出** : 3
> **说明:**玩家的排名将为{1，2，2，4}。
> 数组元素有 3 个，行列小于等于 3。
> 所以，答案是 3。
> 
> **输入:** N = 5，arr[] = {2，2，3，4，5}，K = 4
> **输出:** 5
> **说明:**玩家的排名将为{4，4，3，2，1}。
> 有 5 个数组元素，其行列小于或等于 4。
> 所以，答案是 5。

**天真法:**最简单的方法就是在数组中找到当前的[最大元素，并与之前的最大元素进行比较。如果它们相等，那么前一个元素和当前元素的等级必须相等。否则，将当前最大值元素的等级指定为比先前获得的最大值数目大一。重复此操作，直到给定数组变为空或等级大于 **K** ，以较早者为准。遍历后，打印已删除元素的总数。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效方法:**思路是使用[排序算法](https://www.geeksforgeeks.org/sorting-algorithms/)。在[以非递增顺序](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)对给定数组进行排序后，对于每个元素，如果当前元素和前一个元素不相等，则当前元素的[等级必须比前一个元素大一级。否则，它将保持与前一个相同。按照以下步骤解决问题:](https://www.geeksforgeeks.org/find-relative-rank-of-each-element-in-array/)

*   [按升序排列给定的**arr【】**。](https://www.geeksforgeeks.org/sorting-algorithms/)
*   用 **1** 初始化变量**秩**和**位置**，分别存储当前数组元素的秩和位置。
*   [从**I =(N–1)**到 **0** 遍历排序后的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并执行以下操作:
    *   当相邻数组元素不相等或当 **i** 等于**(N–1)**时，用**位置**更新**等级。**
    *   如果等级大于 **K** ，返回**位置–1**。
    *   在每次遍历中增加**位置**。
*   打印 **N** ，如果所有数组元素的等级都不超过 **K** 。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find count of array
// elements with rank less than or
// equal to k
int rankLessThanK(int* arr, int k, int n)
{

    // Initialize rank and position
    int rank = 1;
    int position = 1;

    // Sort the given array
    sort(arr, arr + n);

    // Traverse array from right to left
    for(int i = n - 1; i >= 0; i--)
    {

        // Update rank with position, if
        // adjacent elements are unequal
        if (i == n - 1 || arr[i] != arr[i + 1])
        {
            rank = position;

            // Return position - 1, if
            // rank greater than k
            if (rank > k)
                return position - 1;
        }

        // Increase position
        position++;
    }
    return n;
}

// Driver Code
int main()
{

    // Given array
    int arr[5] = { 2, 2, 3, 4, 5 };

    int N = 5;

    // Given K
    int K = 4;

    // Function Call
    cout << rankLessThanK(arr, K, N);

    return 0;
}

// This code is contributed by hemanth gadarla
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;
import java.lang.*;
class GFG {

    // Function to find count of array
    // elements with rank less than or
    // equal to k
    static int rankLessThanK(int[] arr,
                             int k, int n)
    {
        // Initialize rank and position
        int rank = 1;
        int position = 1;

        // Sort the given array
        Arrays.sort(arr);

        // Traverse array from right to left
        for (int i = n - 1; i >= 0; i--) {

            // Update rank with position, if
            // adjacent elements are unequal
            if (i == n - 1
                || arr[i] != arr[i + 1]) {

                rank = position;

                // Return position - 1, if
                // rank greater than k
                if (rank > k)
                    return position - 1;
            }

            // Increase position
            position++;
        }

        return n;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array
        int arr[] = { 2, 2, 3, 4, 5 };

        int N = arr.length;

        // Given K
        int K = 4;

        // Function Call
        System.out.println(
            rankLessThanK(arr, K, N));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to find count of
# array elements with rank
# less than or equal to k
def rankLessThanK(arr, k, n):

    # Initialize rank and
    # position
    rank = 1;
    position = 1;

    # Sort the given array
    arr = sorted(arr)

    # Traverse array from
    # right to left
    for i in range(n - 1,
                   -1, -1):

        # Update rank with position,
        # if adjacent elements are
        # unequal
        if (i == n - 1 or
            arr[i] != arr[i + 1]):
            rank = position;

            # Return position - 1, if
            # rank greater than k
            if (rank > k):
                return position - 1;

        # Increase position
        position += 1;

    return n;

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [2, 2, 3, 4, 5];

    N = len(arr);

    # Given K
    K = 4;

    # Function Call
    print(rankLessThanK(arr, K, N));

# This code is contributed by gauravrajput1
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find count of array
// elements with rank less than or
// equal to k
static int rankLessThanK(int[] arr,
                         int k, int n)
{

    // Initialize rank and position
    int rank = 1;
    int position = 1;

    // Sort the given array
    Array.Sort(arr);

    // Traverse array from right to left
    for(int i = n - 1; i >= 0; i--)
    {

        // Update rank with position, if
        // adjacent elements are unequal
        if (i == n - 1 || arr[i] != arr[i + 1])
        {
            rank = position;

            // Return position - 1, if
            // rank greater than k
            if (rank > k)
                return position - 1;
        }

        // Increase position
        position++;
    }
    return n;
}      

// Driver Code
public static void Main()
{

    // Given array
    int[] arr = { 2, 2, 3, 4, 5 };

    int N = arr.Length;

    // Given K
    int K = 4;

    // Function Call
    Console.WriteLine(rankLessThanK(
        arr, K, N));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find count of array
// elements with rank less than or
// equal to k
function rankLessThanK(arr, k, n)
{

    // Initialize rank and position
    let rank = 1;
    let position = 1;

    // Sort the given array
    arr.sort();

    // Traverse array from right to left
    for(let i = n - 1; i >= 0; i--)
    {

        // Update rank with position, if
        // adjacent elements are unequal
        if (i == n - 1 || arr[i] != arr[i + 1])
        {
            rank = position;

            // Return position - 1, if
            // rank greater than k
            if (rank > k)
                return position - 1;
        }

        // Increase position
        position++;
    }
    return n;
}

// Driver code

// Given array
let arr = [ 2, 2, 3, 4, 5 ];
let N = arr.length;

// Given K
let K = 4;

// Function Call
document.write(rankLessThanK(arr, K, N));

// This code is contributed by splevel62   

</script>
```

**Output**

```
5
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*