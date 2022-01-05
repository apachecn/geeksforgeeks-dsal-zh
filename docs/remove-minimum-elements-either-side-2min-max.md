# 从两侧移除最小元素，使 2*min 大于最大值

> 原文:[https://www . geesforgeks . org/remove-最小元素-任一侧-2 分钟-最大值/](https://www.geeksforgeeks.org/remove-minimum-elements-either-side-2min-max/)

给定一个未排序的数组，修剪该数组，使得修剪后的数组中最小值的两倍大于最大值。元素应该从数组的两端移除。
清除的次数应该是最少的。

**示例:**

```
arr[] = {4, 5, 100, 9, 10, 11, 12, 15, 200}
Output: 4
We need to remove 4 elements (4, 5, 100, 200)
so that 2*min becomes more than max.

arr[] = {4, 7, 5, 6}
Output: 0
We don't need to remove any element as 
4*2 > 7 (Note that min = 4, max = 8)

arr[] = {20, 7, 5, 6}
Output: 1
We need to remove 20 so that 2*min becomes
more than max

arr[] = {20, 4, 1, 3}
Output: 3
We need to remove any three elements from ends
like 20, 4, 1 or 4, 1, 3 or 20, 3, 1 or 20, 4, 1
```

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/remove-minimum-elements4612/1)

**天真的解决方案:**
天真的解决方案是利用复发来尝试每一种可能的情况。下面是天真的递归算法。请注意，该算法只返回要进行的最小删除次数，它不打印修剪后的数组。也可以很容易地修改它来打印修剪过的数组。

```
// Returns minimum number of removals to be made in
// arr[l..h]
minRemovals(int arr[], int l, int h)
1) Find min and max in arr[l..h]
2) If 2*min > max, then return 0.
3) Else return minimum of "minRemovals(arr, l+1, h) + 1"
   and "minRemovals(arr, l, h-1) + 1"
```

下面是上述算法的实现。

## C++

```
// C++ implementation of above approach
#include <iostream>
using namespace std;

// A utility function to find minimum of two numbers
int min(int a, int b) {return (a < b)? a : b;}

// A utility function to find minimum in arr[l..h]
int min(int arr[], int l, int h)
{
    int mn = arr[l];
    for (int i=l+1; i<=h; i++)
       if (mn > arr[i])
         mn = arr[i];
    return mn;
}

// A utility function to find maximum in arr[l..h]
int max(int arr[], int l, int h)
{
    int mx = arr[l];
    for (int i=l+1; i<=h; i++)
       if (mx < arr[i])
         mx = arr[i];
    return mx;
}

// Returns the minimum number of removals from either end
// in arr[l..h] so that 2*min becomes greater than max.
int minRemovals(int arr[], int l, int h)
{
    // If there is 1 or less elements, return 0
    // For a single element, 2*min > max
    // (Assumption: All elements are positive in arr[])
    if (l >= h) return 0;

    // 1) Find minimum and maximum in arr[l..h]
    int mn = min(arr, l, h);
    int mx = max(arr, l, h);

    //If the property is followed, no removals needed
    if (2*mn > mx)
       return 0;

    // Otherwise remove a character from left end and recur,
    // then remove a character from right end and recur, take
    // the minimum of two is returned
    return min(minRemovals(arr, l+1, h),
               minRemovals(arr, l, h-1)) + 1;
}

// Driver program to test above functions
int main()
{
  int arr[] = {4, 5, 100, 9, 10, 11, 12, 15, 200};
  int n = sizeof(arr)/sizeof(arr[0]);
  cout << minRemovals(arr, 0, n-1);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG
{
// A utility function to find minimum of two numbers
static int min(int a, int b) {return (a < b)? a : b;}

// A utility function to find minimum in arr[l..h]
static int min(int arr[], int l, int h)
{
    int mn = arr[l];
    for (int i=l+1; i<=h; i++)
    if (mn > arr[i])
        mn = arr[i];
    return mn;
}

// A utility function to find maximum in arr[l..h]
static int max(int arr[], int l, int h)
{
    int mx = arr[l];
    for (int i=l+1; i<=h; i++)
    if (mx < arr[i])
        mx = arr[i];
    return mx;
}

// Returns the minimum number of removals from either end
// in arr[l..h] so that 2*min becomes greater than max.
static int minRemovals(int arr[], int l, int h)
{
    // If there is 1 or less elements, return 0
    // For a single element, 2*min > max
    // (Assumption: All elements are positive in arr[])
    if (l >= h) return 0;

    // 1) Find minimum and maximum in arr[l..h]
    int mn = min(arr, l, h);
    int mx = max(arr, l, h);

    //If the property is followed, no removals needed
    if (2*mn > mx)
    return 0;

    // Otherwise remove a character from left end and recur,
    // then remove a character from right end and recur, take
    // the minimum of two is returned
    return min(minRemovals(arr, l+1, h),
            minRemovals(arr, l, h-1)) + 1;
}

// Driver Code
public static void main(String[] args)
{
int arr[] = {4, 5, 100, 9, 10, 11, 12, 15, 200};
int n = arr.length;
System.out.print(minRemovals(arr, 0, n-1));
}
}

// This code is contributed by Mukul Singh.
```

