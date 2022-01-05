# 子阵列中“最大+最小”的最小值

> 原文:[https://www . geesforgeks . org/mini-value-max-min-subarray/](https://www.geeksforgeeks.org/minimum-value-max-min-subarray/)

给定 n 个正元素的数组，我们需要找到一个[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)中最大和最小元素的最小可能和，假设子阵列的大小应该大于等于 2。
**例:**

```
Input : arr[] = {1 12 2 2}
Output : 4
Sum of 2+2 of subarray [2, 2]

Input  : arr[] = {10 20 30 40 23 45}
Output : 30 
Sum of 10+20 of subarray[10, 20]
```

一个**简单的解决方案**就是生成所有子阵，计算最大和最小之和，最后返回最小和。
一个**有效的解决方案**是基于这样一个事实，即在子阵列中添加任何元素都不会增加最大值和最小值之和。考虑数组[a1，a2，a3，a4，a5…每个 ai 将是一些子阵列[al，ar]的最小值，使得 I 位于[l，r]之间，并且子阵列中的所有元素都大于或等于 ai。这种子阵列的成本是 ai + max(子阵列)。由于数组的最大值在向数组中添加元素时永远不会减少，所以只有当我们添加更大的元素时，它才会增加，因此最好只考虑长度为 2 的子数组。
简而言之，考虑长度为 2 的所有子阵列，比较和并取最小的一个，这将减少 O(N)的时间复杂度，现在我们只需要运行循环一次。

## C++

```
// CPP program to find sum of maximum and
// minimum in any subarray of an array of
// positive numbers.
#include <bits/stdc++.h>
using namespace std;

int maxSum(int arr[], int n)
{
    if (n < 2)
        return -1;
    int ans = arr[0] + arr[1];
    for (int i = 1; i + 1 < n; i++)
        ans = min(ans, (arr[i] + arr[i + 1]));
    return ans;
}

// Driver code
int main()
{
    int arr[] = {1, 12, 2, 2};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << maxSum(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to find sum of maximum and
// minimum in any subarray of an array of
// positive numbers.
import java.io.*;

class GFG {

    static int maxSum(int arr[], int n)
    {
        if (n < 2)
            return -1;
        int ans = arr[0] + arr[1];
        for (int i = 1; i + 1 < n; i++)
            ans = Math.min(ans, (arr[i]
                           + arr[i + 1]));
        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = {1, 12, 2, 2};
        int n = arr.length;

        System.out.println( maxSum(arr, n));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python 3 program to find sum of maximum
# and minimum in any subarray of an array
# of positive numbers.

def maxSum(arr, n):
    if (n < 2):
        return -1
    ans = arr[0] + arr[1]
    for i in range(1, n - 1, 1):
        ans = min(ans, (arr[i] + arr[i + 1]))
    return ans

# Driver code
if __name__ == '__main__':
    arr = [1, 12, 2, 2]
    n = len(arr)
    print(maxSum(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find sum of maximum and
// minimum in any subarray of an array of
// positive numbers.
using System ;

class GFG {

    static int maxSum(int []arr, int n)
    {
        if (n < 2)
            return -1;
        int ans = arr[0] + arr[1];
        for (int i = 1; i + 1 < n; i++)
            ans = Math.Min(ans, (arr[i]
                        + arr[i + 1]));
        return ans;
    }

    // Driver code
    public static void Main ()
    {
        int []arr = {1, 12, 2, 2};
        int n = arr.Length;

        Console.WriteLine( maxSum(arr, n));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of
// maximum and minimum in any
// subarray of an array of
// positive numbers.

function maxSum( $arr, $n)
{
    if ($n < 2)
        return -1;
    $ans = $arr[0] + $arr[1];
    for ( $i = 1; $i + 1 < $n; $i++)
        $ans = min($ans, ($arr[$i] +
                     $arr[$i + 1]));
    return $ans;
}

    // Driver code
    $arr = array(1, 12, 2, 2);
    $n = count($arr);
    echo maxSum($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// java program to find sum of maximum and
// minimum in any subarray of an array of
// positive numbers.
function maxSum(arr,n)
    {
        if (n < 2)
            return -1;
        let ans = arr[0] + arr[1];
        for (let i = 1; i + 1 < n; i++)
            ans = Math.min(ans, (arr[i]
                        + arr[i + 1]));
        return ans;
    }

    // Driver code

        let arr = [1, 12, 2, 2];
        let n = arr.length;

        document.write( maxSum(arr, n));
// This code is contributed by sravan
</script>
```

**Output:** 

```
4
```

时间复杂度:O(n)
辅助空间:O(1)