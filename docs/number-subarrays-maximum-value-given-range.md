# 给定范围内最大值的子阵数量

> 原文:[https://www . geesforgeks . org/number-subarrays-最大值-给定范围/](https://www.geeksforgeeks.org/number-subarrays-maximum-value-given-range/)

给定一个由 N 个元素以及 L 和 R 组成的数组，打印子数组的数量，使得该子数组中最大数组元素的值至少为 L，最多为 R

**示例:**

```
Input : arr[] = {2, 0, 11, 3, 0}
          L = 1, R = 10
Output : 4 
Explanation: the sub-arrays {2}, {2, 0}, {3} 
and {3, 0} have maximum in range 1-10.

Input : arr[] = {3, 4, 1}
          L = 2, R = 4 
Output : 5
Explanation: the sub-arrays are {3}, {4}, 
{3, 4}, {4, 1} and {3, 4, 1}  
```

一种**简单的方法**是对每个子阵列进行迭代，并找到在 L-R 范围内具有最大值的子阵列的数量。该解决方案的时间复杂度为 O(n*n)
一种**高效的**方法基于以下事实:

*   任何元素> R 从不包含在任何子阵列中。
*   只要 L 和 R 之间至少有一个元素，子阵列中可以包含任何数量的小于 L 的元素。
*   大小为 N 的阵列的所有可能子阵列的数量是 N * (N + 1)/2。让**计数子阵(N) = N * (N + 1)/2**

我们跟踪当前子阵列中的两个计数。
1)所有小于或等于 r 的元素的计数。我们称之为 **inc** 。
2)所有小于 l 的元素计数，我们称之为 exc。
我们对当前子阵列的回答是 countsbarray(Inc)–countsbarray(exc)。我们基本上去除了所有那些仅由小于 l 的元素构成的子阵列

以下是上述方法的实施情况-

## C++