## 蟒蛇 3

```
# Python3 implementation of above approach
# A utility function to find
# minimum in arr[l..h]
def mini(arr, l, h):
    mn = arr[l]
    for i in range(l + 1, h + 1):
        if (mn > arr[i]):
            mn = arr[i]
    return mn

# A utility function to find
# maximum in arr[l..h]
def max(arr, l, h):
    mx = arr[l]
    for i in range(l + 1, h + 1):
        if (mx < arr[i]):
            mx = arr[i]
    return mx

# Returns the minimum number of
# removals from either end in
# arr[l..h] so that 2*min becomes
# greater than max.
def minRemovals(arr, l, h):

    # If there is 1 or less elements, return 0
    # For a single element, 2*min > max
    # (Assumption: All elements are positive in arr[])
    if (l >= h):
        return 0

    # 1) Find minimum and maximum
    #    in arr[l..h]
    mn = mini(arr, l, h)
    mx = max(arr, l, h)

    # If the property is followed,
    # no removals needed
    if (2 * mn > mx):
        return 0

    # Otherwise remove a character from
    # left end and recur, then remove a
    # character from right end and recur,
    # take the minimum of two is returned
    return (min(minRemovals(arr, l + 1, h),
                minRemovals(arr, l, h - 1)) + 1)

# Driver Code
arr = [4, 5, 100, 9, 10,
       11, 12, 15, 200]
n = len(arr)
print(minRemovals(arr, 0, n - 1))

# This code is contributed
# by sahilshelangia
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{
// A utility function to find minimum of two numbers
static int min(int a, int b) {return (a < b)? a : b;}

// A utility function to find minimum in arr[l..h]
static int min(int[] arr, int l, int h)
{
    int mn = arr[l];
    for (int i=l+1; i<=h; i++)
    if (mn > arr[i])
        mn = arr[i];
    return mn;
}

// A utility function to find maximum in arr[l..h]
static int max(int[] arr, int l, int h)
{
    int mx = arr[l];
    for (int i=l+1; i<=h; i++)
    if (mx < arr[i])
        mx = arr[i];
    return mx;
}

// Returns the minimum number of removals from either end
// in arr[l..h] so that 2*min becomes greater than max.
static int minRemovals(int[] arr, int l, int h)
{
    // If there is 1 or less elements, return 0
    // For a single element, 2*min > max
    // (Assumption: All elements are positive in arr[])
    if (l >= h) return 0;

    // 1) Find minimum and maximum in arr[l..h]
    int mn = min(arr, l, h);
    int mx = max(arr, l, h);

    //If the property is followed, no removals needed
    if (2*mn > mx)
    return 0;

    // Otherwise remove a character from left end and recur,
    // then remove a character from right end and recur, take
    // the minimum of two is returned
    return min(minRemovals(arr, l+1, h),
            minRemovals(arr, l, h-1)) + 1;
}

// Driver Code
public static void Main()
{
int[] arr = {4, 5, 100, 9, 10, 11, 12, 15, 200};
int n = arr.Length;
Console.Write(minRemovals(arr, 0, n-1));
}
}

// This code is contributed by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// A utility function to find
// minimum in arr[l..h]
function min_1(&$arr, $l, $h)
{
    $mn = $arr[$l];
    for ($i = $l + 1; $i <= $h; $i++)
    if ($mn > $arr[$i])
        $mn = $arr[$i];
    return $mn;
}

// A utility function to find
// maximum in arr[l..h]
function max_1(&$arr, $l, $h)
{
    $mx = $arr[$l];
    for ($i = $l + 1; $i <= $h; $i++)
    if ($mx < $arr[$i])
        $mx = $arr[$i];
    return $mx;
}

// Returns the minimum number of removals
// from either end in arr[l..h] so that
// 2*min becomes greater than max.
function minRemovals(&$arr, $l, $h)
{
    // If there is 1 or less elements,
    // return 0\. For a single element,
    // 2*min > max. (Assumption: All
    // elements are positive in arr[])
    if ($l >= $h) return 0;

    // 1) Find minimum and maximum in arr[l..h]
    $mn = min_1($arr, $l, $h);
    $mx = max_1($arr, $l, $h);

    // If the property is followed,
    // no removals needed
    if (2 * $mn > $mx)
    return 0;

    // Otherwise remove a character from left
    // end and recur, then remove a character
    // from right end and recur, take the
    // minimum of two is returned
    return min(minRemovals($arr, $l + 1, $h),
               minRemovals($arr, $l, $h - 1)) + 1;
}

// Driver Code
$arr = array(4, 5, 100, 9, 10,
             11, 12, 15, 200);
$n = sizeof($arr);
echo minRemovals($arr, 0, $n - 1);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

    // A utility function to find minimum in arr[l..h]
    function min(arr,l,h)
    {
        let mn = arr[l];
        for (let i=l+1; i<=h; i++)
        {
            if (mn > arr[i])
                mn = arr[i];
        }
        return mn;
    }

    // A utility function to find maximum in arr[l..h]
    function max(arr,l,h)
    {
        let mx = arr[l];
        for (let i=l+1; i<=h; i++)
        {
            if (mx < arr[i])
                mx = arr[i];
        }
        return mx;
    }

    // Returns the minimum number of removals from either end
    // in arr[l..h] so that 2*min becomes greater than max.
    function minRemovals(arr,l,h)
    {

        // If there is 1 or less elements, return 0
        // For a single element, 2*min > max
        // (Assumption: All elements are positive in arr[])
        if (l >= h)
            return 0;

        // 1) Find minimum and maximum in arr[l..h]
        let mn = min(arr, l, h);
        let mx = max(arr, l, h);

        // If the property is followed, no removals needed
        if (2*mn > mx)
            return 0;

        // Otherwise remove a character from left end and recur,
        // then remove a character from right end and recur, take
        // the minimum of two is returned
        return Math.min(minRemovals(arr, l+1, h),minRemovals(arr, l, h-1)) + 1;
    }

    // Driver Code
    let arr = [4, 5, 100, 9, 10, 11, 12, 15, 200];
    let n = arr.length;
    document.write(minRemovals(arr, 0, n - 1));

    // This code is contributed by rag2127
</script>
```

