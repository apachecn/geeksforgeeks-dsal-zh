# 大小为 K 的所有子阵列的比率

> 原文:[https://www . geeksforgeeks . org/全尺寸子阵列比率-k/](https://www.geeksforgeeks.org/ratio-of-all-subarrays-of-size-k/)

给定一个[阵列](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个整数 **K** ，任务是计算所有[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)大小 **K** 的比值。

**示例:**

> **输入:** arr[] = {24，3，2，1}，K = 3
> **输出:** 4 1.5
> **解释:**
> 大小为 K 的所有子阵列及其比例:
> 子阵列 1: {24，3，2} = 24 / 3 / 2 = 4
> 子阵列 2: {3，2，1} = 3 / 2 / 1= 1.5
> 
> **输入:** arr[] = {1，-2，3，-4，5，6}，K = 2
> T3】输出:-0.5-0.666667-0.75-0.8 0.833333

**方法:**想法是[迭代给定阵列中存在的大小为 K](https://www.geeksforgeeks.org/sum-of-all-subarrays-of-size-k/) 的每个子阵列，并按照以下步骤解决问题:

1.  初始化一个变量，用子阵列的第一个元素表示**比率**。
2.  迭代剩余的子阵列，并继续用遇到的元素逐个划分**比率**。
3.  最后，打印该子阵列的**比率**的最终值。
4.  对所有子阵列重复上述步骤。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the ratio of
// all subarrays of size K
int calcRatio(double arr[], int n, int k)
{

    // Traverse every subarray of size K
    for (int i = 0; i <= n - k; i++) {

        // Initialize ratio
        double ratio = arr[i];

        // Calculate ratio of the
        // current subarray
        for (int j = i + 1; j < k + i; j++)
            ratio /= arr[j];

        // Print ratio of the subarray
        cout << ratio << " ";
    }
}

// Driver Code
int main()
{
    // Given array
    double arr[] = { 24, 3, 2, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 3;

    // Function Call
    calcRatio(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG{

// Function to find the ratio of
// all subarrays of size K
static void calcRatio(double arr[], int n,
                                    int k)
{

    // Traverse every subarray of size K
    for(int i = 0; i <= n - k; i++)
    {

        // Initialize ratio
        double ratio = arr[i];

        // Calculate ratio of the
        // current subarray
        for(int j = i + 1; j < k + i; j++)
            ratio /= arr[j];

        // Print ratio of the subarray
        System.out.print(ratio + " ");
    }
}

// Driver code
public static void main (String[] args)
{

    // Given array
    double arr[] = { 24, 3, 2, 1 };
    int n = arr.length;
    int k = 3;

    // Function call
    calcRatio(arr, n, k);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation
# of the above approach

# Function to find the ratio of
# all subarrays of size K
def calcRatio(arr, n, k):

    # Traverse every subarray
    # of size K
    for i in range(n - k + 1):

        # Initialize ratio
        ratio = arr[i]

        # Calculate ratio of the
        # current subarray
        for j in range(i + 1, k + i):
            ratio = ratio / arr[j]

        # Print ratio of the subarray
        print(ratio, end = " ")

# Given array
arr = [24, 3, 2, 1]
n = len(arr)
k = 3

# Function Call
calcRatio(arr, n, k)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

// Function to find the ratio of
// all subarrays of size K
static void calcRatio(double []arr, int n,
                                    int k)
{

    // Traverse every subarray of size K
    for(int i = 0; i <= n - k; i++)
    {

        // Initialize ratio
        double ratio = arr[i];

        // Calculate ratio of the
        // current subarray
        for(int j = i + 1; j < k + i; j++)
            ratio /= arr[j];

        // Print ratio of the subarray
        Console.Write(ratio + " ");
    }
}

// Driver code
public static void Main(string[] args)
{

    // Given array
    double []arr = { 24, 3, 2, 1 };
    int n = arr.Length;
    int k = 3;

    // Function call
    calcRatio(arr, n, k);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to find the ratio of
// all subarrays of size K
function calcRatio(arr, n, k)
{

    // Traverse every subarray of size K
    for (var i = 0; i <= n - k; i++) {

        // Initialize ratio
        var ratio = arr[i];

        // Calculate ratio of the
        // current subarray
        for (var j = i + 1; j < k + i; j++)
            ratio /= arr[j];

        // Print ratio of the subarray
        document.write(ratio + " ");
    }
}

// Driver Code
// Given array
var arr = [ 24, 3, 2, 1 ];
var n = arr.length;
var k = 3;
// Function Call
calcRatio(arr, n, k);

</script>
```

**Output**

```
4 1.5 
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*