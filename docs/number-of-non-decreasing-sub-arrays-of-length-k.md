# 长度为 K 的非递减子阵列数量

> 原文:[https://www . geeksforgeeks . org/非递减长度子数组数量-k/](https://www.geeksforgeeks.org/number-of-non-decreasing-sub-arrays-of-length-k/)

给定一个长度为 **N** 的数组 **arr[]** ，任务是找到长度为 **K** 的非递减子数组的数量。
**举例:**

> **输入:** arr[] = {1，2，3，2，5}，K = 2
> **输出:** 3
> {1，2}，{2，3}和{2，5}是长度为 2 的递增
> 子阵。
> **输入:** arr[] = {1，2，3，2，5}，K = 1
> **输出:** 5

**天真法**生成长度为 **K** 的所有子阵列，然后检查子阵列是否满足条件。因此，该方法的时间复杂度将是 **O(N * K)** 。
**更好的方法:**更好的方法是使用[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)。假设现在的指数是 **i** 。

*   找到最大的索引 **j** ，这样子数组**arr【I…j】**是非递减的。这可以通过简单地从 **i + 1** 开始递增 **j** 的值并检查**arr【j】**是否大于**arr【j–1】**来实现。
*   假设上一步找到的子阵列长度为 **L** 。其中包含的长度为 **K** 的子阵列数量将为**最大值(L–K+1，0)** 。
*   现在，更新 **i = j** ，当 **i** 在指数范围内时，重复上述步骤。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of
// increasing subarrays of length k
int cntSubArrays(int* arr, int n, int k)
{
    // To store the final result
    int res = 0;

    int i = 0;
    // Two pointer loop
    while (i < n) {

        // Initialising j
        int j = i + 1;

        // Looping till the subarray increases
        while (j < n and arr[j] >= arr[j - 1])
            j++;

        // Updating the required count
        res += max(j - i - k + 1, 0);

        // Updating i
        i = j;
    }

    // Returning res
    return res;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 2, 5 };
    int n = sizeof(arr) / sizeof(int);
    int k = 2;

    cout << cntSubArrays(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count of
// increasing subarrays of length k
static int cntSubArrays(int []arr, int n, int k)
{
    // To store the final result
    int res = 0;

    int i = 0;

    // Two pointer loop
    while (i < n)
    {

        // Initialising j
        int j = i + 1;

        // Looping till the subarray increases
        while (j < n && arr[j] >= arr[j - 1])
            j++;

        // Updating the required count
        res += Math.max(j - i - k + 1, 0);

        // Updating i
        i = j;
    }

    // Returning res
    return res;
}

// Driver code
public static void main(String []args)
{
    int arr[] = { 1, 2, 3, 2, 5 };
    int n = arr.length;
    int k = 2;

    System.out.println(cntSubArrays(arr, n, k));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# increasing subarrays of length k
def cntSubArrays(arr, n, k) :

    # To store the final result
    res = 0;

    i = 0;

    # Two pointer loop
    while (i < n) :

        # Initialising j
        j = i + 1;

        # Looping till the subarray increases
        while (j < n and arr[j] >= arr[j - 1]) :
            j += 1;

        # Updating the required count
        res += max(j - i - k + 1, 0);

        # Updating i
        i = j;

    # Returning res
    return res;

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, 3, 2, 5 ];
    n = len(arr);
    k = 2;

    print(cntSubArrays(arr, n, k));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of
// increasing subarrays of length k
static int cntSubArrays(int []arr, int n, int k)
{
    // To store the final result
    int res = 0;

    int i = 0;

    // Two pointer loop
    while (i < n)
    {

        // Initialising j
        int j = i + 1;

        // Looping till the subarray increases
        while (j < n && arr[j] >= arr[j - 1])
            j++;

        // Updating the required count
        res += Math.Max(j - i - k + 1, 0);

        // Updating i
        i = j;
    }

    // Returning res
    return res;
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 1, 2, 3, 2, 5 };
    int n = arr.Length;
    int k = 2;

    Console.WriteLine(cntSubArrays(arr, n, k));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count of
// increasing subarrays of length k
function cntSubArrays(arr, n, k)
{
    // To store the final result
    var res = 0;

    var i = 0;
    // Two pointer loop
    while (i < n) {

        // Initialising j
        var j = i + 1;

        // Looping till the subarray increases
        while (j < n && arr[j] >= arr[j - 1])
            j++;

        // Updating the required count
        res += Math.max(j - i - k + 1, 0);

        // Updating i
        i = j;
    }

    // Returning res
    return res;
}

// Driver code
var arr = [ 1, 2, 3, 2, 5 ];
var n = arr.length;
var k = 2;
document.write( cntSubArrays(arr, n, k));

</script>
```

**Output:** 

```
3
```