**输出:**

```
 4 
```

**时间复杂度:**上述函数的时间复杂度可以写成

```
  T(n) = 2T(n-1) + O(n) 
```

上述递推的解的上界是 O(n×2<sup>n</sup>)。

**动态规划:**
上面的递归代码展示了许多重叠的子问题。例如，min removes(arr，l+1，h-1)被评估两次。因此，动态规划是优化解决方案的选择。以下是基于动态规划的解决方案。

## C++

```
// C++ program of above approach
#include <iostream>
using namespace std;

// A utility function to find minimum of two numbers
int min(int a, int b) {return (a < b)? a : b;}

// A utility function to find minimum in arr[l..h]
int min(int arr[], int l, int h)
{
    int mn = arr[l];
    for (int i=l+1; i<=h; i++)
       if (mn > arr[i])
         mn = arr[i];
    return mn;
}

// A utility function to find maximum in arr[l..h]
int max(int arr[], int l, int h)
{
    int mx = arr[l];
    for (int i=l+1; i<=h; i++)
       if (mx < arr[i])
         mx = arr[i];
    return mx;
}

// Returns the minimum number of removals from either end
// in arr[l..h] so that 2*min becomes greater than max.
int minRemovalsDP(int arr[], int n)
{
    // Create a table to store solutions of subproblems
    int table[n][n], gap, i, j, mn, mx;

    // Fill table using above recursive formula. Note that the table
    // is filled in diagonal fashion (similar to http://goo.gl/PQqoS),
    // from diagonal elements to table[0][n-1] which is the result.
    for (gap = 0; gap < n; ++gap)
    {
        for (i = 0, j = gap; j < n; ++i, ++j)
        {
            mn = min(arr, i, j);
            mx = max(arr, i, j);
            table[i][j] = (2*mn > mx)? 0: min(table[i][j-1]+1,
                                              table[i+1][j]+1);
        }
    }
    return table[0][n-1];
}

// Driver program to test above functions
int main()
{
  int arr[] = {20, 4, 1, 3};
  int n = sizeof(arr)/sizeof(arr[0]);
  cout << minRemovalsDP(arr, n);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of above approach
class GFG {

// A utility function to find minimum of two numbers
    static int min(int a, int b) {
        return (a < b) ? a : b;
    }

// A utility function to find minimum in arr[l..h]
    static int min(int arr[], int l, int h) {
        int mn = arr[l];
        for (int i = l + 1; i <= h; i++) {
            if (mn > arr[i]) {
                mn = arr[i];
            }
        }
        return mn;
    }

// A utility function to find maximum in arr[l..h]
    static int max(int arr[], int l, int h) {
        int mx = arr[l];
        for (int i = l + 1; i <= h; i++) {
            if (mx < arr[i]) {
                mx = arr[i];
            }
        }
        return mx;
    }

// Returns the minimum number of removals from either end
// in arr[l..h] so that 2*min becomes greater than max.
    static int minRemovalsDP(int arr[], int n) {
        // Create a table to store solutions of subproblems
        int table[][] = new int[n][n], gap, i, j, mn, mx;

        // Fill table using above recursive formula. Note that the table
        // is filled in diagonal fashion (similar to http://goo.gl/PQqoS),
        // from diagonal elements to table[0][n-1] which is the result.
        for (gap = 0; gap < n; ++gap) {
            for (i = 0, j = gap; j < n; ++i, ++j) {
                mn = min(arr, i, j);
                mx = max(arr, i, j);
                table[i][j] = (2 * mn > mx) ? 0 : min(table[i][j - 1] + 1,
                        table[i + 1][j] + 1);
            }
        }
        return table[0][n - 1];
    }

// Driver program to test above functions
    public static void main(String[] args) {
        int arr[] = {20, 4, 1, 3};
        int n = arr.length;
        System.out.println(minRemovalsDP(arr, n));

    }
}
// This code contributed by 29AJayKumar
```

