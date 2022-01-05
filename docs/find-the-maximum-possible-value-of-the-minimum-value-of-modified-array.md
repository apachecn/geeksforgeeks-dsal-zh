# 求修改数组最小值的最大可能值

> 原文:[https://www . geesforgeks . org/find-最大可能值-最小可能值-修改后的数组/](https://www.geeksforgeeks.org/find-the-maximum-possible-value-of-the-minimum-value-of-modified-array/)

给定一个大小为![N  ](img/05447a6f3ec73065b361522074101320.png "Rendered by QuickLaTeX.com")的数组和一个数字![S  ](img/286065faa2e31cda66548efbe78a36d1.png "Rendered by QuickLaTeX.com")。任务是修改给定的数组，使得:

*   修改前后数组元素之和的差值正好等于 s。
*   修改后的数组元素应该是非负的。
*   修改后的数组中的最小值必须最大化。
*   要修改给定的数组，可以增加或减少数组的任何元素。

任务是找到修改后数组的最小数量。如果不可能，则打印-1。最小数量应该尽可能多。
**例:**

```
Input : a[] = {2, 2, 3}, S = 1
Output : 2
Explanation : Modified array is {2, 2, 2}

Input : a[] = {1, 3, 5}, S = 10
Output : -1
```

一种有效的方法是在修改后的数组中最小数的最小和最大可能值之间建立二分搜索法。最小可能值为零，最大可能数组是给定数组中的最小数。如果给定的数组元素和小于 S，那么答案是不可能的。所以，打印-1。如果给定的数组元素总和等于 S，那么答案将为零。
以下是上述方法的实现:

## C++

```
// CPP program to find the maximum possible
// value of the minimum value of
// modified array

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum possible value
// of the minimum value of the modified array
int maxOfMin(int a[], int n, int S)
{
    // To store minimum value of array
    int mi = INT_MAX;

    // To store sum of elements of array
    int s1 = 0;

    for (int i = 0; i < n; i++) {
        s1 += a[i];
        mi = min(a[i], mi);
    }

    // Solution is not possible
    if (s1 < S)
        return -1;

    // zero is the possible value
    if (s1 == S)
        return 0;

    // minimum possible value
    int low = 0;

    // maximum possible value
    int high = mi;

    // to store a required answer
    int ans;

    // Binary Search
    while (low <= high) {

        int mid = (low + high) / 2;

        // If mid is possible then try to increase
        // required answer
        if (s1 - (mid * n) >= S) {
            ans = mid;
            low = mid + 1;
        }

        // If mid is not possible then decrease
        // required answer
        else
            high = mid - 1;
    }

    // Return required answer
    return ans;
}

// Driver Code
int main()
{
    int a[] = { 10, 10, 10, 10, 10 };

    int S = 10;

    int n = sizeof(a) / sizeof(a[0]);

    cout << maxOfMin(a, n, S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  program to find the maximum possible
// value of the minimum value of
// modified array

import java.io.*;

class GFG {

// Function to find the maximum possible value
// of the minimum value of the modified array
static int maxOfMin(int a[], int n, int S)
{
    // To store minimum value of array
    int mi = Integer.MAX_VALUE;

    // To store sum of elements of array
    int s1 = 0;

    for (int i = 0; i < n; i++) {
        s1 += a[i];
        mi = Math.min(a[i], mi);
    }

    // Solution is not possible
    if (s1 < S)
        return -1;

    // zero is the possible value
    if (s1 == S)
        return 0;

    // minimum possible value
    int low = 0;

    // maximum possible value
    int high = mi;

    // to store a required answer
    int ans=0;

    // Binary Search
    while (low <= high) {

        int mid = (low + high) / 2;

        // If mid is possible then try to increase
        // required answer
        if (s1 - (mid * n) >= S) {
            ans = mid;
            low = mid + 1;
        }

        // If mid is not possible then decrease
        // required answer
        else
            high = mid - 1;
    }

    // Return required answer
    return ans;
}

// Driver Code
    public static void main (String[] args) {

    int a[] = { 10, 10, 10, 10, 10 };

    int S = 10;

    int n = a.length;

    System.out.println( maxOfMin(a, n, S));
    }
//This code is contributed by ajit.   
}
```

## 计算机编程语言

```
# Python program to find the maximum possible
# value of the minimum value of
# modified array

# Function to find the maximum possible value
# of the minimum value of the modified array
def maxOfMin(a, n, S):

    # To store minimum value of array
    mi = 10**9

    # To store sum of elements of array
    s1 = 0

    for i in range(n):
        s1 += a[i]
        mi = min(a[i], mi)

    # Solution is not possible
    if (s1 < S):
        return -1

    # zero is the possible value
    if (s1 == S):
        return 0

    # minimum possible value
    low = 0

    # maximum possible value
    high = mi

    # to store a required answer
    ans=0

    # Binary Search
    while (low <= high):

        mid = (low + high) // 2

        # If mid is possible then try to increase
        # required answer
        if (s1 - (mid * n) >= S):
            ans = mid
            low = mid + 1

        # If mid is not possible then decrease
        # required answer
        else:
            high = mid - 1

    # Return required answer
    return ans

# Driver Code

a=[10, 10, 10, 10, 10]

S = 10

n =len(a)

print(maxOfMin(a, n, S))
#This code is contributed by Mohit kumar 29
```

## C#

```
// C# program to find the maximum possible
// value of the minimum value of
// modified array

using System;

class GFG {

    // Function to find the maximum possible value
    // of the minimum value of the modified array
    static int maxOfMin(int []a, int n, int S)
    {
        // To store minimum value of array
        int mi = int.MaxValue;

        // To store sum of elements of array
        int s1 = 0;

        for (int i = 0; i < n; i++) {
            s1 += a[i];
            mi = Math.Min(a[i], mi);
        }

        // Solution is not possible
        if (s1 < S)
            return -1;

        // zero is the possible value
        if (s1 == S)
            return 0;

        // minimum possible value
        int low = 0;

        // maximum possible value
        int high = mi;

        // to store a required answer
        int ans=0;

        // Binary Search
        while (low <= high) {

            int mid = (low + high) / 2;

            // If mid is possible then try to increase
            // required answer
            if (s1 - (mid * n) >= S) {
                ans = mid;
                low = mid + 1;
            }

            // If mid is not possible then decrease
            // required answer
            else
                high = mid - 1;
        }

        // Return required answer
        return ans;
    }

    // Driver Code
    public static void Main () {

    int []a = { 10, 10, 10, 10, 10 };

    int S = 10;

    int n = a.Length;

    Console.WriteLine(maxOfMin(a, n, S));
    }
    //This code is contributed by Ryuga
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the maximum possible
// value of the minimum value of modified array

// Function to find the maximum possible value
// of the minimum value of the modified array
function maxOfMin($a, $n, $S)
{
    // To store minimum value
    // of array
    $mi = PHP_INT_MAX;

    // To store sum of elements
    // of array
    $s1 = 0;

    for ($i = 0; $i < $n; $i++)
    {
        $s1 += $a[$i];
        $mi = min($a[$i], $mi);
    }

    // Solution is not possible
    if ($s1 < $S)
        return -1;

    // zero is the possible value
    if ($s1 == $S)
        return 0;

    // minimum possible value
    $low = 0;

    // maximum possible value
    $high = $mi;

    // to store a required answer
    $ans;

    // Binary Search
    while ($low <= $high)
    {

        $mid = ($low + $high) / 2;

        // If mid is possible then try
        // to increase required answer
        if ($s1 - ($mid * $n) >= $S)
        {
            $ans = $mid;
            $low = $mid + 1;
        }

        // If mid is not possible then
        // decrease required answer
        else
            $high = $mid - 1;
    }

    // Return required answer
    return $ans;
}

// Driver Code
$a = array( 10, 10, 10, 10, 10 );
$S = 10;
$n = sizeof($a);
echo maxOfMin($a, $n, $S);

// This code is contributed by akt_mit
?>
```

## java 描述语言

```
<script>

    // Javascript program to find the maximum possible
    // value of the minimum value of
    // modified array

    // Function to find the maximum possible value
    // of the minimum value of the modified array
    function maxOfMin(a, n, S)
    {
        // To store minimum value of array
        let mi = Number.MAX_VALUE;

        // To store sum of elements of array
        let s1 = 0;

        for (let i = 0; i < n; i++) {
            s1 += a[i];
            mi = Math.min(a[i], mi);
        }

        // Solution is not possible
        if (s1 < S)
            return -1;

        // zero is the possible value
        if (s1 == S)
            return 0;

        // minimum possible value
        let low = 0;

        // maximum possible value
        let high = mi;

        // to store a required answer
        let ans=0;

        // Binary Search
        while (low <= high) {

            let mid = parseInt((low + high) / 2, 10);

            // If mid is possible then try to increase
            // required answer
            if (s1 - (mid * n) >= S) {
                ans = mid;
                low = mid + 1;
            }

            // If mid is not possible then decrease
            // required answer
            else
                high = mid - 1;
        }

        // Return required answer
        return ans;
    }

    let a = [ 10, 10, 10, 10, 10 ];

    let S = 10;

    let n = a.length;

    document.write(maxOfMin(a, n, S));

</script>
```

**Output:** 

```
8
```