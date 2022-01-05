# 长度大于或等于 K 的非递减子阵列数量

> 原文:[https://www . geesforgeks . org/长度大于或等于 k 的非递减子数组数量/](https://www.geeksforgeeks.org/number-of-non-decreasing-sub-arrays-of-length-greater-than-or-equal-to-k/)

给定一个由 **N** 元素组成的数组 **arr[]** 和一个整数 **K** ，任务是找出长度大于或等于 **K** 的非递减子数组的数量。
**举例:**

> **输入:** arr[] = {1，2，3}，K = 2
> **输出:** 3
> {1，2}、{2，3}和{1，2，3}是有效的子阵。
> **输入:** arr[] = {3，2，1}，K = 1
> **输出:** 3

**朴素方法:**简单的方法是生成所有长度大于等于 **K** 的子阵列，然后检查子阵列是否满足条件。因此，该方法的时间复杂度将是 **O(N <sup>3</sup> )** 。
**有效方法:**更好的方法是使用[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)。

*   对于任何索引 **i** ，找到最大的索引 **j** ，使得子数组**arr【I…j】**不递减。这可以通过简单地增加 **j** 的值来实现，从 **i + 1** 开始，检查**arr【j】**是否大于**arr【j–1】**。
*   假设上一步找到的子阵列长度为 **L** 。计算 **X = max(0，L–K+1)**和 **(X * (X + 1)) / 2** 将被添加到最终答案中。这是因为对于长度为 **L** 的数组，长度为 **≥ K** 的子数组个数。
    *   从第一个元素开始的子数组数量=**L–K+1 = X**。
    *   从第二个元素开始的子阵列数量=**L–K = X–1**。
    *   从第三个元素开始的子阵列数量=**L–K–1 = X–2**。
    *   以此类推，直到 0，即 **1 + 2 + 3 +..+ X = (X * (X + 1)) / 2** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the required count
int findCnt(int* arr, int n, int k)
{
    // To store the final result
    int ret = 0;

    // Two pointer loop
    int i = 0;
    while (i < n) {

        // Initialising j
        int j = i + 1;

        // Looping till the subarray increases
        while (j < n and arr[j] >= arr[j - 1])
            j++;
        int x = max(0, j - i - k + 1);

        // Update ret
        ret += (x * (x + 1)) / 2;

        // Update i
        i = j;
    }

    // Return ret
    return ret;
}

// Driver code
int main()
{
    int arr[] = { 5, 4, 3, 2, 1 };
    int n = sizeof(arr) / sizeof(int);
    int k = 2;

    cout << findCnt(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the required count
static int findCnt(int []arr, int n, int k)
{
    // To store the final result
    int ret = 0;

    // Two pointer loop
    int i = 0;
    while (i < n)
    {

        // Initialising j
        int j = i + 1;

        // Looping till the subarray increases
        while (j < n && arr[j] >= arr[j - 1])
            j++;
        int x = Math.max(0, j - i - k + 1);

        // Update ret
        ret += (x * (x + 1)) / 2;

        // Update i
        i = j;
    }

    // Return ret
    return ret;
}

// Driver code
public static void main(String []args)
{
    int arr[] = { 5, 4, 3, 2, 1 };
    int n = arr.length;
    int k = 2;

    System.out.println(findCnt(arr, n, k));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the required count
def findCnt(arr, n, k) :

    # To store the final result
    ret = 0;

    # Two pointer loop
    i = 0;
    while (i < n) :

        # Initialising j
        j = i + 1;

        # Looping till the subarray increases
        while (j < n and arr[j] >= arr[j - 1]) :
            j += 1;

        x = max(0, j - i - k);

        # Update ret
        ret += (x * (x + 1)) / 2;

        # Update i
        i = j;

    # Return ret
    return ret;

# Driver code
if __name__ == "__main__" :

    arr = [ 5, 4, 3, 2, 1 ];
    n = len(arr);
    k = 2;

    print(findCnt(arr, n, k));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the required count
static int findCnt(int []arr, int n, int k)
{
    // To store the final result
    int ret = 0;

    // Two pointer loop
    int i = 0;
    while (i < n)
    {

        // Initialising j
        int j = i + 1;

        // Looping till the subarray increases
        while (j < n && arr[j] >= arr[j - 1])
            j++;
        int x = Math.Max(0, j - i - k + 1);

        // Update ret
        ret += (x * (x + 1)) / 2;

        // Update i
        i = j;
    }

    // Return ret
    return ret;
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 5, 4, 3, 2, 1 };
    int n = arr.Length;
    int k = 2;

    Console.WriteLine(findCnt(arr, n, k));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the required count
function findCnt(arr, n, k)
{
    // To store the final result
    var ret = 0;

    // Two pointer loop
    var i = 0;
    while (i < n) {

        // Initialising j
        var j = i + 1;

        // Looping till the subarray increases
        while (j < n && arr[j] >= arr[j - 1])
            j++;
        var x = Math.max(0, j - i - k + 1);

        // Update ret
        ret += (x * (x + 1)) / 2;

        // Update i
        i = j;
    }

    // Return ret
    return ret;
}

// Driver code
var arr = [5, 4, 3, 2, 1];
var n = arr.length;
var k = 2;
document.write( findCnt(arr, n, k));

</script>
```

**Output:** 

```
0
```