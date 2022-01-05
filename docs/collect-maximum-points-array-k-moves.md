# 用 k 次移动收集数组中的最大点数

> 原文:[https://www . geeksforgeeks . org/collect-最大点数-数组-k-moves/](https://www.geeksforgeeks.org/collect-maximum-points-array-k-moves/)

给定一个由整数和两个值 k 和 I 组成的数组，其中 k 是移动次数，I 是数组中的索引。任务是通过从给定的索引 I 单向或双向移动并进行 k 次移动来收集数组中的最大点。请注意，访问的每个数组元素都被视为一个移动，包括 arr[i]。
**约束:**
n 是阵的大小。
0<= I<n .
1<= k<= n

**示例:**

```
Input  :  arr[] = { 5, 6, 4, 2, 8, 3, 1 }  
          k = 3, i = 3  
Output :  Maximum point: 14         

Explanation: arr[i] is 2
All possible ways to collect points in the array 
by moving either both or a single direction are:
  case 1:  6 + 4 + 2 = 12
  case 2:  4 + 2 + 8 = 14
  case 3:  2 + 8 + 3 = 13      
So maximum points we collects in k moves  : 14

Input  : arr[] = { 5, 6, 4, 2, 8, 3, 1 }
         k = 2, i = 5
Output : Maximum point: 11 ( 8 + 3 ) 
```

一个**简单的解决方案**就是生成 k 大小的所有子阵(有一点要注意，我们只生成包含索引(I)的子阵)，计算它们的和，最后返回所有和的最大值。这个解的时间复杂度是 O(n*k)

一个**有效的解决方案**是基于文章[大小为 k](https://www.geeksforgeeks.org/find-maximum-minimum-sum-subarray-size-k/) 的最大和 _ 子数组。这个想法是利用这样一个事实，即大小为 k 的子阵列的和可以通过使用大小为 k 的前一个子阵列的和来获得。除了大小为 k 的第一个子阵列之外，对于其他子阵列，我们通过移除最后一个窗口的第一个元素并添加当前窗口的最后一个元素来计算和。
时间复杂度:O(n)
以下是上述思路的实现。

## C++

```
// C++ program to Collect maximum point
// in array with k moves.
#include <iostream>
using namespace std;

// function return maximum point 
// that we can collect with K moves
int maximumPoints(int arr[], int n, int k, int i)
{
    // Compute sum of first window of size k in which
    // we consider subArray from index ( 'i-k' to 'i' )
    // store starting index of sub_array
    int start;
    if (k > i)

        // sub_array from ( 0 to I+(K-I))
        start = 0;
    else

        // sub_array from ( i-i, to i )
        start = i - k;

    int res = 0;
    for (int j = start; j <= start + k && j < n; j++)
        res += arr[j];

    // Compute sums of remaining windows by
    // removing first element of previous
    // window and adding last element of
    // current window.
    int curr_sum = res;
    for (int j = start + k + 1; j < n && j <= i + k; j++)
    {
        curr_sum += arr[j] - arr[j - k - 1];
        res = max(res, curr_sum);
    }
    return res;
}

// Driver code
int main()
{
    int arr[] = { 5, 6, 4, 2, 8, 3, 1 };
    int k = 3, i = 3;
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Maximum points : "
        << maximumPoints(arr, n, k - 1, i);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Collect maximum point
// in array with k moves.
class GFG {

    // function return maximum point
    // that we can collect with K moves
    static int maximumPoints(int arr[], int n, int k, int i)
    {

        // Compute sum of first window of size k in which
        // we consider subArray from index ( 'i-k' to 'i' )
        // store starting index of sub_array
        int start;

        if (k > i)

            // sub_array from ( 0 to I+(K-I))
            start = 0;
        else

            // sub_array from ( i-i, to i )
            start = i - k;

        int res = 0;

        for (int j = start; j <= start + k && j < n; j++)
            res += arr[j];

        // Compute sums of remaining windows by
        // removing first element of previous
        // window and adding last element of
        // current window.
        int curr_sum = res;

        for (int j = start + k + 1; j < n && j <= i + k; j++)
        {
            curr_sum += arr[j] - arr[j - k - 1];
            res = Math.max(res, curr_sum);
        }

        return res;
    }

    // driver code
    public static void main (String[] args)
    {

        int arr[] = { 5, 6, 4, 2, 8, 3, 1 };
        int k = 3, i = 3;
        int n = arr.length;

        System.out.print("Maximum points : "
            +maximumPoints(arr, n, k - 1, i));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to Collect maximum point
# in array with k moves.

# function return maximum point
# that we can collect with K moves
def maximumPoints(arr, n, k, i):

    # Compute sum of first window of size k in which
    # we consider subArray from index ( 'i-k' to 'i' )
    # store starting index of sub_array
    start = 0
    if (k > i):

        # sub_array from ( 0 to I+(K-I))
        start = 0
    else:

        # sub_array from ( i-i, to i )
        start = i - k

    res = 0
    j = start
    while(j <= start + k and j < n):
        res += arr[j]
        j += 1

    # Compute sums of remaining windows by
    # removing first element of previous
    # window and adding last element of
    # current window.
    curr_sum = res
    j = start + k + 1
    while(j < n and j <= i + k):
        curr_sum += arr[j] - arr[j - k - 1]
        res = max(res, curr_sum)
        j += 1
    return res

# Driver code
arr = [ 5, 6, 4, 2, 8, 3, 1 ]
k, i = 3, 3
n = len(arr)
print ("Maximum points :", maximumPoints(arr, n, k - 1, i))

# This code is contributed by Sachin Bisht
```

## C#

```
// C# program to Collect maximum point
// in array with k moves.
using System;

class GFG {

    // function return maximum point 
    // that we can collect with K moves
    static int maximumPoints(int []arr, int n, int k, int i)
    {

        // Compute sum of first window of size k
        // in which we consider subArray from
        // index ( 'i-k' to 'i' ) and store
        // starting index of sub_array
        int start;

        if (k > i)

            // sub_array from ( 0 to I+(K-I))
            start = 0;
        else

            // sub_array from ( i-i, to i )
            start = i - k;

        int res = 0;

        for (int j = start; j <= start + k && j < n; j++)
            res += arr[j];

        // Compute sums of remaining windows by
        // removing first element of previous
        // window and adding last element of
        // current window.
        int curr_sum = res;

        for (int j = start + k + 1; j < n && j <= i + k; j++)
        {
            curr_sum += arr[j] - arr[j - k - 1];
            res = Math.Max(res, curr_sum);
        }

        return res;
    }

    // driver code
    public static void Main ()
    {

        int []arr = { 5, 6, 4, 2, 8, 3, 1 };
        int k = 3, i = 3;
        int n = arr.Length;

        Console.Write("Maximum points : "
            +maximumPoints(arr, n, k - 1, i));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Collect maximum
// points in array with k moves.

// function return maximum po$
// that we can collect with K moves
function maximumPo($arr, $n, $k, $i)
{

    // Compute sum of first
    // window of size k in which
    // we consider subArray from
    // index ( 'i-k' to 'i' )
    // store starting index of
    // sub_array
    $start;
    if ($k > $i)

        // sub_array from (0 to
        // I + (K - I))
        $start = 0;
    else

        // sub_array from (i - i, to i )
        $start = $i - $k;

    $res = 0;
    for ($j = $start; $j <= $start +
               $k and $j < $n; $j++)
        $res += $arr[$j];

    // Compute sums of remaining windows by
    // removing first element of previous
    // window and adding last element of
    // current window.
    $curr_sum = $res;
    for ($j = $start + $k + 1; $j < $n and
                      $j <= $i + $k; $j++)
    {
        $curr_sum += $arr[$j] - $arr[$j - $k - 1];
        $res = max($res, $curr_sum);
    }
    return $res;
}

    // Driver code
    $arr = array(5, 6, 4, 2, 8, 3, 1);
    $k = 3; $i = 3;
    $n = count($arr);
    echo "Maximum pos : ",
        maximumPo($arr, $n, $k - 1, $i);

// This code is contributed by anuj_67
?>
```

## java 描述语言

```
<script>

// Javascript program to Collect maximum point
// in array with k moves.

// function return maximum point 
// that we can collect with K moves
function maximumPoints(arr, n, k, i)
{
    // Compute sum of first window of size k in which
    // we consider subArray from index ( 'i-k' to 'i' )
    // store starting index of sub_array
    var start;
    if (k > i)

        // sub_array from ( 0 to I+(K-I))
        start = 0;
    else

        // sub_array from ( i-i, to i )
        start = i - k;

    var res = 0;
    for (var j = start; j <= start + k && j < n; j++)
        res += arr[j];

    // Compute sums of remaining windows by
    // removing first element of previous
    // window and adding last element of
    // current window.
    var curr_sum = res;
    for (var j = start + k + 1; j < n && j <= i + k; j++)
    {
        curr_sum += arr[j] - arr[j - k - 1];
        res = Math.max(res, curr_sum);
    }
    return res;
}

// Driver code
var arr = [ 5, 6, 4, 2, 8, 3, 1 ];
var k = 3, i = 3;
var n = arr.length;
document.write( "Maximum points : "
    + maximumPoints(arr, n, k - 1, i));

</script>
```

**输出:**

```
Maximum point : 14 
```

时间复杂度:O(n)
辅助空间:O(1)

本文由 [**尼尚·辛格**](https://www.facebook.com/nishant.chaudhary.7334) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。