```
// CPP program to count subarrays whose maximum
// elements are in given range.
#include <bits/stdc++.h>
using namespace std;

// function to calculate N*(N+1)/2
long countSubarrys(long n)
{
    return n * (n + 1) / 2;
}

// function to count the number of sub-arrays with
// maximum greater then L and less then R.
long countSubarrays(int a[], int n, int L, int R)
{
    long res = 0;

    // exc is going to store count of elements
    // smaller than L in current valid subarray.
    // inc is going to store count of elements
    // smaller than or equal to R.
    long exc = 0, inc = 0;

    // traverse through all elements of the array
    for (int i = 0; i < n; i++) {

        // If the element is greater than R,
        // add current value to result and reset
        // values of exc and inc.
        if (a[i] > R) {
            res += (countSubarrys(inc) - countSubarrys(exc));
            inc = 0;
            exc = 0;
        }

        // if it is less than L, then it is included
        // in the sub-arrays
        else if (a[i] < L) {
            exc++;
            inc++;
        }

        // if >= L and <= R, then count of
        // subarrays formed by previous chunk
        // of elements formed by only smaller
        // elements is reduced from result.
        else {
            res -= countSubarrys(exc);
            exc = 0;
            inc++;
        }
    }

    // Update result.
    res += (countSubarrys(inc) - countSubarrys(exc));

    // returns the count of sub-arrays
    return res;
}

// driver program
int main()
{
    int a[] = { 2, 0, 11, 3, 0 };
    int n = sizeof(a) / sizeof(a[0]);
    int l = 1, r = 10;
    cout << countSubarrays(a, n, l, r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count subarrays
// whose maximum elements are
// in given range.

class GFG {

// function to calculate N*(N+1)/2
static long countSubarrys(long n)
{
    return n * (n + 1) / 2;
}

// function to count the number of
// sub-arrays with maximum greater
// then L and less then R.
static long countSubarrays(int a[], int n,
                             int L, int R)
{
    long res = 0;

    // exc is going to store count of elements
    // smaller than L in current valid subarray.
    // inc is going to store count of elements
    // smaller than or equal to R.
    long exc = 0, inc = 0;

    // traverse through all elements of the array
    for (int i = 0; i < n; i++) {

    // If the element is greater than R,
    // add current value to result and reset
    // values of exc and inc.
    if (a[i] > R) {
        res += (countSubarrys(inc) - countSubarrys(exc));
        inc = 0;
        exc = 0;
    }

    // if it is less than L, then it is included
    // in the sub-arrays
    else if (a[i] < L) {
        exc++;
        inc++;
    }

    // if >= L and <= R, then count of
    // subarrays formed by previous chunk
    // of elements formed by only smaller
    // elements is reduced from result.
    else {
        res -= countSubarrys(exc);
        exc = 0;
        inc++;
    }
    }

    // Update result.
    res += (countSubarrys(inc) - countSubarrys(exc));

    // returns the count of sub-arrays
    return res;
}

// Driver code
public static void main(String arg[])
{
    int a[] = {2, 0, 11, 3, 0};
    int n = a.length;
    int l = 1, r = 10;
    System.out.print(countSubarrays(a, n, l, r));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to count
# subarrays whose maximum
# elements are in given range.

# function to calculate N*(N+1)/2
def countSubarrys(n):

    return n * (n + 1) // 2

# function to count the
# number of sub-arrays with
# maximum greater then
# L and less then R.
def countSubarrays(a,n,L,R):

    res = 0

    # exc is going to store
    # count of elements
    # smaller than L in
    # current valid subarray.
    # inc is going to store
    # count of elements
    # smaller than or equal to R.
    exc = 0
    inc = 0

    # traverse through all
    # elements of the array
    for i in range(n):

        # If the element is
        # greater than R,
        # add current value
        # to result and reset
        # values of exc and inc.
        if (a[i] > R):

            res =res + (countSubarrys(inc) - countSubarrys(exc))
            inc = 0
            exc = 0

        # if it is less than L,
        # then it is included
        # in the sub-arrays
        elif (a[i] < L):
            exc=exc + 1
            inc=inc + 1

        # if >= L and <= R, then count of
        # subarrays formed by previous chunk
        # of elements formed by only smaller
        # elements is reduced from result.
        else:

            res =res - countSubarrys(exc)
            exc = 0
            inc=inc + 1

    # Update result.
    res =res + (countSubarrys(inc) - countSubarrys(exc))

    # returns the count of sub-arrays
    return res

# Driver code

a = [ 2, 0, 11, 3, 0]
n =len(a)
l = 1
r = 10

print(countSubarrays(a, n, l, r))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to count subarrays
// whose maximum elements are
// in given range.
using System;

class GFG
{

// function to
// calculate N*(N+1)/2
static long countSubarrys(long n)
{
    return n * (n + 1) / 2;
}

// function to count the
// number of sub-arrays
// with maximum greater
// then L and less then R.
static long countSubarrays(int []a, int n,
                           int L, int R)
{
    long res = 0;

    // exc is going to store
    // count of elements smaller
    // than L in current valid
    // subarray. inc is going to
    // store count of elements
    // smaller than or equal to R.
    long exc = 0, inc = 0;

    // traverse through all
    // elements of the array
    for (int i = 0; i < n; i++)
    {

    // If the element is greater
    // than R, add current value
    // to result and reset values
    // of exc and inc.
    if (a[i] > R)
    {
        res += (countSubarrys(inc) -
                countSubarrys(exc));
        inc = 0;
        exc = 0;
    }

    // if it is less than L,
    // then it is included
    // in the sub-arrays
    else if (a[i] < L)
    {
        exc++;
        inc++;
    }

    // if >= L and <= R, then
    // count of subarrays formed
    // by previous chunk of elements
    // formed by only smaller elements
    // is reduced from result.
    else
    {
        res -= countSubarrys(exc);
        exc = 0;
        inc++;
    }
    }

    // Update result.
    res += (countSubarrys(inc) -
            countSubarrys(exc));

    // returns the count
    // of sub-arrays
    return res;
}

// Driver code
public static void Main()
{
    int []a = {2, 0, 11, 3, 0};
    int n = a.Length;
    int l = 1, r = 10;
    Console.WriteLine(countSubarrays(a, n,
                                     l, r));
}
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count subarrays
// whose maximum elements are in
// given range.

// function to calculate N*(N+1)/2
function countSubarrys($n)
{
    return $n * ($n + 1) / 2;
}

// function to count the number
// of sub-arrays with maximum
// greater then L and less then R.
function countSubarrays($a, $n,
                        $L, $R)
{
    $res = 0;

    // exc is going to store
    // count of elements smaller
    // than L in current valid
    // subarray. inc is going to
    // store count of elements
    // smaller than or equal to R.
    $exc = 0; $inc = 0;

    // traverse through all
    // elements of the array
    for ($i = 0; $i < $n; $i++)
    {

        // If the element is greater
        // than R, add current value
        // to result and reset values
        // of exc and inc.
        if ($a[$i] > $R)
        {
            $res += (countSubarrys($inc) -
                     countSubarrys($exc));
            $inc = 0;
            $exc = 0;
        }

        // if it is less than L,
        // then it is included
        // in the sub-arrays
        else if ($a[$i] < $L)
        {
            $exc++;
            $inc++;
        }

        // if >= L and <= R, then
        // count of subarrays formed
        // by previous chunk of elements
        // formed by only smaller elements
        // is reduced from result.
        else
        {
            $res -= countSubarrys($exc);
            $exc = 0;
            $inc++;
        }
    }

    // Update result.
    $res += (countSubarrys($inc) -
             countSubarrys($exc));

    // returns the count
    // of sub-arrays
    return $res;
}

// Driver Code
$a = array(2, 0, 11, 3, 0 );
$n = count($a);
$l = 1; $r = 10;
echo countSubarrays($a, $n, $l, $r);

// This code is contributed
// by anuj_67.
?>
```

## java 描述语言

```
<script>
// javascript program to count subarrays
// whose maximum elements are
// in given range.
    // function to calculate N*(N+1)/2
    function countSubarrys(n) {
        return n * (n + 1) / 2;
    }

    // function to count the number of
    // sub-arrays with maximum greater
    // then L and less then R.
    function countSubarrays(a , n , L , R) {
        var res = 0;

        // exc is going to store count of elements
        // smaller than L in current valid subarray.
        // inc is going to store count of elements
        // smaller than or equal to R.
        var exc = 0, inc = 0;

        // traverse through all elements of the array
        for (i = 0; i < n; i++) {

            // If the element is greater than R,
            // add current value to result and reset
            // values of exc and inc.
            if (a[i] > R) {
                res += (countSubarrys(inc) - countSubarrys(exc));
                inc = 0;
                exc = 0;
            }

            // if it is less than L, then it is included
            // in the sub-arrays
            else if (a[i] < L) {
                exc++;
                inc++;
            }

            // if >= L and <= R, then count of
            // subarrays formed by previous chunk
            // of elements formed by only smaller
            // elements is reduced from result.
            else {
                res -= countSubarrys(exc);
                exc = 0;
                inc++;
            }
        }

        // Update result.
        res += (countSubarrys(inc) - countSubarrys(exc));

        // returns the count of sub-arrays
        return res;
    }

    // Driver code
        var a = [ 2, 0, 11, 3, 0 ];
        var n = a.length;
        var l = 1, r = 10;
        document.write(countSubarrays(a, n, l, r));

// This code is contributed by todaysgaurav
</script>
```

**输出:**

```
4
```

**时间复杂度:** O(n)