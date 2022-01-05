# 移除数组末端的最小元素，使总和至少减少 K | O(N)

> 原文:[https://www . geeksforgeeks . org/从数组末尾移除最小元素，以便总和至少减少 k/on/](https://www.geeksforgeeks.org/remove-minimum-elements-from-ends-of-array-so-that-sum-decreases-by-at-least-k-on/)

给定一个由 **N** 元素组成的数组 **arr[]** ，任务是从数组的末端移除最少数量的元素，使得数组的总和至少减少 **K** 。**注意****K**将始终小于或等于数组所有元素的和。
**举例:**

> **输入:** arr[] = {1，11，5，5}，K = 11
> **输出:** 2
> 从左侧
> 端去掉两个元素后，总和减 1 + 11 = 12。
> 于是，答案是 2。
> **输入:** arr[] = {1，2，3}，K = 6
> **输出:** 3

**方法:**基于[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)的方法已经在另一篇文章中讨论过了。在本文中，将讨论使用[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)的方法。可以观察到，任务是找到最长的子阵列，其元素之和最多**sum(arr)–K**，其中 **sum(arr)** 是阵列所有元素之和 **arr[]** 。
让这种子阵列的长度为 **L** 。因此，要从阵列中移除的元素的最小数量将等于**N–L**。要找到这种子阵列最长的长度，请参考本文[。](https://www.geeksforgeeks.org/longest-subarray-sum-elements-atmost-k/)
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of minimum
// elements to be removed from the ends
// of the array such that the sum of the
// array decrease by at least K
int minCount(int* arr, int n, int k)
{

    // To store the final answer
    int ans = 0;

    // Maximum possible sum required
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];
    sum -= k;

    // Left point
    int l = 0;

    // Right pointer
    int r = 0;

    // Total current sum
    int tot = 0;

    // Two pointer loop
    while (l < n) {

        // If the sum fits
        if (tot <= sum) {

            // Update the answer
            ans = max(ans, r - l);
            if (r == n)
                break;

            // Update the total sum
            tot += arr[r++];
        }

        else {

            // Increment the left pointer
            tot -= arr[l++];
        }
    }

    return (n - ans);
}

// Driver code
int main()
{
    int arr[] = { 1, 11, 5, 5 };
    int n = sizeof(arr) / sizeof(int);
    int k = 11;

    cout << minCount(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the count of minimum
    // elements to be removed from the ends
    // of the array such that the sum of the
    // array decrease by at least K
    static int minCount(int arr[],
                        int n, int k)
    {

        // To store the final answer
        int ans = 0;

        // Maximum possible sum required
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += arr[i];
        sum -= k;

        // Left point
        int l = 0;

        // Right pointer
        int r = 0;

        // Total current sum
        int tot = 0;

        // Two pointer loop
        while (l < n)
        {

            // If the sum fits
            if (tot <= sum)
            {

                // Update the answer
                ans = Math.max(ans, r - l);
                if (r == n)
                    break;

                // Update the total sum
                tot += arr[r++];
            }
            else
            {

                // Increment the left pointer
                tot -= arr[l++];
            }
        }
        return (n - ans);
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 1, 11, 5, 5 };
        int n = arr.length;
        int k = 11;

        System.out.println(minCount(arr, n, k));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of minimum
# elements to be removed from the ends
# of the array such that the sum of the
# array decrease by at least K
def minCount(arr, n, k) :

    # To store the final answer
    ans = 0;

    # Maximum possible sum required
    sum = 0;
    for i in range(n) :
        sum += arr[i];
    sum -= k;

    # Left point
    l = 0;

    # Right pointer
    r = 0;

    # Total current sum
    tot = 0;

    # Two pointer loop
    while (l < n) :

        # If the sum fits
        if (tot <= sum) :

            # Update the answer
            ans = max(ans, r - l);
            if (r == n) :
                break;

            # Update the total sum
            tot += arr[r];
            r += 1

        else :

            # Increment the left pointer
            tot -= arr[l];
            l += 1

    return (n - ans);

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 11, 5, 5 ];
    n = len(arr);
    k = 11;

    print(minCount(arr, n, k));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the count of minimum
    // elements to be removed from the ends
    // of the array such that the sum of the
    // array decrease by at least K
    static int minCount(int []arr,
                        int n, int k)
    {

        // To store the final answer
        int ans = 0;

        // Maximum possible sum required
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += arr[i];
        sum -= k;

        // Left point
        int l = 0;

        // Right pointer
        int r = 0;

        // Total current sum
        int tot = 0;

        // Two pointer loop
        while (l < n)
        {

            // If the sum fits
            if (tot <= sum)
            {

                // Update the answer
                ans = Math.Max(ans, r - l);
                if (r == n)
                    break;

                // Update the total sum
                tot += arr[r++];
            }
            else
            {

                // Increment the left pointer
                tot -= arr[l++];
            }
        }
        return (n - ans);
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 1, 11, 5, 5 };
        int n = arr.Length;
        int k = 11;

        Console.WriteLine(minCount(arr, n, k));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the count of minimum
// elements to be removed from the ends
// of the array such that the sum of the
// array decrease by at least K
function minCount(arr, n, k)
{

    // To store the final answer
    var ans = 0;

    // Maximum possible sum required
    var sum = 0;
    for (var i = 0; i < n; i++)
        sum += arr[i];
    sum -= k;

    // Left point
    var l = 0;

    // Right pointer
    var r = 0;

    // Total current sum
    var tot = 0;

    // Two pointer loop
    while (l < n) {

        // If the sum fits
        if (tot <= sum) {

            // Update the answer
            ans = Math.max(ans, r - l);
            if (r == n)
                break;

            // Update the total sum
            tot += arr[r++];
        }

        else {

            // Increment the left pointer
            tot -= arr[l++];
        }
    }

    return (n - ans);
}

// Driver code
var arr = [1, 11, 5, 5 ];
var n = arr.length;
var k = 11;
document.write( minCount(arr, n, k));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
2
```