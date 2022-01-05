# 最小数除以数组中的最小元素数

> 原文:[https://www . geesforgeks . org/最小数除法最小数组元素数/](https://www.geeksforgeeks.org/smallest-number-dividing-minimum-number-of-elements-in-the-array/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是从数组中找出除以元素最小个数的最小数。
**例:**

> **输入:** arr[] = {2，12，6}
> **输出:** 5
> 这里，1 除 3 元素
> 2 除 3 元素
> 3 除 2 元素
> 4 除 1 元素
> 5 除无元素
> 6 除 2 元素
> 7 除无元素
> 8 除无元素
> 9 除无元素
> 10 除无元素
> 11 除无元素
> 12 除因此，ans = 5
> **输入:** arr[] = {1，7，9}
> **输出:** 2

**进场:**先观察一些细节。除零元素的数字已经存在，即 **max(arr) + 1** 。现在，我们只需要找到数组中除以零的最小数。
在本文中，将讨论使用平方根因子分解解决这个问题的方法。将对每个元素进行因子分解，并保持长度为 **max(arr) + 2** 的频率数组 **cnt[]** ，以存储数组中多个元素的计数，每个元素位于 **1** 至 **max(arr) + 1** 之间。

*   对于每个 **i** ，因子分解**arr【I】**。
*   对于**arr【I】**的每个因子 **Fij** ，更新**CNT【Fij】**为**CNT【Fij】++**。
*   用 **cnt[k] = 0** 求频率数组 **cnt[]** 中的最小数 **k** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the smallest number
// that divides minimum number of elements
int findMin(int* arr, int n)
{
    // m stores the maximum in the array
    int m = 0;
    for (int i = 0; i < n; i++)
        m = max(m, arr[i]);

    // Frequency table
    int cnt[m + 2] = { 0 };

    // Loop to factorize
    for (int i = 0; i < n; i++) {

        // sqrt factorization of the numbers
        for (int j = 1; j * j <= arr[i]; j++) {
            if (arr[i] % j == 0) {
                if (j * j == arr[i])
                    cnt[j]++;
                else
                    cnt[j]++, cnt[arr[i] / j]++;
            }
        }
    }

    // Finding the smallest number
    // with zero multiples
    for (int i = 1; i <= m + 1; i++)
        if (cnt[i] == 0) {
            return i;
        }

    return -1;
}

// Driver code
int main()
{
    int arr[] = { 2, 12, 6 };
    int n = sizeof(arr) / sizeof(int);

    cout << findMin(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the smallest number
    // that divides minimum number of elements
    static int findMin(int arr[], int n)
    {
        // m stores the maximum in the array
        int m = 0;
        for (int i = 0; i < n; i++)
            m = Math.max(m, arr[i]);

        // Frequency table
        int cnt[] = new int[m + 2];

        // Loop to factorize
        for (int i = 0; i < n; i++)
        {

            // sqrt factorization of the numbers
            for (int j = 1; j * j <= arr[i]; j++)
            {
                if (arr[i] % j == 0)
                {
                    if (j * j == arr[i])
                        cnt[j]++;
                    else
                    {
                        cnt[j]++;
                        cnt[arr[i] / j]++;
                    }
                }
            }
        }

        // Finding the smallest number
        // with zero multiples
        for (int i = 1; i <= m + 1; i++)
            if (cnt[i] == 0)
            {
                return i;
            }
        return -1;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 2, 12, 6 };
        int n = arr.length;

        System.out.println(findMin(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the smallest number
# that divides minimum number of elements
def findMin(arr, n):

    # m stores the maximum in the array
    m = 0
    for i in range(n):
        m = max(m, arr[i])

    # Frequency table
    cnt = [0] * (m + 2)

    # Loop to factorize
    for i in range(n):

        # sqrt factorization of the numbers
        j = 1
        while j * j <= arr[i]:

            if (arr[i] % j == 0):
                if (j * j == arr[i]):
                    cnt[j] += 1
                else:
                    cnt[j] += 1
                    cnt[arr[i] // j] += 1
            j += 1   

    # Finding the smallest number
    # with zero multiples
    for i in range(1, m + 2):
        if (cnt[i] == 0):
            return i

    return -1

# Driver code
arr = [2, 12, 6]
n = len(arr)

print(findMin(arr, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the smallest number
    // that divides minimum number of elements
    static int findMin(int []arr, int n)
    {
        // m stores the maximum in the array
        int m = 0;
        for (int i = 0; i < n; i++)
            m = Math.Max(m, arr[i]);

        // Frequency table
        int []cnt = new int[m + 2];

        // Loop to factorize
        for (int i = 0; i < n; i++)
        {

            // sqrt factorization of the numbers
            for (int j = 1; j * j <= arr[i]; j++)
            {
                if (arr[i] % j == 0)
                {
                    if (j * j == arr[i])
                        cnt[j]++;
                    else
                    {
                        cnt[j]++;
                        cnt[arr[i] / j]++;
                    }
                }
            }
        }

        // Finding the smallest number
        // with zero multiples
        for (int i = 1; i <= m + 1; i++)
            if (cnt[i] == 0)
            {
                return i;
            }
        return -1;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = { 2, 12, 6 };
        int n = arr.Length;

        Console.WriteLine(findMin(arr, n));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the smallest number
// that divides minimum number of elements
function findMin(arr, n)
{
    // m stores the maximum in the array
    var m = 0;
    for (var i = 0; i < n; i++)
        m = Math.max(m, arr[i]);

    // Frequency table
    var cnt = Array(m+2).fill(0);

    // Loop to factorize
    for (var i = 0; i < n; i++) {

        // sqrt factorization of the numbers
        for (var j = 1; j * j <= arr[i]; j++) {
            if (arr[i] % j == 0) {
                if (j * j == arr[i])
                    cnt[j]++;
                else
                    cnt[j]++, cnt[arr[i] / j]++;
            }
        }
    }

    // Finding the smallest number
    // with zero multiples
    for (var i = 1; i <= m + 1; i++)
        if (cnt[i] == 0) {
            return i;
        }

    return -1;
}

// Driver code
var arr = [2, 12, 6];
var n = arr.length;
document.write( findMin(arr, n));

</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(N * sqrt(max(arr)))。