## 蟒蛇 3

```
# Python3 program of above approach

# A utility function to find
# minimum in arr[l..h]
def min1(arr, l, h):
    mn = arr[l];
    for i in range(l + 1,h+1):
        if (mn > arr[i]):
            mn = arr[i];
    return mn;

# A utility function to find
# maximum in arr[l..h]
def max1(arr, l, h):
    mx = arr[l];
    for i in range(l + 1, h + 1):
        if (mx < arr[i]):
            mx = arr[i];
    return mx;

# Returns the minimum number of removals
# from either end in arr[l..h] so that
# 2*min becomes greater than max.
def minRemovalsDP(arr, n):

    # Create a table to store
    # solutions of subproblems
    table = [[0 for x in range(n)] for y in range(n)];

    # Fill table using above recursive formula.
    # Note that the table is filled in diagonal fashion
    # (similar to http:#goo.gl/PQqoS), from diagonal elements
    # to table[0][n-1] which is the result.
    for gap in range(n):
        i = 0;
        for j in range(gap,n):
            mn = min1(arr, i, j);
            mx = max1(arr, i, j);
            table[i][j] = 0 if (2 * mn > mx) else min(table[i][j - 1] + 1,table[i + 1][j] + 1);
            i += 1;
    return table[0][n - 1];

# Driver Code
arr = [20, 4, 1, 3];
n = len(arr);
print(minRemovalsDP(arr, n));

# This code is contributed by mits
```

