# 求给定数组的峰值索引

> 原文:[https://www . geesforgeks . org/find-给定数组的峰值索引/](https://www.geeksforgeeks.org/find-the-peak-index-of-a-given-array/)

给定一个由 **N** ( *> 2* )整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到数组的峰值索引。如果数组不包含任何峰值索引，则打印 **-1** 。

> 由 **N** 个整数组成的给定数组**arr【】**的峰值指数，比如 **idx** 定义为:
> 
> *   0 < idx < N – 1
> *   arr[0] < arr[1] < arr[2] < …。< arr[idx] < …。< arr[N-2]< arr[N-1]

**示例:**

> **输入:** arr[] = {0，1，0}
> **输出:** 1
> **解释:**在索引 1 处的给定数组中，arr[0] < arr[1]和 arr[1] > arr[2]。由于索引 1 满足给定条件，因此 1 是数组的峰值索引。
> 
> **输入:** arr[] = {3，5，5，4，3，2，1}
> **输出:** -1

**天真法:**最简单的方法就是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)检查每个指标，比如说 **idx** ，在**【1，N–2】**的范围内是否指标 **idx** 可以是数组的峰值指标。这可以通过检查该索引 **idx** 左右的所有元素是否必须严格递增和严格递减来实现。检查所有索引后，如果存在任何这样的索引，则打印该索引。否则，打印**-1”**。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以基于这样的事实进行优化，即只有当数组包含严格递增的前缀和严格递减的后缀时，峰值索引才会存在。
按照以下步骤解决问题:

