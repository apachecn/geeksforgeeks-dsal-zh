# 检查数组元素在 O(n)时间和 O(1)空间是否连续(处理正数和负数)

> 原文:[https://www . geesforgeks . org/check-array-elements-continuous-time-O1-space-handles-正数-负数/](https://www.geeksforgeeks.org/check-array-elements-consecutive-time-o1-space-handles-positive-negative-numbers/)

给定一个由**个不同的**个数字组成的未排序数组，编写一个函数，如果数组由连续的数字组成，该函数返回 true。
**例:**

```
Input : arr[] = {5, 4, 2, 1, 3}
Output : Yes

Input : arr[] = {2, 1, 0, -3, -1, -2}
Output : Yes
```

我们在下面的帖子
[中讨论了三种不同的方法，检查数组元素是否连续](https://www.geeksforgeeks.org/check-if-array-elements-are-consecutive/)
在上面的帖子中。用 O(n)的最佳时间复杂度和 O(1)的额外空间讨论了解决这个问题的三种方法，但是该解决方案不处理负数的情况。因此，在这篇文章中，我们将讨论一个时间复杂度为 O(n)并且使用 O(1)空间的方法，它也将处理负的情况。这里的一个重要假设是元素是不同的。

1.  求数组的和。
2.  如果给定的数组元素是连续的，这意味着它们在 AP 中。因此，找到最小元素，即 AP 的第一项，然后计算 ap_sum = n/2 * [2a +(n-1)*d]，其中 d = 1。所以，ap_sum = n/2 * [2a +(n-1)]
3.  比较两者的总和。如果相等，则打印是，否则打印否

## C++

```
// C++ program for above implementation
#include <bits/stdc++.h>
using namespace std;

// Function to check if elements are consecutive
bool areConsecutives(int arr[], int n)
{
    // Find minimum element in array
    int first_term = *(min_element(arr, arr + n));

    // Calculate AP sum
    int ap_sum = (n * (2 * first_term + (n - 1) * 1)) / 2;

    // Calculate given array sum
    int arr_sum = 0;
    for (int i = 0; i < n; i++)
        arr_sum += arr[i];

    // Compare both sums and return
    return ap_sum == arr_sum;
}

// Drivers code
int main()
{
    int arr[] = { 2, 1, 0, -3, -1, -2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    areConsecutives(arr, n) ? cout << "Yes"
                            : cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if array elements
// are consecutive
import java.io.*;

class GFG {

    // Function to check if elements are
    // consecutive
    static Boolean areConsecutives(int arr[],
                                      int n)
    {
        // Find minimum element in array
        int first_term = Integer.MAX_VALUE;
        for (int j = 0; j < n; j++)
        {
            if(arr[j] < first_term)
            first_term = arr[j];
        }

        // Calculate AP sum
        int ap_sum = (n * (2 * first_term +
                         (n - 1) * 1)) / 2;

        // Calculate given array sum
        int arr_sum = 0;
        for (int i = 0; i < n; i++)
            arr_sum += arr[i];

        // Compare both sums and return
        return ap_sum == arr_sum;
    }

    // Driver code
    public static void main(String[] args)
    {
    int arr[] = { 2, 1, 0, -3, -1, -2 };
    int n = arr.length;

    Boolean result = areConsecutives(arr, n);
    if(result == true)
    System.out.println("Yes");
    else
    System.out.println("No");

    }
}
// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python 3 program for above
# implementation
import sys

# Function to check if elements
# are consecutive
def areConsecutives(arr, n):

    # Find minimum element in array
    first_term = sys.maxsize
    for i in range(n):
        if arr[i] < first_term:
            first_term = arr[i]

    # Calculate AP sum
    ap_sum = ((n * (2 * first_term +
              (n - 1) * 1)) // 2)

    # Calculate given array sum
    arr_sum = 0
    for i in range( n):
        arr_sum += arr[i]

    # Compare both sums and return
    return ap_sum == arr_sum

# Driver Code
arr = [ 2, 1, 0, -3, -1, -2 ]
n = len(arr)

if areConsecutives(arr, n):
    print( "Yes")
else:
    print( "No")

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to check if array
// elements are consecutive
using System;

class GFG {

    // Function to check if elements 
    // are consecutive
    static bool areConsecutives(int []arr,
                                int n)
    {

        // Find minimum element in array
        int first_term = int.MaxValue;

        for (int j = 0; j < n; j++)
        {
            if(arr[j] < first_term)
            first_term = arr[j];
        }

        // Calculate AP sum
        int ap_sum = (n * (2 * first_term +
                     (n - 1) * 1)) / 2;

        // Calculate given array sum
        int arr_sum = 0;
        for (int i = 0; i < n; i++)
            arr_sum += arr[i];

        // Compare both sums and return
        return ap_sum == arr_sum;
    }

    // Driver code
    public static void Main()
    {
        int []arr = {2, 1, 0, -3, -1, -2};
        int n = arr.Length;

        bool result = areConsecutives(arr, n);
        if(result == true)
        Console.WriteLine("Yes");
        else
        Console.WriteLine("No");

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if
// array elements are consecutive

// Function to check if elements
// are consecutive
function areConsecutives($arr, $n)
{

    // Find minimum element in array
    $first_term = 9999999;

    for ($j = 0; $j < $n; $j++)
    {
        if($arr[$j] < $first_term)
            $first_term = $arr[$j];
    }

    // Calculate AP sum
    $ap_sum = intval(($n * (2 * $first_term +
                         ($n - 1) * 1)) / 2);

    // Calculate given array sum
    $arr_sum = 0;
    for ($i = 0; $i < $n; $i++)
        $arr_sum += $arr[$i];

    // Compare both sums and return
    return $ap_sum == $arr_sum;
}

// Driver code
$arr = array(2, 1, 0, -3, -1, -2);
$n = count($arr);

$result = areConsecutives($arr, $n);
if($result == true)
echo "Yes";
else
echo "No";

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// Javascript program to check if array elements
// are consecutive

    // Function to check if elements are
    // consecutive
    function areConsecutives(arr,n)
    {
        // Find minimum element in array
        let first_term = Number.MAX_VALUE;
        for (let j = 0; j < n; j++)
        {
            if(arr[j] < first_term)
                first_term = arr[j];
        }

        // Calculate AP sum
        let ap_sum = (n * (2 * first_term +
                         (n - 1) * 1)) / 2;

        // Calculate given array sum
        let arr_sum = 0;
        for (let i = 0; i < n; i++)
            arr_sum += arr[i];

        // Compare both sums and return
        return ap_sum == arr_sum;
    }

    // Driver code
    let arr=[2, 1, 0, -3, -1, -2 ];
    let n = arr.length;
    let result = areConsecutives(arr, n);
    if(result == true)
        document.write("Yes");
    else
        document.write("No");

    //This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
Yes
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)
本文由 [**萨希尔·查布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。