## C#

```
// C# program of above approach
using System;

public class GFG {

    // A utility function to find minimum of two numbers
    static int min(int a, int b) {
        return (a < b) ? a : b;
    }

    // A utility function to find minimum in arr[l..h]
    static int min(int []arr, int l, int h) {
        int mn = arr[l];
        for (int i = l + 1; i <= h; i++) {
            if (mn > arr[i]) {
                mn = arr[i];
            }
        }
        return mn;
    }

// A utility function to find maximum in arr[l..h]
    static int max(int []arr, int l, int h) {
        int mx = arr[l];
        for (int i = l + 1; i <= h; i++) {
            if (mx < arr[i]) {
                mx = arr[i];
            }
        }
        return mx;
    }

    // Returns the minimum number of removals from either end
    // in arr[l..h] so that 2*min becomes greater than max.
    static int minRemovalsDP(int []arr, int n) {
        // Create a table to store solutions of subproblems
        int [,]table = new int[n,n];
        int gap, i, j, mn, mx;

        // Fill table using above recursive formula. Note that the table
        // is filled in diagonal fashion (similar to http://goo.gl/PQqoS),
        // from diagonal elements to table[0][n-1] which is the result.
        for (gap = 0; gap < n; ++gap) {
            for (i = 0, j = gap; j < n; ++i, ++j) {
                mn = min(arr, i, j);
                mx = max(arr, i, j);
                table[i,j] = (2 * mn > mx) ? 0 : min(table[i,j - 1] + 1,
                        table[i + 1,j] + 1);
            }
        }
        return table[0,n - 1];
    }

    // Driver program to test above functions
    public static void Main() {
        int []arr = {20, 4, 1, 3};
        int n = arr.Length;
        Console.WriteLine(minRemovalsDP(arr, n));

    }
}
// This code contributed by 29AJayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program of above approach

// A utility function to find
// minimum in arr[l..h]
function min1($arr, $l, $h)
{
    $mn = $arr[$l];
    for ($i = $l + 1; $i <= $h; $i++)
    if ($mn > $arr[$i])
        $mn = $arr[$i];
    return $mn;
}

// A utility function to find
// maximum in arr[l..h]
function max1($arr, $l, $h)
{
    $mx = $arr[$l];
    for ($i = $l + 1; $i <= $h; $i++)
    if ($mx < $arr[$i])
        $mx = $arr[$i];
    return $mx;
}

// Returns the minimum number of removals
// from either end in arr[l..h] so that
// 2*min becomes greater than max.
function minRemovalsDP($arr, $n)
{

    // Create a table to store
    // solutions of subproblems
    $table = array_fill(0, $n,
             array_fill(0, $n, 0));

    // Fill table using above recursive formula.
    // Note that the table is filled in diagonal fashion
    // (similar to http://goo.gl/PQqoS), from diagonal elements
    // to table[0][n-1] which is the result.
    for ($gap = 0; $gap < $n; ++$gap)
    {
        for ($i = 0, $j = $gap; $j < $n; ++$i, ++$j)
        {
            $mn = min1($arr, $i, $j);
            $mx = max1($arr, $i, $j);
            $table[$i][$j] = (2 * $mn > $mx) ? 0 :
                              min($table[$i][$j - 1] + 1,
                                  $table[$i + 1][$j] + 1);
        }
    }
    return $table[0][$n - 1];
}

// Driver Code
$arr = array(20, 4, 1, 3);
$n = count($arr);
echo minRemovalsDP($arr, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program of above approach   

// A utility function to find minimum
// of two numbers
function minq(a, b)
{
    return (a < b) ? a : b;
}

// A utility function to find minimum
// in arr[l..h]
function min(arr, l, h)
{
    var mn = arr[l];
    for(i = l + 1; i <= h; i++)
    {
        if (mn > arr[i])
        {
            mn = arr[i];
        }
    }
    return parseInt(mn);
}

// A utility function to find maximum in arr[l..h]
function max(arr, l, h)
{
    var mx = arr[l];
    for(i = l + 1; i <= h; i++)
    {
        if (mx < arr[i])
        {
            mx = arr[i];
        }
    }
    return parseInt(mx);
}

// Returns the minimum number of removals
// from either end in arr[l..h] so that
// 2*min becomes greater than max.
function minRemovalsDP(arr, n)
{

    // Create a table to store solutions
    // of subproblems
    var table = Array(n);
    var gap, i, j, mn, mx;

    for(i = 0; i < n; i++)
        table[i] = Array(n).fill(0);

    // Fill table using above recursive formula.
    // Note that the table is filled in diagonal
    // fashion (similar to http://goo.gl/PQqoS),
    // from diagonal elements to table[0][n-1]
    // which is the result.
    for(gap = 0; gap < n; ++gap)
    {
        for(i = 0, j = gap; j < n; ++i, ++j)
        {
            mn = min(arr, i, j);
            mx = max(arr, i, j);
            table[i][j] = parseInt((2 * mn > mx) ?
                  0 : minq(table[i][j - 1] + 1,
                           table[i + 1][j] + 1));
        }
    }
    return table[0][n - 1];
}

// Driver code
var arr = [ 20, 4, 1, 3 ];
var n = arr.length;

document.write(minRemovalsDP(arr, n));

// This code is contributed by gauravrajput1

</script>
```

