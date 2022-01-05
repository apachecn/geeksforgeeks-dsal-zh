# 无界二分搜索法示例(找到单调递增函数首次变为正的点)

> 原文:[https://www . geesforgeks . org/find-函数变负的点/](https://www.geeksforgeeks.org/find-the-point-where-a-function-becomes-negative/)

给定一个函数 int f(无符号 int x)’，该函数将一个**非负整数**‘x’作为输入，并返回一个**整数**作为输出。该函数相对于 x 的值单调递增，即对于每个输入 x，f(x+1)的值大于 f(x)。找到值“n”，其中 f()首次变为正。因为 f()是单调递增的，所以 f(n+1)、f(n+2)、…的值必须为正，而 f(n-2)、f(n-3)、…的值必须为负。
在 O(logn)时间内求 n，你可以假设 f(x)可以在 O(1)时间内对任何输入 x 进行求值。

一个**简单的解法**就是从 I 等于 0 开始，逐个计算 f(i)对于 1，2，3，4 …等的值，直到我们找到一个正的 f(i)。这是可行的，但需要时间。
**我们可以应用二分搜索法在 O(Logn)时间中寻找 n 吗？**我们不能直接套用二分搜索法，因为我们没有上限，也没有高指数。这个想法是重复加倍，直到我们找到一个正值，即检查 f()的值，直到 f(i)变为正值。

```
  f(0) 
  f(1)
  f(2)
  f(4)
  f(8)
  f(16)
  f(32)
  ....
  ....
  f(high)
Let 'high' be the value of i when f() becomes positive for first time.
```

在找到“高”之后，我们可以应用二分搜索法来找到 n 吗？我们现在可以应用二分搜索法，我们可以用“高/2”作为低，用“高”作为二分搜索法的高指数。结果 n 必须介于“高/2”和“高”之间。
寻找‘高’的步数为 O(Logn)。所以我们可以在 O(Logn)时间里找到‘high’。二分搜索法在高/2 和高之间花了多少时间？“高”的值必须小于 2*n。高/2 和高之间的元素数量必须为 0(n)。因此，二分搜索法的时间复杂度为 O(Logn)，总时间复杂度为 2*O(Logn)，也就是 O(Logn)。

## C++

```
// C++ code for binary search
#include<bits/stdc++.h>
using namespace std;

int binarySearch(int low, int high); // prototype

// Let's take an example function
// as f(x) = x^2 - 10*x - 20 Note that
// f(x) can be any monotonocally increasing function
int f(int x) { return (x*x - 10*x - 20); }

// Returns the value x where above
// function f() becomes positive
// first time.
int findFirstPositive()
{
    // When first value itself is positive
    if (f(0) > 0)
        return 0;

    // Find 'high' for binary search by repeated doubling
    int i = 1;
    while (f(i) <= 0)
        i = i*2;

    // Call binary search
    return binarySearch(i/2, i);
}

// Searches first positive value
// of f(i) where low <= i <= high
int binarySearch(int low, int high)
{
    if (high >= low)
    {
        int mid = low + (high - low)/2; /* mid = (low + high)/2 */

        // If f(mid) is greater than 0 and
        // one of the following two
        // conditions is true:
        // a) mid is equal to low
        // b) f(mid-1) is negative
        if (f(mid) > 0 && (mid == low || f(mid-1) <= 0))
            return mid;

        // If f(mid) is smaller than or equal to 0
        if (f(mid) <= 0)
            return binarySearch((mid + 1), high);
        else // f(mid) > 0
            return binarySearch(low, (mid -1));
    }

    /* Return -1 if there is no
    positive value in given range */
    return -1;
}

/* Driver code */
int main()
{
    cout<<"The value n where f() becomes" <<
        "positive first is "<< findFirstPositive();
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
#include <stdio.h>
int binarySearch(int low, int high); // prototype

// Let's take an example function as f(x) = x^2 - 10*x - 20
// Note that f(x) can be any monotonocally increasing function
int f(int x) { return (x*x - 10*x - 20); }

// Returns the value x where above function f() becomes positive
// first time.
int findFirstPositive()
{
    // When first value itself is positive
    if (f(0) > 0)
        return 0;

    // Find 'high' for binary search by repeated doubling
    int i = 1;
    while (f(i) <= 0)
        i = i*2;

    //  Call binary search
    return binarySearch(i/2, i);
}

// Searches first positive value of f(i) where low <= i <= high
int binarySearch(int low, int high)
{
    if (high >= low)
    {
        int mid = low + (high - low)/2; /* mid = (low + high)/2 */

        // If f(mid) is greater than 0 and one of the following two
        // conditions is true:
        // a) mid is equal to low
        // b) f(mid-1) is negative
        if (f(mid) > 0 && (mid == low || f(mid-1) <= 0))
            return mid;

        // If f(mid) is smaller than or equal to 0
        if (f(mid) <= 0)
            return binarySearch((mid + 1), high);
        else // f(mid) > 0
            return binarySearch(low, (mid -1));
    }

    /* Return -1 if there is no positive value in given range */
    return -1;
}

/* Driver program to check above functions */
int main()
{
    printf("The value n where f() becomes positive first is %d",
           findFirstPositive());
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for Binary Search
import java.util.*;

class Binary
{
    public static int f(int x)
    { return (x*x - 10*x - 20); }

    // Returns the value x where above
    // function f() becomes positive
    // first time.
    public static int findFirstPositive()
    {
        // When first value itself is positive
        if (f(0) > 0)
            return 0;

        // Find 'high' for binary search
        // by repeated doubling
        int i = 1;
        while (f(i) <= 0)
            i = i * 2;

        // Call binary search
        return binarySearch(i / 2, i);
    }

    // Searches first positive value of
    // f(i) where low <= i <= high
    public static int binarySearch(int low, int high)
    {
        if (high >= low)
        {  
            /* mid = (low + high)/2 */
            int mid = low + (high - low)/2;

            // If f(mid) is greater than 0 and
            // one of the following two
            // conditions is true:
            // a) mid is equal to low
            // b) f(mid-1) is negative
            if (f(mid) > 0 && (mid == low || f(mid-1) <= 0))
                return mid;

            // If f(mid) is smaller than or equal to 0
            if (f(mid) <= 0)
                return binarySearch((mid + 1), high);
            else // f(mid) > 0
                return binarySearch(low, (mid -1));
        }

        /* Return -1 if there is no positive
        value in given range */
        return -1;
    }

    // driver code
    public static void main(String[] args)
    {
        System.out.print ("The value n where f() "+
                         "becomes positive first is "+
                         findFirstPositive());
    }
}

// This code is contributed by rishabh_jain
```

## 蟒蛇 3

```
# Python3 program for Unbound Binary search.

# Let's take an example function as
# f(x) = x^2 - 10*x - 20
# Note that f(x) can be any monotonocally
# increasing function
def f(x):
    return (x * x - 10 * x - 20)

# Returns the value x where above function
# f() becomes positive first time.
def findFirstPositive() :

    # When first value itself is positive
    if (f(0) > 0):
        return 0

    # Find 'high' for binary search
    # by repeated doubling
    i = 1
    while (f(i) <= 0) :
        i = i * 2

    # Call binary search
    return binarySearch(i/2, i)

# Searches first positive value of
# f(i) where low <= i <= high
def binarySearch(low, high):
    if (high >= low) :

        # mid = (low + high)/2
        mid = low + (high - low)/2; 

        # If f(mid) is greater than 0
        # and one of the following two
        # conditions is true:
        # a) mid is equal to low
        # b) f(mid-1) is negative
        if (f(mid) > 0 and (mid == low or f(mid-1) <= 0)) :
            return mid;

        # If f(mid) is smaller than or equal to 0
        if (f(mid) <= 0) :
            return binarySearch((mid + 1), high)
        else : # f(mid) > 0
            return binarySearch(low, (mid -1))

    # Return -1 if there is no positive
    # value in given range
    return -1;

# Driver Code
print ("The value n where f() becomes "+
      "positive first is ", findFirstPositive());

# This code is contributed by rishabh_jain
```

## C#

```
// C# program for Binary Search
using System;

class Binary
{
    public static int f(int x)
    {
        return (x*x - 10*x - 20);
    }

    // Returns the value x where above
    // function f() becomes positive
    // first time.
    public static int findFirstPositive()
    {
        // When first value itself is positive
        if (f(0) > 0)
            return 0;

        // Find 'high' for binary search
        // by repeated doubling
        int i = 1;
        while (f(i) <= 0)
            i = i * 2;

        // Call binary search
        return binarySearch(i / 2, i);
    }

    // Searches first positive value of
    // f(i) where low <= i <= high
    public static int binarySearch(int low, int high)
    {
        if (high >= low)
        {
            /* mid = (low + high)/2 */
            int mid = low + (high - low)/2;

            // If f(mid) is greater than 0 and
            // one of the following two
            // conditions is true:
            // a) mid is equal to low
            // b) f(mid-1) is negative
            if (f(mid) > 0 && (mid == low ||
                             f(mid-1) <= 0))
                return mid;

            // If f(mid) is smaller than or equal to 0
            if (f(mid) <= 0)
                return binarySearch((mid + 1), high);
            else

                // f(mid) > 0
                return binarySearch(low, (mid -1));
        }

        /* Return -1 if there is no positive
        value in given range */
        return -1;
    }

    // Driver code
    public static void Main()
    {
       Console.Write ("The value n where f() " +
                      "becomes positive first is " +
                       findFirstPositive());
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for Binary Search

// Let's take an example function
// as f(x) = x^2 - 10*x - 20
// Note that f(x) can be any
// monotonocally increasing function
function f($x)
{
    return ($x * $x - 10 * $x - 20);
}

// Returns the value x where above
// function f() becomes positive
// first time.
function findFirstPositive()
{
    // When first value
    // itself is positive
    if (f(0) > 0)
        return 0;

    // Find 'high' for binary
    // search by repeated doubling
    $i = 1;
    while (f($i) <= 0)
        $i = $i * 2;

    // Call binary search
    return binarySearch(intval($i / 2), $i);
}

// Searches first positive value
// of f(i) where low <= i <= high
function binarySearch($low, $high)
{
    if ($high >= $low)
    {
        /* mid = (low + high)/2 */
        $mid = $low + intval(($high -
                              $low) / 2);

        // If f(mid) is greater than 0
        // and one of the following two
        // conditions is true:
        // a) mid is equal to low
        // b) f(mid-1) is negative
        if (f($mid) > 0 && ($mid == $low ||
                          f($mid - 1) <= 0))
            return $mid;

        // If f(mid) is smaller
        // than or equal to 0
        if (f($mid) <= 0)
            return binarySearch(($mid + 1), $high);
        else // f(mid) > 0
            return binarySearch($low, ($mid - 1));
    }

    /* Return -1 if there is no
    positive value in given range */
    return -1;
}

// Driver Code
echo "The value n where f() becomes ".
                 "positive first is ".
                 findFirstPositive() ;

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
    // Javascript program for Binary Search

    function f(x)
    {
        return (x*x - 10*x - 20);
    }

    // Returns the value x where above
    // function f() becomes positive
    // first time.
    function findFirstPositive()
    {
        // When first value itself is positive
        if (f(0) > 0)
            return 0;

        // Find 'high' for binary search
        // by repeated doubling
        let i = 1;
        while (f(i) <= 0)
            i = i * 2;

        // Call binary search
        return binarySearch(parseInt(i / 2, 10), i);
    }

    // Searches first positive value of
    // f(i) where low <= i <= high
    function binarySearch(low, high)
    {
        if (high >= low)
        {
            /* mid = (low + high)/2 */
            let mid = low + parseInt((high - low)/2, 10);

            // If f(mid) is greater than 0 and
            // one of the following two
            // conditions is true:
            // a) mid is equal to low
            // b) f(mid-1) is negative
            if (f(mid) > 0 && (mid == low ||
                             f(mid-1) <= 0))
                return mid;

            // If f(mid) is smaller than or equal to 0
            if (f(mid) <= 0)
                return binarySearch((mid + 1), high);
            else

                // f(mid) > 0
                return binarySearch(low, (mid -1));
        }

        /* Return -1 if there is no positive
        value in given range */
        return -1;
    }

    document.write ("The value n where f() " +
                      "becomes positive first is " +
                       findFirstPositive());

</script>
```

**输出:**

```
The value n where f() becomes positive first is 12
```