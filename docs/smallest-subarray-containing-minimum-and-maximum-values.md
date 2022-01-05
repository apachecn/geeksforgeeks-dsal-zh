# 包含最小值和最大值的最小子阵列

> 原文:[https://www . geesforgeks . org/minist-subarray-包含最小值和最大值/](https://www.geeksforgeeks.org/smallest-subarray-containing-minimum-and-maximum-values/)

给定大小为 n 的数组 A，任务是找到包含最大值和最小值的最小子数组的长度。
**例:**

```
Input : A[] = {1, 5, 9, 7, 1, 9, 4}
Output : 2
subarray {1, 9} has both maximum and minimum value.

Input : A[] = {2, 2, 2, 2}
Output : 1
2 is both maximum and minimum here.
```

**进场:**思路是使用[双指技术](https://www.geeksforgeeks.org/two-pointers-technique/)这里:

*   求数组的最大值和最小值。
*   遍历数组并存储最近出现的最大值和最小值。
*   如果最大值最后一次出现的时间是 **pos_max** ，最小值是 **pos_min** ，那么**ABS(pos _ min–pos _ max)+1**的最小值就是我们需要的答案。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return length of
// smallest subarray containing both
// maximum and minimum value
int minSubarray(int A[], int n)
{

    // find maximum and minimum
    // values in the array
    int minValue = *min_element(A, A + n);
    int maxValue = *max_element(A, A + n);

    int pos_min = -1, pos_max = -1, ans = INT_MAX;

    // iterate over the array and set answer
    // to smallest difference between position
    // of maximum and position of minimum value
    for (int i = 0; i < n; i++) {

        // last occurrence of minValue
        if (A[i] == minValue)
            pos_min = i;

        // last occurrence of maxValue
        if (A[i] == maxValue)
            pos_max = i;

        if (pos_max != -1 and pos_min != -1)
            ans = min(ans, abs(pos_min - pos_max) + 1);
    }

    return ans;
}

// Driver code
int main()
{
    int A[] = { 1, 5, 9, 7, 1, 9, 4 };
    int n = sizeof(A) / sizeof(A[0]);

    cout << minSubarray(A, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;

class GFG
{

// Function to return length of
// smallest subarray containing both
// maximum and minimum value
static int minSubarray(int A[], int n)
{

    // find maximum and minimum
    // values in the array
    int minValue = A[0];
    for(int i = 1; i < n; i++)
    {
        if(A[i] < minValue)
            minValue = A[i];
    }
    int maxValue = A[0];
    for(int i = 1; i < n; i++)
    {
        if(A[i] > maxValue)
            maxValue = A[i];
    }

    int pos_min = -1, pos_max = -1,
        ans = Integer.MAX_VALUE;

    // iterate over the array and set answer
    // to smallest difference between position
    // of maximum and position of minimum value
    for (int i = 0; i < n; i++)
    {

        // last occurrence of minValue
        if (A[i] == minValue)
            pos_min = i;

        // last occurrence of maxValue
        if (A[i] == maxValue)
            pos_max = i;

        if (pos_max != -1 && pos_min != -1)
            ans = Math.min(ans,
                  Math.abs(pos_min - pos_max) + 1);
    }

    return ans;
}

// Driver code
public static void main(String args[])
{
    int A[] = { 1, 5, 9, 7, 1, 9, 4 };
    int n = A.length;

    System.out.println(minSubarray(A, n));
}
}

// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of above approach
import sys

# Function to return length of smallest
# subarray containing both maximum and
# minimum value
def minSubarray(A, n):

    # find maximum and minimum
    # values in the array
    minValue = min(A)
    maxValue = max(A)

    pos_min, pos_max, ans = -1, -1, sys.maxsize

    # iterate over the array and set answer
    # to smallest difference between position
    # of maximum and position of minimum value
    for i in range(0, n):

        # last occurrence of minValue
        if A[i] == minValue:
            pos_min = i

        # last occurrence of maxValue
        if A[i] == maxValue:
            pos_max = i

        if pos_max != -1 and pos_min != -1 :
            ans = min(ans, abs(pos_min - pos_max) + 1)

    return ans

# Driver code
A = [ 1, 5, 9, 7, 1, 9, 4 ]
n = len(A)

print(minSubarray(A, n))

# This code is contributed
# by Saurabh_Shukla
```

## C#

```
// C# implementation of above approach
using System;
using System.Linq;

public class GFG{

// Function to return length of
// smallest subarray containing both
// maximum and minimum value
static int minSubarray(int []A, int n)
{

    // find maximum and minimum
    // values in the array
    int minValue = A.Min();
    int maxValue = A.Max();

    int pos_min = -1, pos_max = -1, ans = int.MaxValue;

    // iterate over the array and set answer
    // to smallest difference between position
    // of maximum and position of minimum value
    for (int i = 0; i < n; i++) {

        // last occurrence of minValue
        if (A[i] == minValue)
            pos_min = i;

        // last occurrence of maxValue
        if (A[i] == maxValue)
            pos_max = i;

        if (pos_max != -1 && pos_min != -1)
            ans = Math.Min(ans, Math.Abs(pos_min - pos_max) + 1);
    }

    return ans;
}

// Driver code

    static public void Main (){
            int []A = { 1, 5, 9, 7, 1, 9, 4 };
    int n = A.Length;

    Console.WriteLine(minSubarray(A, n));
    }
}
// This code is contributed by anuj_67..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to return length of
// smallest subarray containing both
// maximum and minimum value
function minSubarray($A, $n)
{

    // find maximum and minimum
    // values in the array
    $minValue = min($A);
    $maxValue = max($A);

    $pos_min = -1;
    $pos_max = -1;
    $ans = PHP_INT_MAX;

    // iterate over the array and set answer
    // to smallest difference between position
    // of maximum and position of minimum value
    for ($i = 0; $i < $n; $i++)
    {

        // last occurrence of minValue
        if ($A[$i] == $minValue)
            $pos_min = $i;

        // last occurrence of maxValue
        if ($A[$i] == $maxValue)
            $pos_max = $i;

        if ($pos_max != -1 and $pos_min != -1)
            $ans = min($ans, abs($pos_min -
                                 $pos_max) + 1);
    }

    return $ans;
}

// Driver code
$A = array(1, 5, 9, 7, 1, 9, 4);
$n = sizeof($A);

echo minSubarray($A, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of above approach

    // Function to return length of
    // smallest subarray containing both
    // maximum and minimum value
    function minSubarray(A, n)
    {

        // find maximum and minimum
        // values in the array
        let minValue = Number.MAX_VALUE;
        let maxValue = Number.MIN_VALUE;
        for (let i = 0; i < n; i++)
        {
            minValue = Math.min(minValue, A[i]);
            maxValue = Math.max(maxValue, A[i]);
        }

        let pos_min = -1, pos_max = -1, ans = Number.MAX_VALUE;

        // iterate over the array and set answer
        // to smallest difference between position
        // of maximum and position of minimum value
        for (let i = 0; i < n; i++) {

            // last occurrence of minValue
            if (A[i] == minValue)
                pos_min = i;

            // last occurrence of maxValue
            if (A[i] == maxValue)
                pos_max = i;

            if (pos_max != -1 && pos_min != -1)
                ans = Math.min(ans, Math.abs(pos_min - pos_max) + 1);
        }

        return ans;
    }

    let A = [ 1, 5, 9, 7, 1, 9, 4 ];
    let n = A.length;

    document.write(minSubarray(A, n));

</script>
```

**Output:** 

```
2
```