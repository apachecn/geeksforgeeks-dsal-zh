# 最大可分对子集

> 原文:[https://www . geesforgeks . org/最大可分对子集/](https://www.geeksforgeeks.org/largest-divisible-pairs-subset/)

给定 n 个不同元素的数组，求最大子集的长度，使得子集中的每一对都可以被较小的元素整除。

**示例:**

```
Input : arr[] = {10, 5, 3, 15, 20} 
Output : 3 
Explanation: The largest subset is 10, 5, 20.
10 is divisible by 5, and 20 is divisible by 10.

Input : arr[] = {18, 1, 3, 6, 13, 17} 
Output : 4
Explanation: The largest subset is 18, 1, 3, 6,
In the subsequence, 3 is divisible by 1, 
6 by 3 and 18 by 6.
```

这可以通过[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)解决。我们从头到尾遍历排序后的数组。对于每个元素 a[i]，我们计算 dp[i]，其中 dp[i]表示最大可分子集的大小，其中 a[i]是最小元素。我们可以使用从 dp[i+1]到 dp[n-1]的值来计算数组中的 dp[i]。最后，我们从 dp[]返回最大值。

下面是上述方法的实现:

## C++

```
// CPP program to find the largest subset which
// where each pair is divisible.
#include <bits/stdc++.h>
using namespace std;

// function to find the longest Subsequence
int largestSubset(int a[], int n)
{
    // dp[i] is going to store size of largest
    // divisible subset beginning with a[i].
    int dp[n];

    // Since last element is largest, d[n-1] is 1
    dp[n - 1] = 1;

    // Fill values for smaller elements.
    for (int i = n - 2; i >= 0; i--) {

        // Find all multiples of a[i] and consider
        // the multiple that has largest subset
        // beginning with it.
        int mxm = 0;
        for (int j = i + 1; j < n; j++)
            if (a[j] % a[i] == 0 || a[i] % a[j] == 0)
                mxm = max(mxm, dp[j]);

        dp[i] = 1 + mxm;
    }

    // Return maximum value from dp[]
    return *max_element(dp, dp + n);
}

// driver code to check the above function
int main()
{
    int a[] = { 1, 3, 6, 13, 17, 18 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << largestSubset(a, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Arrays;

// Java program to find the largest
// subset which was each pair
// is divisible.
class GFG {

    // function to find the longest Subsequence
    static int largestSubset(int[] a, int n)
    {
        // dp[i] is going to store size of largest
        // divisible subset beginning with a[i].
        int[] dp = new int[n];

        // Since last element is largest, d[n-1] is 1
        dp[n - 1] = 1;

        // Fill values for smaller elements.
        for (int i = n - 2; i >= 0; i--) {

            // Find all multiples of a[i] and consider
            // the multiple that has largest subset
            // beginning with it.
            int mxm = 0;
            for (int j = i + 1; j < n; j++) {
                if (a[j] % a[i] == 0 || a[i] % a[j] == 0) {
                    mxm = Math.max(mxm, dp[j]);
                }
            }

            dp[i] = 1 + mxm;
        }

        // Return maximum value from dp[]
        return Arrays.stream(dp).max().getAsInt();
    }

    // driver code to check the above function
    public static void main(String[] args)
    {
        int[] a = { 1, 3, 6, 13, 17, 18 };
        int n = a.length;
        System.out.println(largestSubset(a, n));
    }
}

/* This JAVA code is contributed by Rajput-Ji*/
```

## 蟒蛇 3

```
# Python program to find the largest
# subset where each pair is divisible.

# function to find the longest Subsequence
def largestSubset(a, n):

    # dp[i] is going to store size
    # of largest divisible subset
    # beginning with a[i].
    dp = [0 for i in range(n)]

    # Since last element is largest,
    # d[n-1] is 1
    dp[n - 1] = 1;

    # Fill values for smaller elements
    for i in range(n - 2, -1, -1):

        # Find all multiples of a[i]
        # and consider the multiple
        # that has largest subset    
        # beginning with it.
        mxm = 0;
        for j in range(i + 1, n):
            if a[j] % a[i] == 0 or a[i] % a[j] == 0:
                mxm = max(mxm, dp[j])
        dp[i] = 1 + mxm

    # Return maximum value from dp[]
    return max(dp)

# Driver Code
a = [ 1, 3, 6, 13, 17, 18 ]
n = len(a)
print(largestSubset(a, n))

# This code is contributed by
# sahil shelangia
```

## C#

```
// C# program to find the largest
// subset which where each pair
// is divisible.
using System;
using System.Linq;

public class GFG {

    // function to find the longest Subsequence
    static int largestSubset(int[] a, int n)
    {
        // dp[i] is going to store size of largest
        // divisible subset beginning with a[i].
        int[] dp = new int[n];

        // Since last element is largest, d[n-1] is 1
        dp[n - 1] = 1;

        // Fill values for smaller elements.
        for (int i = n - 2; i >= 0; i--) {

            // Find all multiples of a[i] and consider
            // the multiple that has largest subset
            // beginning with it.
            int mxm = 0;
            for (int j = i + 1; j < n; j++)
                if (a[j] % a[i] == 0 | a[i] % a[j] == 0)
                    mxm = Math.Max(mxm, dp[j]);

            dp[i] = 1 + mxm;
        }

        // Return maximum value from dp[]
        return dp.Max();
    }

    // driver code to check the above function
    static public void Main()
    {
        int[] a = { 1, 3, 6, 13, 17, 18 };
        int n = a.Length;
        Console.WriteLine(largestSubset(a, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// largest subset which
// where each pair is
// divisible.

// function to find the
// longest Subsequence
function largestSubset($a, $n)
{
    // dp[i] is going to
    // store size of largest
    // divisible subset
    // beginning with a[i].
    $dp = array();

    // Since last element is
    // largest, d[n-1] is 1
    $dp[$n - 1] = 1;

    // Fill values for
    // smaller elements.
    for ($i = $n - 2; $i >= 0; $i--)
    {

        // Find all multiples of
        // a[i] and consider
        // the multiple that
        // has largest subset
        // beginning with it.
        $mxm = 0;
        for ($j = $i + 1; $j < $n; $j++)
            if ($a[$j] % $a[$i] == 0 or $a[$i] % $a[$j] == 0)
                $mxm = max($mxm, $dp[$j]);

        $dp[$i] = 1 + $mxm;
    }

    // Return maximum value
    // from dp[]
    return max($dp);
}

    // Driver Code
    $a = array(1, 3, 6, 13, 17, 18);
    $n = count($a);
    echo largestSubset($a, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to find the largest
// subset which was each pair
// is divisible.

// Function to find the longest Subsequence
function largestSubset(a, n)
{

    // dp[i] is going to store size of largest
    // divisible subset beginning with a[i].
    let dp = [];

    // Since last element is largest, d[n-1] is 1
    dp[n - 1] = 1;

    // Fill values for smaller elements.
    for(let i = n - 2; i >= 0; i--)
    {

        // Find all multiples of a[i] and consider
        // the multiple that has largest subset
        // beginning with it.
        let mxm = 0;
        for(let j = i + 1; j < n; j++)
        {
            if (a[j] % a[i] == 0 ||
                a[i] % a[j] == 0)
            {
                mxm = Math.max(mxm, dp[j]);
            }
        }
        dp[i] = 1 + mxm;
    }

    // Return maximum value from dp[]
    return Math.max(...dp);
}

// Driver code
let a = [ 1, 3, 6, 13, 17, 18 ];
let n = a.length;

document.write(largestSubset(a, n));

// This code is contributed by sanjoy_62

</script>
```

**输出:**

```
4
```

**时间复杂度:** O(n*n)