**输出:**

```
 3
```

**时间复杂度:** O(n <sup>3</sup> )，其中 n 是 arr[]中的元素个数。

进一步优化:
以上代码可以通过多种方式进行优化。
**1)** 当最小和/或最大值没有通过移除角元素来改变时，我们可以避免计算最小()和/或最大()。
**2)** 我们可以对数组进行预处理，在 O(n)时间内构建[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)。在建立段树后，我们可以在 O(Logn)时间内查询范围最小值和最大值。整体时间复杂度降低到 O(n <sup>2</sup> Logn)时间。
**A O(n^2)解决方案**
的思路是找到尺寸最大的子阵列，使得 2*min > max。我们运行两个嵌套循环，外部循环选择一个起点，内部循环选择当前起点的终点。我们跟踪具有给定属性的最长子阵列。

下面是上述方法的实现。感谢张曦轲提出这个解决方案。

## C++

```
// A O(n*n) solution to find the minimum of elements to
// be removed
#include <iostream>
#include <climits>
using namespace std;

// Returns the minimum number of removals from either end
// in arr[l..h] so that 2*min becomes greater than max.
int minRemovalsDP(int arr[], int n)
{
    // Initialize starting and ending indexes of the maximum
    // sized subarray with property 2*min > max
    int longest_start = -1, longest_end = 0;

    // Choose different elements as starting point
    for (int start=0; start<n; start++)
    {
        // Initialize min and max for the current start
        int min = INT_MAX, max = INT_MIN;

        // Choose different ending points for current start
        for (int end = start; end < n; end ++)
        {
            // Update min and max if necessary
            int val = arr[end];
            if (val < min) min = val;
            if (val > max) max = val;

            // If the property is violated, then no
            // point to continue for a bigger array
            if (2 * min <= max) break;

            // Update longest_start and longest_end if needed
            if (end - start > longest_end - longest_start ||
                longest_start == -1)
            {
                longest_start = start;
                longest_end = end;
            }
        }
    }

    // If not even a single element follow the property,
    // then return n
    if (longest_start == -1) return n;

    // Return the number of elements to be removed
    return (n - (longest_end - longest_start + 1));
}

// Driver program to test above functions
int main()
{
    int arr[] = {4, 5, 100, 9, 10, 11, 12, 15, 200};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << minRemovalsDP(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A O(n*n) solution to find the minimum of elements to
// be removed

class GFG {

// Returns the minimum number of removals from either end
// in arr[l..h] so that 2*min becomes greater than max.
    static int minRemovalsDP(int arr[], int n) {
        // Initialize starting and ending indexes of the maximum
        // sized subarray with property 2*min > max
        int longest_start = -1, longest_end = 0;

        // Choose different elements as starting point
        for (int start = 0; start < n; start++) {
            // Initialize min and max for the current start
            int min = Integer.MAX_VALUE, max = Integer.MIN_VALUE;

            // Choose different ending points for current start
            for (int end = start; end < n; end++) {
                // Update min and max if necessary
                int val = arr[end];
                if (val < min) {
                    min = val;
                }
                if (val > max) {
                    max = val;
                }

                // If the property is violated, then no
                // point to continue for a bigger array
                if (2 * min <= max) {
                    break;
                }

                // Update longest_start and longest_end if needed
                if (end - start > longest_end - longest_start
                        || longest_start == -1) {
                    longest_start = start;
                    longest_end = end;
                }
            }
        }

        // If not even a single element follow the property,
        // then return n
        if (longest_start == -1) {
            return n;
        }

        // Return the number of elements to be removed
        return (n - (longest_end - longest_start + 1));
    }

// Driver program to test above functions
    public static void main(String[] args) {
        int arr[] = {4, 5, 100, 9, 10, 11, 12, 15, 200};
        int n = arr.length;
        System.out.println(minRemovalsDP(arr, n));
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# A O(n*n) solution to find the minimum of
# elements to be removed
import sys;

# Returns the minimum number of removals
# from either end in arr[l..h] so that
# 2*min becomes greater than max.
def minRemovalsDP(arr, n):

    # Initialize starting and ending indexes
    # of the maximum sized subarray
    # with property 2*min > max
    longest_start = -1;
    longest_end = 0;

    # Choose different elements as starting point
    for start in range(n):

        # Initialize min and max
        # for the current start
        min = sys.maxsize;
        max = -sys.maxsize;

        # Choose different ending points for current start
        for end in range(start,n):
            # Update min and max if necessary
            val = arr[end];
            if (val < min):
                min = val;
            if (val > max):
                max = val;

            # If the property is violated, then no
            # point to continue for a bigger array
            if (2 * min <= max):
                break;

            # Update longest_start and longest_end if needed
            if (end - start > longest_end - longest_start or longest_start == -1):
                longest_start = start;
                longest_end = end;

    # If not even a single element follow the property,
    # then return n
    if (longest_start == -1):
        return n;

    # Return the number of elements to be removed
    return (n - (longest_end - longest_start + 1));

# Driver Code
arr = [4, 5, 100, 9, 10, 11, 12, 15, 200];
n = len(arr);
print(minRemovalsDP(arr, n));

# This code is contributed by mits
```

