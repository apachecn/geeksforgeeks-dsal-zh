# 最小数除以数组中的最小元素数|集合 2

> 原文:[https://www . geesforgeks . org/最小数除法最小数组元素集数-2/](https://www.geeksforgeeks.org/smallest-number-dividing-minimum-number-of-elements-in-the-array-set-2/)

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
在本文中，将讨论一种使用筛子(M = max(arr))在 O(M*log(M) + N)时间内解决这个问题的方法。

*   首先，在数组中找到最大元素 **M** ，创建一个长度为 **M + 1** 的频率表**freq【】**，存储 **1** 到 **M** 之间数字的频率。
*   迭代数组并将每个索引 **i** 的 **freq[]** 更新为**freq[arr[I]]+**。
*   现在，应用筛选算法。迭代 **1** 到 **M + 1** 之间的所有元素。
    *   假设我们在迭代一个数字 **X** 。
    *   创建一个临时变量 **cnt** 。
    *   对于 **X** 和 **M** 之间的每个倍数的**X**{ X，2X，3X……。}将 cnt 更新为 **cnt = cnt + freq[kX]** 。
    *   如果 **cnt = 0** ，那么答案将是 **X** 否则继续迭代 **X** 的下一个值。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the smallest number
// that divides minimum number of elements
// in the given array
int findMin(int* arr, int n)
{
    // m stores the maximum in the array
    int m = 0;
    for (int i = 0; i < n; i++)
        m = max(m, arr[i]);

    // Frequency array
    int freq[m + 2] = { 0 };
    for (int i = 0; i < n; i++)
        freq[arr[i]]++;

    // Sieve
    for (int i = 1; i <= m + 1; i++) {
        int j = i;
        int cnt = 0;

        // Incrementing j
        while (j <= m) {
            cnt += freq[j];
            j += i;
        }

        // If no multiples of j are
        // in the array
        if (!cnt)
            return i;
    }

    return m + 1;
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
    // in the given array
    static int findMin(int arr[], int n)
    {
        // m stores the maximum in the array
        int m = 0;
        for (int i = 0; i < n; i++)
            m = Math.max(m, arr[i]);

        // Frequency array
        int freq [] = new int[m + 2];
        for (int i = 0; i < n; i++)
            freq[arr[i]]++;

        // Sieve
        for (int i = 1; i <= m + 1; i++)
        {
            int j = i;
            int cnt = 0;

            // Incrementing j
            while (j <= m)
            {
                cnt += freq[j];
                j += i;
            }

            // If no multiples of j are
            // in the array
            if (cnt == 0)
                return i;
        }
        return m + 1;
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
# in the given array
def findMin(arr, n):

    # m stores the maximum in the array
    m = 0
    for i in range(n):
        m = max(m, arr[i])

    # Frequency array
    freq = [0] * (m + 2)
    for i in range(n):
        freq[arr[i]] += 1

    # Sieve
    for i in range(1, m + 2):
        j = i
        cnt = 0

        # Incrementing j
        while (j <= m):
            cnt += freq[j]
            j += i

        # If no multiples of j are
        # in the array
        if (not cnt):
            return i

    return m + 1

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
    // in the given array
    static int findMin(int []arr, int n)
    {
        // m stores the maximum in the array
        int m = 0;
        for (int i = 0; i < n; i++)
            m = Math.Max(m, arr[i]);

        // Frequency array
        int []freq = new int[m + 2];
        for (int i = 0; i < n; i++)
            freq[arr[i]]++;

        // Sieve
        for (int i = 1; i <= m + 1; i++)
        {
            int j = i;
            int cnt = 0;

            // Incrementing j
            while (j <= m)
            {
                cnt += freq[j];
                j += i;
            }

            // If no multiples of j are
            // in the array
            if (cnt == 0)
                return i;
        }
        return m + 1;
    }

    // Driver code
    public static void Main ()
    {
        int []arr = { 2, 12, 6 };
        int n = arr.Length;

        Console.WriteLine(findMin(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the smallest number
// that divides minimum number of elements
// in the given array
function findMin(arr, n)
{
    // m stores the maximum in the array
    var m = 0;
    for (var i = 0; i < n; i++)
        m = Math.max(m, arr[i]);

    // Frequency array
    var freq = Array(m+2).fill(0);
    for (var i = 0; i < n; i++)
        freq[arr[i]]++;

    // Sieve
    for (var i = 1; i <= m + 1; i++) {
        var j = i;
        var cnt = 0;

        // Incrementing j
        while (j <= m) {
            cnt += freq[j];
            j += i;
        }

        // If no multiples of j are
        // in the array
        if (!cnt)
            return i;
    }

    return m + 1;
}

// Driver code
var arr = [2, 12, 6];
var n = arr.length;
document.write( findMin(arr, n));

</script>
```

**输出:**

```
5
```

**时间复杂度:** O(Mlog(M) + N)