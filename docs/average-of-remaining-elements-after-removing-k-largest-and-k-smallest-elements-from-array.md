# 从数组中移除 K 个最大和 K 个最小元素后剩余元素的平均值

> 原文:[https://www . geeksforgeeks . org/从数组中移除 k 个最大和 k 个最小元素后剩余元素的平均值/](https://www.geeksforgeeks.org/average-of-remaining-elements-after-removing-k-largest-and-k-smallest-elements-from-array/)

给定一个 N 个整数的数组。任务是在从数组中移除 k 个最大元素和 k 个最小元素后，找到数字的平均值，即计算剩余的 N–2K 个元素的平均值。

**示例:**

```
Input: arr = [1, 2, 4, 4, 5, 6], K = 2
Output: 4
Remove 2 smallest elements i.e. 1 and 2
Remove 2 largest elements i.e. 5 and 6
Remaining elements are 4, 4\. So average of 4, 4 is 4.

Input: arr = [1, 2, 3], K = 3
Output: 0
```

**进场:**

*   如果要移除的元素数量大于数组中存在的元素数量，则 ans = 0。
*   否则，对数组的所有元素进行排序。然后，计算从 Kth 指数到 n-k-1 指数的元素平均值。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find average
double average(int arr[], int n, int k)
{
    double total = 0;

    // base case if 2*k>=n
    // means all element get removed
    if (2 * k >= n)
        return 0;

    // first sort all elements
    sort(arr, arr + n);
    int start = k, end = n - k - 1;

    // sum of req number
    for (int i = start; i <= end; i++)
        total += arr[i];

    // find average
    return (total / (n - 2 * k));
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 4, 4, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;

    cout << average(arr, n, k) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

import java.io.*;
import java.util.*;
class GFG {

// Function to find average
static double average(int arr[], int n, int k)
{
    double total = 0;

    // base case if 2*k>=n
    // means all element get removed
    if (2 * k >= n)
        return 0;

    // first sort all elements
    Arrays.sort(arr);
    int start = k, end = n - k - 1;

    // sum of req number
    for (int i = start; i <= end; i++)
        total += arr[i];

    // find average
    return (total / (n - 2 * k));
}

// Driver code

    public static void main (String[] args) {
            int arr[] = { 1, 2, 4, 4, 5, 6 };
    int n = arr.length;
    int k = 2;

    System.out.println( average(arr, n, k));

}
}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to find average
def average(arr, n, k) :
    total = 0

    # base case if 2*k>=n
    # means all element get removed
    if (2 * k >= n) :
        return 0

    # first sort all elements
    arr.sort()

    start , end = k , n - k - 1

    # sum of req number
    for i in range(start, end + 1) :
        total += arr[i]

    # find average
    return (total / (n - 2 * k))

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, 4, 4, 5, 6 ]
    n = len(arr)
    k = 2

    print(average(arr, n, k))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the above approach

using System;
public class GFG {

    // Function to find average
    static double average(int []arr, int n, int k)
    {
        double total = 0;

        // base case if 2*k>=n
        // means all element get removed
        if (2 * k >= n)
            return 0;

        // first sort all elements
        Array.Sort(arr);
        int start = k, end = n - k - 1;

        // sum of req number
        for (int i = start; i <= end; i++)
            total += arr[i];

        // find average
        return (total / (n - 2 * k));
    }

    // Driver code

        public static void Main() {
                int []arr = { 1, 2, 4, 4, 5, 6 };
        int n = arr.Length;
        int k = 2;

        Console.WriteLine( average(arr, n, k));

    }
}
//This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php implementation of the
// above approach

// Function to find average
function average($arr, $n, $k)
{
    $total = 0;

    // base case if 2*k>=n
    // means all element get removed
    if (2 * $k >= $n)
        return 0;

    // first sort all elements
    sort($arr) ;

    $start = $k ;
    $end = $n - $k - 1;

    // sum of req number
    for ($i = $start; $i <= $end; $i++)
        $total += $arr[$i];

    // find average
    return ($total / ($n - 2 * $k));
}

// Driver code
$arr = array(1, 2, 4, 4, 5, 6);
$n = sizeof($arr);
$k = 2;

echo average($arr, $n, $k);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to find average
function average(arr, n, k)
{
    var total = 0;

    // Base case if 2*k>=n
    // means all element get removed
    if (2 * k >= n)
        return 0;

    // First sort all elements
    arr.sort();
    var start = k, end = n - k - 1;

    // Sum of req number
    for(i = start; i <= end; i++)
        total += arr[i];

    // Find average
    return (total / (n - 2 * k));
}

// Driver code
var arr = [ 1, 2, 4, 4, 5, 6 ];
var n = arr.length;
var k = 2;

document.write(average(arr, n, k));

// This code is contributed by aashish1995

</script>
```

**Output:** 

```
4
```