## C#

```
// A O(n*n) solution to find the minimum of elements to
// be removed

using System;
public class GFG {

// Returns the minimum number of removals from either end
// in arr[l..h] so that 2*min becomes greater than max.
    static int minRemovalsDP(int []arr, int n) {
        // Initialize starting and ending indexes of the maximum
        // sized subarray with property 2*min > max
        int longest_start = -1, longest_end = 0;

        // Choose different elements as starting point
        for (int start = 0; start < n; start++) {
            // Initialize min and max for the current start
            int min = int.MaxValue, max = int.MinValue;

            // Choose different ending points for current start
            for (int end = start; end < n; end++) {
                // Update min and max if necessary
                int val = arr[end];
                if (val < min) {
                    min = val;
                }
                if (val > max) {
                    max = val;
                }

                // If the property is violated, then no
                // point to continue for a bigger array
                if (2 * min <= max) {
                    break;
                }

                // Update longest_start and longest_end if needed
                if (end - start > longest_end - longest_start
                        || longest_start == -1) {
                    longest_start = start;
                    longest_end = end;
                }
            }
        }

        // If not even a single element follow the property,
        // then return n
        if (longest_start == -1) {
            return n;
        }

        // Return the number of elements to be removed
        return (n - (longest_end - longest_start + 1));
    }

// Driver program to test above functions
    public static void Main() {
        int []arr = {4, 5, 100, 9, 10, 11, 12, 15, 200};
        int n = arr.Length;
        Console.WriteLine(minRemovalsDP(arr, n));
    }
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A O(n*n) solution to find the minimum of
// elements to be removed

// Returns the minimum number of removals
// from either end in arr[l..h] so that
// 2*min becomes greater than max.
function minRemovalsDP($arr, $n)
{
    // Initialize starting and ending indexes
    // of the maximum sized subarray
    // with property 2*min > max
    $longest_start = -1;
    $longest_end = 0;

    // Choose different elements as starting point
    for ($start = 0; $start < $n; $start++)
    {

        // Initialize min and max
        // for the current start
        $min = PHP_INT_MAX;
        $max = PHP_INT_MIN;

        // Choose different ending points for current start
        for ($end = $start; $end < $n; $end ++)
        {
            // Update min and max if necessary
            $val = $arr[$end];
            if ($val < $min) $min = $val;
            if ($val > $max) $max = $val;

            // If the property is violated, then no
            // point to continue for a bigger array
            if (2 * $min <= $max) break;

            // Update longest_start and longest_end if needed
            if ($end - $start > $longest_end - $longest_start ||
                $longest_start == -1)
            {
                $longest_start = $start;
                $longest_end = $end;
            }
        }
    }

    // If not even a single element follow the property,
    // then return n
    if ($longest_start == -1) return $n;

    // Return the number of elements to be removed
    return ($n - ($longest_end - $longest_start + 1));
}

// Driver Code
$arr = array(4, 5, 100, 9, 10, 11, 12, 15, 200);
$n = sizeof($arr);
echo minRemovalsDP($arr, $n);

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>

// A O(n*n) solution to find the minimum of elements to
// be removed

    // Returns the minimum number of removals from either end
    // in arr[l..h] so that 2*min becomes greater than max.
    function minRemovalsDP(arr,n)
    {
        // Initialize starting and ending indexes of the maximum
        // sized subarray with property 2*min > max
        let longest_start = -1, longest_end = 0;

        // Choose different elements as starting point
        for (let start = 0; start < n; start++)
        {
            // Initialize min and max for the current start
            let  min = Number.MAX_VALUE, max = Number.MIN_VALUE;

            // Choose different ending points for current start
            for (let end = start; end < n; end++)
            {
                // Update min and max if necessary
                let val = arr[end];
                if (val < min)
                {
                    min = val;
                }
                if (val > max)
                {
                    max = val;
                }
                // If the property is violated, then no
                // point to continue for a bigger array
                if (2 * min <= max)
                {
                    break;
                }

                // Update longest_start and longest_end if needed
                if (end - start > longest_end - longest_start
                        || longest_start == -1)
                {
                    longest_start = start;
                    longest_end = end;
                }

            }
        }
        // If not even a single element follow the property,
        // then return n
        if (longest_start == -1)
        {
            return n;
        }
        // Return the number of elements to be removed
        return (n - (longest_end - longest_start + 1));
    }

    // Driver program to test above functions
    let arr=[4, 5, 100, 9, 10, 11, 12, 15, 200];
    let n = arr.length;
    document.write(minRemovalsDP(arr, n));

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
4
```

本文由**拉胡尔·贾恩**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息