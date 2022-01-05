# 在给定范围内求和的子阵列数量

> 原文:[https://www . geeksforgeeks . org/给定范围内具有总和的子阵列数量/](https://www.geeksforgeeks.org/number-of-subarrays-having-sum-in-a-given-range/)

给定一个正整数数组 arr[]和一个范围(L，R)。求和在范围 L 到 r 内的子阵的数目
**例:**

```
Input : arr[] = {1, 4, 6}, L = 3, R = 8
Output : 3
The subarrays are {1, 4}, {4}, {6}.

Input : arr[] = {2, 3, 5, 8}, L = 4, R = 13
Output : 6
The subarrays are {2, 3}, {2, 3, 5}, {3, 5},
{5}, {5, 8}, {8}.
```

[Recommended: Please try your approach first on IDE and then look at the solution.](https://ide.geeksforgeeks.org) 

一个**简单的**解法就是逐个考虑每个子阵，求其和。如果总和在[L，R]范围内，则增加计数。这个解决方案的时间复杂度是 O(n^2).
一个**有效的**解决方案是首先找到和小于或等于 r 的子阵列的数量。从这个计数中，减去和小于或等于 L-1 的子阵列的数量。为了找到和小于或等于给定值的子阵数量，使用了下面文章中讨论的使用滑动窗口的线性时间方法:
[和小于或等于 k 的子阵数量](https://www.geeksforgeeks.org/number-subarrays-sum-less-k/)。
以下是上述方法的实施:

## C++

```
// CPP program to find number of subarrays having
// sum in the range L to R.
#include <bits/stdc++.h>
using namespace std;

// Function to find number of subarrays having
// sum less than or equal to x.
int countSub(int arr[], int n, int x)
{

    // Starting index of sliding window.
    int st = 0;

    // Ending index of sliding window.
    int end = 0;

    // Sum of elements currently present
    // in sliding window.
    int sum = 0;

    // To store required number of subarrays.
    int cnt = 0;

    // Increment ending index of sliding
    // window one step at a time.
    while (end < n) {

        // Update sum of sliding window on
        // adding a new element.
        sum += arr[end];

        // Increment starting index of sliding
        // window until sum is greater than x.
        while (st <= end && sum > x) {
            sum -= arr[st];
            st++;
        }

        // Update count of number of subarrays.
        cnt += (end - st + 1);
        end++;
    }

    return cnt;
}

// Function to find number of subarrays having
// sum in the range L to R.
int findSubSumLtoR(int arr[], int n, int L, int R)
{

    // Number of subarrays having sum less
    // than or equal to R.
    int Rcnt = countSub(arr, n, R);

    // Number of subarrays having sum less
    // than or equal to L-1.
    int Lcnt = countSub(arr, n, L - 1);

    return Rcnt - Lcnt;
}

// Driver code.
int main()
{
    int arr[] = { 1, 4, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    int L = 3;
    int R = 8;

    cout << findSubSumLtoR(arr, n, L, R);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number
// of subarrays having sum in
// the range L to R.
import java.io.*;

class GFG
{

    // Function to find number
    // of subarrays having sum
    // less than or equal to x.
    static int countSub(int arr[],
                        int n, int x)
    {

        // Starting index of
        // sliding window.
        int st = 0;

        // Ending index of
        // sliding window.
        int end = 0;

        // Sum of elements currently
        // present in sliding window.
        int sum = 0;

        // To store required
        // number of subarrays.
        int cnt = 0;

        // Increment ending index
        // of sliding window one
        // step at a time.
        while (end < n)
        {

            // Update sum of sliding
            // window on adding a
            // new element.
            sum += arr[end];

            // Increment starting index
            // of sliding window until
            // sum is greater than x.
            while (st <= end && sum > x)
            {
                sum -= arr[st];
                st++;
            }

            // Update count of
            // number of subarrays.
            cnt += (end - st + 1);
            end++;
        }

        return cnt;
    }

    // Function to find number
    // of subarrays having sum
    // in the range L to R.
    static int findSubSumLtoR(int arr[], int n,
                              int L, int R)
    {

        // Number of subarrays
        // having sum less than
        // or equal to R.
        int Rcnt = countSub(arr, n, R);

        // Number of subarrays
        // having sum less than
        // or equal to L-1.
        int Lcnt = countSub(arr, n, L - 1);

        return Rcnt - Lcnt;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 1, 4, 6 };
        int n = arr.length;

        int L = 3;
        int R = 8;

        System.out.println(findSubSumLtoR(arr, n, L, R));
    }
}

// This code is contributed
// by Mahadev99
```

## C#

```
// C# program to find number
// of subarrays having sum in
// the range L to R.
using System;

class GFG
{

    // Function to find number
    // of subarrays having sum
    // less than or equal to x.
    static int countSub(int[] arr,
                        int n, int x)
    {

        // Starting index of
        // sliding window.
        int st = 0;

        // Ending index of
        // sliding window.
        int end = 0;

        // Sum of elements currently
        // present in sliding window.
        int sum = 0;

        // To store required
        // number of subarrays.
        int cnt = 0;

        // Increment ending index
        // of sliding window one
        // step at a time.
        while (end < n)
        {

            // Update sum of sliding
            // window on adding a
            // new element.
            sum += arr[end];

            // Increment starting index
            // of sliding window until
            // sum is greater than x.
            while (st <= end && sum > x)
            {
                sum -= arr[st];
                st++;
            }

            // Update count of
            // number of subarrays.
            cnt += (end - st + 1);
            end++;
        }

        return cnt;
    }

    // Function to find number
    // of subarrays having sum
    // in the range L to R.
    static int findSubSumLtoR(int[] arr, int n,
                              int L, int R)
    {

        // Number of subarrays
        // having sum less than
        // or equal to R.
        int Rcnt = countSub(arr, n, R);

        // Number of subarrays
        // having sum less than
        // or equal to L-1.
        int Lcnt = countSub(arr, n, L - 1);

        return Rcnt - Lcnt;
    }

    // Driver code
    public static void Main ()
    {
        int[] arr = { 1, 4, 6 };
        int n = arr.Length;

        int L = 3;
        int R = 8;

        Console.Write(findSubSumLtoR(arr, n, L, R));
    }
}

// This code is contributed
// by ChitraNayal
```

## 蟒蛇 3

```
# Python 3 program to find
# number of subarrays having
# sum in the range L to R.

# Function to find number
# of subarrays having sum
# less than or equal to x.
def countSub(arr, n, x):

    # Starting index of
    # sliding window.
    st = 0

    # Ending index of
    # sliding window.
    end = 0

    # Sum of elements currently
    # present in sliding window.
    sum = 0

    # To store required
    # number of subarrays.
    cnt = 0

    # Increment ending index
    # of sliding window one
    # step at a time.
    while end < n :

        # Update sum of sliding
        # window on adding a
        # new element.
        sum += arr[end]

        # Increment starting index
        # of sliding window until
        # sum is greater than x.
        while (st <= end and sum > x) :
            sum -= arr[st]
            st += 1

        # Update count of
        # number of subarrays.
        cnt += (end - st + 1)
        end += 1

    return cnt

# Function to find number
# of subarrays having sum
# in the range L to R.
def findSubSumLtoR(arr, n, L, R):

    # Number of subarrays
    # having sum less
    # than or equal to R.
    Rcnt = countSub(arr, n, R)

    # Number of subarrays
    # having sum less than
    # or equal to L-1.
    Lcnt = countSub(arr, n, L - 1)

    return Rcnt - Lcnt

# Driver code
arr = [ 1, 4, 6 ]
n = len(arr)
L = 3
R = 8
print(findSubSumLtoR(arr, n, L, R))

# This code is contributed
# by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number
// of subarrays having sum
// in the range L to R.

// Function to find number
// of subarrays having sum
// less than or equal to x.
function countSub(&$arr, $n, $x)
{
    // Starting index of
    // sliding window.
    $st = 0;

    // Ending index of
    // sliding window.
    $end = 0;

    // Sum of elements currently
    // present in sliding window.
    $sum = 0;

    // To store required
    // number of subarrays.
    $cnt = 0;

    // Increment ending index
    // of sliding window one
    // step at a time.
    while ($end < $n)
    {
        // Update sum of sliding window
        // on adding a new element.
        $sum += $arr[$end];

        // Increment starting index
        // of sliding window until
        // sum is greater than x.
        while ($st <= $end && $sum > $x)
        {
            $sum -= $arr[$st];
            $st++;
        }

        // Update count of
        // number of subarrays.
        $cnt += ($end - $st + 1);
        $end++;
    }

    return $cnt;
}

// Function to find number
// of subarrays having sum
// in the range L to R.
function findSubSumLtoR(&$arr, $n, $L, $R)
{
    // Number of subarrays
    // having sum less
    // than or equal to R.
    $Rcnt = countSub($arr, $n, $R);

    // Number of subarrays
    // having sum less
    // than or equal to L-1.
    $Lcnt = countSub($arr, $n, $L - 1);

    return $Rcnt - $Lcnt;
}

// Driver code.
$arr = array( 1, 4, 6 );
$n = sizeof($arr);
$L = 3;
$R = 8;
echo findSubSumLtoR($arr, $n, $L, $R);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript program to find number of subarrays having
// sum in the range L to R.

// Function to find number of subarrays having
// sum less than or equal to x.
function countSub(arr, n, x)
{

    // Starting index of sliding window.
    var st = 0;

    // Ending index of sliding window.
    var end = 0;

    // Sum of elements currently present
    // in sliding window.
    var sum = 0;

    // To store required number of subarrays.
    var cnt = 0;

    // Increment ending index of sliding
    // window one step at a time.
    while (end < n) {

        // Update sum of sliding window on
        // adding a new element.
        sum += arr[end];

        // Increment starting index of sliding
        // window until sum is greater than x.
        while (st <= end && sum > x) {
            sum -= arr[st];
            st++;
        }

        // Update count of number of subarrays.
        cnt += (end - st + 1);
        end++;
    }

    return cnt;
}

// Function to find number of subarrays having
// sum in the range L to R.
function findSubSumLtoR(arr, n, L, R)
{

    // Number of subarrays having sum less
    // than or equal to R.
    var Rcnt = countSub(arr, n, R);

    // Number of subarrays having sum less
    // than or equal to L-1.
    var Lcnt = countSub(arr, n, L - 1);

    return Rcnt - Lcnt;
}

// Driver code.
var arr = [ 1, 4, 6 ];
var n = arr.length;
var L = 3;
var R = 8;
document.write( findSubSumLtoR(arr, n, L, R));

</script>
```

**输出:**

```
 3
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)