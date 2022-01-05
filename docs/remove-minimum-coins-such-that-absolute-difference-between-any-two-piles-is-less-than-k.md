# 取出最小硬币，使任意两堆硬币的绝对差值小于 K

> 原文:[https://www . geesforgeks . org/remove-minimum-coins-so-任何两堆硬币的绝对差值小于-k/](https://www.geeksforgeeks.org/remove-minimum-coins-such-that-absolute-difference-between-any-two-piles-is-less-than-k/)

给定一个数组，大小为 **N** 的 **arr[]** 和一个整数 K，表示有 **N** 堆硬币，第**I<sup>th</sup>T9】包含**arr【I】**硬币。任务是调整每堆硬币的数量，如果 **a** 是第一堆硬币的数量， **b** 是第二堆硬币的数量，则**| a–b |≤K**。
可以从不同的堆中取出硬币来减少那些堆中的硬币数量，但不能通过增加更多的硬币来增加一堆中的硬币数量。找出满足给定条件需要移除的最小硬币数量。**

**示例:**

> **输入:** arr[] = {2，2，2，2}，K = 0
> **输出:** 0
> 对于任意两堆硬币，硬币数量之差≤ 0。
> 所以，不需要移除任何硬币。
> **输入:** arr[] = {1，5，1，2，5，1}，K = 3
> **输出:** 2
> 如果我们从包含
> 5 枚硬币的两堆中各取出一枚硬币，那么对于任意两堆而言，硬币数量的绝对差异
> 为≤ 3 枚。

**进场:**既然我们不能增加一堆硬币的数量。所以，任何一堆硬币的最小数量将保持不变，因为它们不能被移除，增加它们将增加我们需要最小化的操作。现在，找到一堆中的最小硬币，对于每隔一堆，如果当前堆中的硬币和最小硬币堆之间的差异大于 K，则从当前堆中移除多余的硬币。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum number
// of coins that need to be removed
int minimumCoins(int a[], int n, int k)
{
    // To store the coins needed to be removed
    int cnt = 0;

    // Minimum value from the array
    int minVal = *min_element(a, a + n);

    // Iterate over the array
    // and remove extra coins
    for (int i = 0; i < n; i++)
    {
        int diff = a[i] - minVal;

        // If the difference between
        //  the current pile and the
        // minimum coin pile is greater than k
        if (diff > k)
        {

            // Count the extra coins to be removed
            cnt += (diff - k);
        }
    }

    // Return the required count
    return cnt;
}

// Driver code
int main()
{
    int a[] = { 1, 5, 1, 2, 5, 1 };
    int n = sizeof(a) / sizeof(a[0]);
    int k = 3;

    cout << minimumCoins(a, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG {

    // Function to return the minimum number
    // of coins that need to be removed
    static int min_val(int[] a)
    {
        int min = 2147483647;
        for (int el : a) {
            if (el < min) {
                min = el;
            }
        }
        return min;
    }
    static int minimumCoins(int a[], int n, int k)
    {
        // To store the coins needed to be removed
        int cnt = 0;

        // Minimum value from the array
        int minVal = min_val(a);

        // Iterate over the array and remove extra coins
        for (int i = 0; i < n; i++) {
            int diff = a[i] - minVal;

            // If the difference between the current pile
            // and the minimum coin pile is greater than k
            if (diff > k) {
                // Count the extra coins to be removed
                cnt += (diff - k);
            }
        }

        // Return the required count
        return cnt;
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[] = { 1, 5, 1, 2, 5, 1 };
        int n = a.length;
        int k = 3;
        System.out.println(minimumCoins(a, n, k));
    }
}

// This code is contributed by jit_t
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function to return the minimum number
# of coins that need to be removed
def minimumCoins(a, n, k):
    # To store the coins needed to be removed
    cnt = 0;

    # Minimum value from the array
    minVal = min(a);

    # Iterate over the array and remove extra coins
    for i in range(n):
        diff = a[i] - minVal;

        # If the difference between the current pile and
        # the minimum coin pile is greater than k
        if (diff > k):
            # Count the extra coins to be removed
            cnt += (diff - k);
    # Return the required count
    return cnt;

# Driver code
a = [1, 5, 1, 2, 5, 1];
n = len(a);
k = 3;
print(minimumCoins(a, n, k));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    // Function to return the minimum number
    // of coins that need to be removed
    static int min_val(int[] a, int n)
    {
        int min = 2147483647;
        for (int i = 0;i<n;i++)
        {
            int el = a[i];
            if (el < min)
            {
                min = el;
            }
        }
        return min;
    }

    // Function to return the minimum number
    // of coins that need to be removed
    static int minimumCoins(int[] a, int n, int k)
    {
        // To store the coins needed to be removed
        int cnt = 0;

        // Minimum value from the array
        int minVal = min_val(a, n);

        // Iterate over the array and remove extra coins
        for (int i = 0; i < n; i++)
        {
            int diff = a[i] - minVal;

            // If the difference between the current pile
            // and the minimum coin pile is greater than k
            if (diff > k)
            {
                // Count the extra coins to be removed
                cnt += (diff - k);
            }
        }

        // Return the required count
        return cnt;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] a = { 1, 5, 1, 2, 5, 1 };
        int n = a.Length;
        int k = 3;
        Console.WriteLine(minimumCoins(a, n, k));
    }
}

/* This code is contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    // Function to return the minimum number
    // of coins that need to be removed
    function min_val(a, n)
    {
        let min = 2147483647;
        for (let i = 0;i<n;i++)
        {
            let el = a[i];
            if (el < min)
            {
                min = el;
            }
        }
        return min;
    }

    // Function to return the minimum number
    // of coins that need to be removed
    function minimumCoins(a, n, k)
    {
        // To store the coins needed to be removed
        let cnt = 0;

        // Minimum value from the array
        let minVal = min_val(a, n);

        // Iterate over the array and remove extra coins
        for (let i = 0; i < n; i++)
        {
            let diff = a[i] - minVal;

            // If the difference between the current pile
            // and the minimum coin pile is greater than k
            if (diff > k)
            {
                // Count the extra coins to be removed
                cnt += (diff - k);
            }
        }

        // Return the required count
        return cnt;
    }

    let a = [ 1, 5, 1, 2, 5, 1 ];
    let n = a.length;
    let k = 3;
    document.write(minimumCoins(a, n, k));

</script>
```

**Output**

```
2
```