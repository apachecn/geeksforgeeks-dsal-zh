# 求最小和，取每三个连续元素中的一个

> 原文:[https://www . geesforgeks . org/find-最小和-每三个连续元素取一个-take/](https://www.geeksforgeeks.org/find-minimum-sum-one-every-three-consecutive-elements-taken/)

给定一个非负数 **n** 的数组，任务是找到元素的最小和(从数组中选取)，以便在数组中每 3 个连续的元素中至少选取一个元素。
**例:**

```
Input : arr[] = {1, 2, 3}
Output : 1

Input : arr[] = {1, 2, 3, 6, 7, 1}
Output : 4
We pick 3 and 1  (3 + 1 = 4)
Note that there are following subarrays
of three consecutive elements
{1, 2, 3}, {2, 3, 6}, {3, 6, 7} and {6, 7, 1}
We have picked one element from every subarray.

Input : arr[] = {1, 2, 3, 6, 7, 1, 8, 6, 2,
                 7, 7, 1}
Output : 7
The result is obtained as sum of 3 + 1 + 2 + 1
```

当 arr[i]是解和的一部分(不一定是结果)并且是最后选择的元素时，设 sum(i)是最小可能和。那么我们的结果是和(n-1)、和(n-2)和和(n-3)的最小值[我们必须选择最后三个元素中的至少一个]。
我们可以递归地计算和(I)作为 arr[i]和最小值(和(i-1)，和(i-2)，和(i-3))的和。由于问题的递归结构中存在[重叠子问题](https://www.geeksforgeeks.org/dynamic-programming-set-1/)，我们可以使用动态规划来解决这个问题。
以下是以上思路的实现。

## C++

```
// A Dynamic Programming based C++ program to
// find minimum possible sum of elements of array
// such that an element out of every three
// consecutive is picked.
#include <iostream>
using namespace std;

// A utility function to find minimum of
// 3 elements
int minimum(int a, int b, int c)
{
    return min(min(a, b), c);
}

// Returns minimum possible sum of elements such
// that an element out of every three consecutive
// elements is picked.
int findMinSum(int arr[], int n)
{
    // Create a DP table to store results of
    // subproblems. sum[i] is going to store
    // minimum possible sum when arr[i] is
    // part of the solution.
    int sum[n];

    // When there are less than or equal to
    // 3 elements
    sum[0] = arr[0];
    sum[1] = arr[1];
    sum[2] = arr[2];

    // Iterate through all other elements
    for (int i=3; i<n; i++)
      sum[i] = arr[i] +
              minimum(sum[i-3], sum[i-2], sum[i-1]);

    return minimum(sum[n-1], sum[n-2], sum[n-3]);
}

// Driver code
int main()
{
    int arr[] = {1, 2, 3, 20, 2, 10, 1};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << "Min Sum is " << findMinSum(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Dynamic Programming based java program to
// find minimum possible sum of elements of array
// such that an element out of every three
// consecutive is picked.
import java.io.*;

class GFG
{
    // A utility function to find minimum of
    // 3 elements
    static int minimum(int a, int b, int c)
    {
        return Math. min(Math.min(a, b), c);
    }

    // Returns minimum possible sum of elements such
    // that an element out of every three consecutive
    // elements is picked.
    static int findMinSum(int arr[], int n)
    {
        // Create a DP table to store results of
        // subproblems. sum[i] is going to store
        // minimum possible sum when arr[i] is
        // part of the solution.
        int sum[] =new int[n];

        // When there are less than or equal to
        // 3 elements
        sum[0] = arr[0];
        sum[1] = arr[1];
        sum[2] = arr[2];

        // Iterate through all other elements
        for (int i = 3; i < n; i++)
        sum[i] = arr[i] + minimum(sum[i - 3],
                         sum[i - 2], sum[i - 1]);

        return minimum(sum[n - 1], sum[n - 2], sum[n - 3]);
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = {1, 2, 3, 20, 2, 10, 1};
        int n = arr.length;
        System.out.println("Min Sum is " + findMinSum(arr, n));

    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# A Dynamic Programming based python 3 program to
# find minimum possible sum of elements of array
# such that an element out of every three
# consecutive is picked.

# A utility function to find minimum of
# 3 elements
def minimum(a, b, c):
    return min(min(a, b), c);

# Returns minimum possible sum of elements such
# that an element out of every three consecutive
# elements is picked.
def findMinSum(arr,n):
    # Create a DP table to store results of
    # subproblems. sum[i] is going to store
    # minimum possible sum when arr[i] is
    # part of the solution.
    sum = []

    # When there are less than or equal to
    # 3 elements
    sum.append(arr[0])
    sum.append(arr[1])
    sum.append(arr[2])

    # Iterate through all other elements
    for i in range(3, n):
        sum.append( arr[i] + minimum(sum[i-3],
                           sum[i-2], sum[i-1]))

    return minimum(sum[n-1], sum[n-2], sum[n-3])

# Driver code
arr = [1, 2, 3, 20, 2, 10, 1]
n = len(arr)
print( "Min Sum is ",findMinSum(arr, n))

# This code is contributed by Sam007
```

## C#

```
// A Dynamic Programming based C# program to
// find minimum possible sum of elements of array
// such that an element out of every three
// consecutive is picked.
using System;

class GFG
{
    // A utility function to find minimum of
    // 3 elements
    static int minimum(int a, int b, int c)
    {
        return Math. Min(Math.Min(a, b), c);
    }

    // Returns minimum possible sum of elements such
    // that an element out of every three consecutive
    // elements is picked.
    static int findMinSum(int []arr, int n)
    {
        // Create a DP table to store results of
        // subproblems. sum[i] is going to store
        // minimum possible sum when arr[i] is
        // part of the solution.
        int []sum =new int[n];

        // When there are less than or equal to
        // 3 elements
        sum[0] = arr[0];
        sum[1] = arr[1];
        sum[2] = arr[2];

        // Iterate through all other elements
        for (int i = 3; i < n; i++)
        sum[i] = arr[i] + minimum(sum[i - 3],
                     sum[i - 2], sum[i - 1]);

        return minimum(sum[n - 1], sum[n - 2], sum[n - 3]);
    }

    // Driver code
    public static void Main ()
    {
        int []arr = {1, 2, 3, 20, 2, 10, 1};
        int n = arr.Length;
        Console.WriteLine("Min Sum is " + findMinSum(arr, n));

    }
}

//This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A Dynamic Programming based
// PHP program to find minimum
// possible sum of elements of
// array such that an element
// out of every three consecutive
// is picked.

// function to find minimum of
// 3 elements
function minimum($a, $b, $c)
{
    return min(min($a, $b), $c);
}

// Returns minimum possible sum
// of elements such that an
// element out of every three
// consecutive elements is picked.
function findMinSum($arr, $n)
{

    // Create a DP table to store results of
    // subproblems. sum[i] is going to store
    // minimum possible sum when arr[i] is
    // part of the solution.
    $sum[$n] = 0;

    // When there are less
    // than or equal to
    // 3 elements
    $sum[0] = $arr[0];
    $sum[1] = $arr[1];
    $sum[2] = $arr[2];

    // Iterate through all other elements
    for ($i = 3; $i < $n; $i++)
    $sum[$i] = $arr[$i] + minimum($sum[$i - 3],
                   $sum[$i - 2], $sum[$i - 1]);

    return minimum($sum[$n - 1], $sum[$n - 2],
                                $sum[$n - 3]);
}

    // Driver code
    $arr = array(1, 2, 3, 20, 2, 10, 1);
    $n = sizeof($arr);
    echo "Min Sum is " , findMinSum($arr, $n);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// A Dynamic Programming based Javascript program to
// find minimum possible sum of elements of array
// such that an element out of every three
// consecutive is picked.

// A utility function to find minimum of
// 3 elements
function minimum(a, b, c)
{
    return Math.min(Math.min(a, b), c);
}

// Returns minimum possible sum of elements such
// that an element out of every three consecutive
// elements is picked.
function findMinSum(arr, n)
{
    // Create a DP table to store results of
    // subproblems. sum[i] is going to store
    // minimum possible sum when arr[i] is
    // part of the solution.
    var sum= Array(n).fill(0);

    // When there are less than or equal to
    // 3 elements
    sum[0] = arr[0];
    sum[1] = arr[1];
    sum[2] = arr[2];

    // Iterate through all other elements
    for (var i=3; i<n; i++)
    sum[i] = arr[i] +
            minimum(sum[i-3], sum[i-2], sum[i-1]);

    return minimum(sum[n-1], sum[n-2], sum[n-3]);
}

// Driver code
var arr = [1, 2, 3, 20, 2, 10, 1];
var n = arr.length;
document.write( "Min Sum is " + findMinSum(arr, n));

</script>
```

**输出:**

```
Min Sum is 4
```

时间复杂度:O(n)
辅助空间:O(n)
这个问题和解决方案是由 [**阿尤什·萨卢加**](https://practice.geeksforgeeks.org/user-profile.php?user=Ayush%20Saluja) 贡献的。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。