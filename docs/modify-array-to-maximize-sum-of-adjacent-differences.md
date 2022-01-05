# 修改数组，使相邻差之和最大化

> 原文:[https://www . geesforgeks . org/modify-array-to-maximize-sum-of-neighbor-difference/](https://www.geeksforgeeks.org/modify-array-to-maximize-sum-of-adjacent-differences/)

给定一个数组，我们需要修改这个数组的值，使得两个连续元素之间的绝对差之和最大化。如果一个数组元素的值是 X，那么我们可以把它改成 1 或者 X。
**示例:**

```
Input  : arr[] = [3, 2, 1, 4, 5]
Output : 8
We can modify above array as,
Modified arr[] = [3, 1, 1, 4, 1]
Sum of differences = 
|1-3| + |1-1| + |4-1| + |1-4| = 8
Which is the maximum obtainable value 
among all choices of modification.

Input  : arr[] = [1, 8, 9]
Output : 14
```

这个问题是[流水线调度](https://www.geeksforgeeks.org/dynamic-programming-set-34-assembly-line-scheduling/)的变种，可以用动态规划来解决。我们需要最大化差的和，每个值 X 应该被改变为 1 或 X。为了实现上述条件，我们采用具有 2 列的数组长度大小的 dp 数组，其中只有当数组值被修改为 1 时，dp[i][0]才存储使用前 I 个元素的和的最大值，并且如果数组值保持为[i]本身，dp[i][1]存储使用前 I 个元素的和的最大值。主要观察的是，

## C++

```
//  C++ program to get maximum consecutive element
// difference sum
#include <bits/stdc++.h>
using namespace std;

// Returns maximum-difference-sum with array
// modifications allowed.
int maximumDifferenceSum(int arr[], int N)
{
    // Initialize dp[][] with 0 values.
    int dp[N][2];
    for (int i = 0; i < N; i++)
        dp[i][0] = dp[i][1] = 0;

    for (int i=0; i<(N-1); i++)
    {
        /*  for [i+1][0] (i.e. current modified
            value is 1), choose maximum from
            dp[i][0] + abs(1 - 1) = dp[i][0] and
            dp[i][1] + abs(1 - arr[i])   */
        dp[i + 1][0] = max(dp[i][0],
                          dp[i][1] + abs(1-arr[i]));

        /*  for [i+1][1] (i.e. current modified value
            is arr[i+1]), choose maximum from
            dp[i][0] + abs(arr[i+1] - 1)    and
            dp[i][1] + abs(arr[i+1] - arr[i])*/
        dp[i + 1][1] = max(dp[i][0] + abs(arr[i+1] - 1),
                     dp[i][1] + abs(arr[i+1] - arr[i]));
    }

    return max(dp[N-1][0], dp[N-1][1]);
}

//  Driver code to test above methods
int main()
{
    int arr[] = {3, 2, 1, 4, 5};
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << maximumDifferenceSum(arr, N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to get maximum consecutive element
// difference sum
import java.io.*;

class GFG
{
    // Returns maximum-difference-sum with array
    // modifications allowed.
    static int maximumDifferenceSum(int arr[], int N)
    {
        // Initialize dp[][] with 0 values.
        int dp[][] = new int [N][2];

        for (int i = 0; i < N; i++)
            dp[i][0] = dp[i][1] = 0;

        for (int i = 0; i< (N - 1); i++)
        {
            /* for [i+1][0] (i.e. current modified
            value is 1), choose maximum from
            dp[i][0] + abs(1 - 1) = dp[i][0] and
            dp[i][1] + abs(1 - arr[i]) */
            dp[i + 1][0] = Math.max(dp[i][0],
                           dp[i][1] + Math.abs(1 - arr[i]));

            /* for [i+1][1] (i.e. current modified value
            is arr[i+1]), choose maximum from
            dp[i][0] + abs(arr[i+1] - 1) and
            dp[i][1] + abs(arr[i+1] - arr[i])*/
            dp[i + 1][1] = Math.max(dp[i][0] +
                           Math.abs(arr[i + 1] - 1),
                           dp[i][1] + Math.abs(arr[i + 1]
                           - arr[i]));
        }

        return Math.max(dp[N - 1][0], dp[N - 1][1]);
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = {3, 2, 1, 4, 5};
        int N = arr.length;
        System.out.println( maximumDifferenceSum(arr, N));

    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python3 program to get maximum
# consecutive element difference sum

# Returns maximum-difference-sum
# with array modifications allowed.
def maximumDifferenceSum(arr, N):

    # Initialize dp[][] with 0 values.
    dp = [[0, 0] for i in range(N)]
    for i in range(N):
        dp[i][0] = dp[i][1] = 0

    for i in range(N - 1):

        # for [i+1][0] (i.e. current modified
        # value is 1), choose maximum from
        # dp[i][0] + abs(1 - 1) = dp[i][0]
        # and dp[i][1] + abs(1 - arr[i])
        dp[i + 1][0] = max(dp[i][0], dp[i][1] +
                             abs(1 - arr[i]))

        # for [i+1][1] (i.e. current modified value
        # is arr[i+1]), choose maximum from
        # dp[i][0] + abs(arr[i+1] - 1) and
        # dp[i][1] + abs(arr[i+1] - arr[i])
        dp[i + 1][1] = max(dp[i][0] + abs(arr[i + 1] - 1),
                           dp[i][1] + abs(arr[i + 1] - arr[i]))

    return max(dp[N - 1][0], dp[N - 1][1])

# Driver Code
if __name__ == '__main__':
    arr = [3, 2, 1, 4, 5]
    N = len(arr)
    print(maximumDifferenceSum(arr, N))

# This code is contributed by PranchalK
```

## C#

```
// C# program to get maximum consecutive element
// difference sum
using System;

class GFG {

    // Returns maximum-difference-sum with array
    // modifications allowed.
    static int maximumDifferenceSum(int []arr, int N)
    {

        // Initialize dp[][] with 0 values.
        int [,]dp = new int [N,2];

        for (int i = 0; i < N; i++)
            dp[i,0] = dp[i,1] = 0;

        for (int i = 0; i < (N - 1); i++)
        {
            /* for [i+1][0] (i.e. current modified
            value is 1), choose maximum from
            dp[i][0] + abs(1 - 1) = dp[i][0] and
            dp[i][1] + abs(1 - arr[i]) */
            dp[i + 1,0] = Math.Max(dp[i,0],
                        dp[i,1] + Math.Abs(1 - arr[i]));

            /* for [i+1][1] (i.e. current modified value
            is arr[i+1]), choose maximum from
            dp[i][0] + abs(arr[i+1] - 1) and
            dp[i][1] + abs(arr[i+1] - arr[i])*/
            dp[i + 1,1] = Math.Max(dp[i,0] +
                        Math.Abs(arr[i + 1] - 1),
                        dp[i,1] + Math.Abs(arr[i + 1]
                        - arr[i]));
        }

        return Math.Max(dp[N - 1,0], dp[N - 1,1]);
    }

    // Driver code
    public static void Main ()
    {
        int []arr = {3, 2, 1, 4, 5};
        int N = arr.Length;

        Console.Write( maximumDifferenceSum(arr, N));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to get maximum
// consecutive element
// difference sum

// Returns maximum-difference-sum
// with array modifications allowed.
function maximumDifferenceSum($arr, $N)
{
    // Initialize dp[][]
    // with 0 values.
    $dp = array(array());
    for ($i = 0; $i < $N; $i++)
        $dp[$i][0] = $dp[$i][1] = 0;

    for ($i = 0; $i < ($N - 1); $i++)
    {
        /* for [i+1][0] (i.e. current
            modified value is 1), choose
            maximum from dp[$i][0] +
            abs(1 - 1) = dp[i][0] and
            dp[$i][1] + abs(1 - arr[i]) */
        $dp[$i + 1][0] = max($dp[$i][0],
                            $dp[$i][1] +
                            abs(1 - $arr[$i]));

        /* for [i+1][1] (i.e. current
            modified value is arr[i+1]),
            choose maximum from dp[i][0] +
            abs(arr[i+1] - 1) and dp[i][1] +
            abs(arr[i+1] - arr[i])*/
        $dp[$i + 1][1] = max($dp[$i][0] +
                             abs($arr[$i + 1] - 1),
                                       $dp[$i][1] +
                                 abs($arr[$i + 1] -
                                        $arr[$i]));
    }

    return max($dp[$N - 1][0], $dp[$N - 1][1]);
}

// Driver Code
$arr = array(3, 2, 1, 4, 5);
$N = count($arr);
echo maximumDifferenceSum($arr, $N);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript program to get maximum consecutive element difference sum

    // Returns maximum-difference-sum with array
    // modifications allowed.
    function maximumDifferenceSum(arr, N)
    {
        // Initialize dp[][] with 0 values.
        let dp = new Array(N);
        for (let i = 0; i < N; i++)
        {
            dp[i] = new Array(2);
            for (let j = 0; j < 2; j++)
            {
                dp[i][j] = 0;
            }
        }

        for (let i = 0; i < N; i++)
            dp[i][0] = dp[i][1] = 0;

        for (let i = 0; i< (N - 1); i++)
        {
            /* for [i+1][0] (i.e. current modified
            value is 1), choose maximum from
            dp[i][0] + abs(1 - 1) = dp[i][0] and
            dp[i][1] + abs(1 - arr[i]) */
            dp[i + 1][0] = Math.max(dp[i][0],
                           dp[i][1] + Math.abs(1 - arr[i]));

            /* for [i+1][1] (i.e. current modified value
            is arr[i+1]), choose maximum from
            dp[i][0] + abs(arr[i+1] - 1) and
            dp[i][1] + abs(arr[i+1] - arr[i])*/
            dp[i + 1][1] = Math.max(dp[i][0] +
                           Math.abs(arr[i + 1] - 1),
                           dp[i][1] + Math.abs(arr[i + 1]
                           - arr[i]));
        }

        return Math.max(dp[N - 1][0], dp[N - 1][1]);
    }

    let arr = [3, 2, 1, 4, 5];
    let N = arr.length;
    document.write( maximumDifferenceSum(arr, N));

    // This code is contributed by rameshtravel07.
</script>
```

**Output**

```
8
```