*   初始化两个变量，比如**和**，来存储数组峰值元素的索引。
*   [使用变量遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)的索引范围**【1，N–2】**，比如 **i** 。如果 **arr[i]** 的值大于或等于 **arr[i + 1]** ，则更新 **ans** 为**I**[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   如果**和**的值为 **0** 或**(N–1)**，则打印**-1”**，因为给定数组不存在这样的峰值索引。
*   现在，[使用变量 **i** 在范围**【ans，N–2】**内遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，如果 **arr[i]** 的值小于或等于 **arr[i + 1]** ，则[脱离循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   完成上述步骤后，如果 **i** 的值为**(N–1)**，则打印 **ans** 的值作为合成峰指数。否则，打印**-1”**，因为给定阵列不存在这样的峰值索引。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the peak
// index for the given array
int peakIndex(int arr[], int N)
{

    // Base Case
    if (N < 3)
        return -1;

    int i = 0;

    // Check for strictly
    // increasing array
    while (i + 1 < N)
    {

        // If the strictly increasing
        // condition is violated, then break
        if (arr[i + 1] < arr[i] ||
            arr[i] == arr[i + 1])
            break;

        i++;
    }

    if (i == 0 || i == N - 1)
        return -1;

    // Stores the value of i, which
    // is a potential peak index
    int ans = i;

    // Second traversal, for
    // strictly decreasing array
    while (i < N - 1)
    {

        // When the strictly
        // decreasing condition is
        // violated, then break
        if (arr[i] < arr[i + 1] ||
            arr[i] == arr[i + 1])
            break;

        i++;
    }

    // If i = N - 1, it means that
    // ans is the peak index
    if (i == N - 1)
        return ans;

    // Otherwise, peak index doesn't exist
    return -1;
}

// Driver Code
int main()
{
    int arr[] = { 0, 1, 0 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << peakIndex(arr, N) << "\n";

    return 0;
}

// This code is contributed by Kingash
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to find the peak
    // index for the given array
    public static int peakIndex(int[] arr)
    {
        int N = arr.length;

        // Base Case
        if (arr.length < 3)
            return -1;

        int i = 0;

        // Check for strictly
        // increasing array
        while (i + 1 < N) {

            // If the strictly increasing
            // condition is violated, then break
            if (arr[i + 1] < arr[i]
                || arr[i] == arr[i + 1])
                break;
            i++;
        }

        if (i == 0 || i == N - 1)
            return -1;

        // Stores the value of i, which
        // is a potential peak index
        int ans = i;

        // Second traversal, for
        // strictly decreasing array
        while (i < N - 1) {

            // When the strictly
            // decreasing condition is
            // violated, then break
            if (arr[i] < arr[i + 1]
                || arr[i] == arr[i + 1])
                break;
            i++;
        }

        // If i = N - 1, it means that
        // ans is the peak index
        if (i == N - 1)
            return ans;

        // Otherwise, peak index doesn't exist
        return -1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 0, 1, 0 };
        System.out.println(peakIndex(arr));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the peak
# index for the given array
def peakIndex(arr):

    N = len(arr)

    # Base Case
    if (len(arr) < 3):
        return -1

    i = 0

    # Check for strictly
    # increasing array
    while (i + 1 < N):

        # If the strictly increasing
        # condition is violated, then break
        if (arr[i + 1] < arr[i] or
            arr[i] == arr[i + 1]):
            break

        i += 1

    if (i == 0 or i == N - 1):
        return -1

    # Stores the value of i, which
    # is a potential peak index
    ans = i

    # Second traversal, for
    # strictly decreasing array
    while (i < N - 1):

        # When the strictly
        # decreasing condition is
        # violated, then break
        if (arr[i] < arr[i + 1] or
            arr[i] == arr[i + 1]):
            break

        i += 1

    # If i = N - 1, it means that
    # ans is the peak index
    if (i == N - 1):
        return ans

    # Otherwise, peak index doesn't exist
    return -1

# Driver Code
if __name__ == '__main__':

    arr = [0, 1, 0]

    print(peakIndex(arr))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the peak
// index for the given array
public static int peakIndex(int[] arr)
{
    int N = arr.Length;

    // Base Case
    if (arr.Length < 3)
        return -1;

    int i = 0;

    // Check for strictly
    // increasing array
    while (i + 1 < N)
    {

        // If the strictly increasing
        // condition is violated, then break
        if (arr[i + 1] < arr[i] ||
            arr[i] == arr[i + 1])
            break;

        i++;
    }

    if (i == 0 || i == N - 1)
        return -1;

    // Stores the value of i, which
    // is a potential peak index
    int ans = i;

    // Second traversal, for
    // strictly decreasing array
    while (i < N - 1)
    {

        // When the strictly
        // decreasing condition is
        // violated, then break
        if (arr[i] < arr[i + 1] ||
            arr[i] == arr[i + 1])
            break;

        i++;
    }

    // If i = N - 1, it means that
    // ans is the peak index
    if (i == N - 1)
        return ans;

    // Otherwise, peak index doesn't exist
    return -1;
}

// Driver Code
static public void Main()
{
    int[] arr = { 0, 1, 0 };

    Console.WriteLine(peakIndex(arr));
}
}

// This code is contributed by splevel62
```

## java 描述语言

```
<script>

// Javascript program for the above approach

    // Function to find the peak
    // index for the given array
    function peakIndex(arr)
    {
        var N = arr.length;

        // Base Case
        if (arr.length < 3)
            return -1;

        var i = 0;

        // Check for strictly
        // increasing array
        while (i + 1 < N) {

            // If the strictly increasing
            // condition is violated, then break
            if (arr[i + 1] < arr[i] || arr[i] == arr[i + 1])
                break;
            i++;
        }

        if (i == 0 || i == N - 1)
            return -1;

        // Stores the value of i, which
        // is a potential peak index
        var ans = i;

        // Second traversal, for
        // strictly decreasing array
        while (i < N - 1) {

            // When the strictly
            // decreasing condition is
            // violated, then break
            if (arr[i] < arr[i + 1] || arr[i] == arr[i + 1])
                break;
            i++;
        }

        // If i = N - 1, it means that
        // ans is the peak index
        if (i == N - 1)
            return ans;

        // Otherwise, peak index doesn't exist
        return -1;
    }

    // Driver Code

        var arr = [ 0, 1, 0 ];
        document.write(peakIndex(arr));

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)