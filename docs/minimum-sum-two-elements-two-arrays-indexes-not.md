# 两个数组中两个元素的最小和，使得索引不相同

> 原文:[https://www . geesforgeks . org/minimum-sum-two-elements-two-array-indexes-not/](https://www.geeksforgeeks.org/minimum-sum-two-elements-two-arrays-indexes-not/)

给定两个大小相同的数组 a[]和 b[]。任务是找到两个元素的最小和，使它们属于不同的数组，并且不在数组的同一索引处。

**示例:**

```
Input : a[] = {5, 4, 13, 2, 1}
        b[] = {2, 3, 4, 6, 5}
Output : 3
We take 1 from a[] and 2 from b[]
Sum is 1 + 2 = 3.

Input : a[] = {5, 4, 13, 1}
        b[] = {3, 2, 6, 1}
Output : 3
We take 1 from a[] and 2 from b[].
Note that we can't take 1 from b[]
as the elements can not be at same
index. 
```

A **简单的解决方案**是考虑 a[]的每个元素，在不同于其索引的索引处与 b[]的所有元素形成对，并计算和。最后返回最小和。该解决方案的时间复杂度为 0(n<sup>2</sup>

一个**高效的解决方案**在 O(n)时间内起作用。以下是步骤。

1.  从 a[]和 b[]中查找最小元素。让这些元素分别是 minA 和 minB。
2.  如果 minA 和 minB 的索引不一样，返回 minA + minB。
3.  否则从两个数组中找出第二个最小元素。让这些元素是 minA2 和 minB2。返回最小值(minA + minB2，minA2 + minB)

以下是上述想法的实现:

## C++

```
// C++ program to find minimum sum of two
// elements chosen from two arrays such that
// they are not at same index.
#include <bits/stdc++.h>
using namespace std;

// Function which returns minimum sum of two
// array elements such that their indexes are
// not same
int minSum(int a[], int b[], int n)
{
    // Finding minimum element in array A and
    // also/ storing its index value.
    int minA = a[0], indexA;
    for (int i=1; i<n; i++)
    {
        if (a[i] < minA)
        {
            minA = a[i];
            indexA = i;
        }
    }

    // Finding minimum element in array B and
    // also storing its index value
    int minB = b[0], indexB;
    for (int i=1; i<n; i++)
    {
        if (b[i] < minB)
        {
            minB = b[i];
            indexB = i;
        }
    }

    // If indexes of minimum elements are
    // not same, return their sum.
    if (indexA != indexB)
        return (minA + minB);

    // When index of A is not same as previous
    // and value is also less than other minimum
    // Store new minimum and store its index
    int minA2 = INT_MAX, indexA2;
    for (int i=0; i<n; i++)
    {
        if (i != indexA && a[i] < minA2)
        {
            minA2 = a[i];
            indexA2 = i;
        }
    }

    // When index of B is not same as previous
    // and value is also less than other minimum.
    // Store new minimum and store its index
    int minB2 = INT_MAX, indexB2;
    for (int i=0; i<n; i++)
    {
        if (i != indexB && b[i] < minB2)
        {
            minB2 = b[i];
            indexB2 = i;
        }
    }

    // Taking sum of previous minimum of a[]
    // with new minimum of b[]
    // and also sum of previous minimum of b[]
    //  with new minimum of a[]
    // and return whichever is minimum.
    return min(minB + minA2, minA + minB2);
}

// Driver code
int main()
{
    int a[] = {5, 4, 3, 8, 1};
    int b[] = {2, 3, 4, 2, 1};
    int n = sizeof(a)/sizeof(a[0]);
    cout << minSum(a, b, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum sum of two
// elements chosen from two arrays such that
// they are not at same index.

class Minimum{

    // Function which returns minimum sum of two
    // array elements such that their indexes are
    // not same
    public static int minSum(int a[], int b[], int n)
        {
           // Finding minimum element in array A and
           // also/ storing its index value.
           int minA = a[0], indexA = 0;
           for (int i=1; i<n; i++)
           {
               if (a[i] < minA)
               {
                   minA = a[i];
                   indexA = i;
               }
           }

           // Finding minimum element in array B and
           // also storing its index value
           int minB = b[0], indexB = 0;
           for (int i=1; i<n; i++)
           {
              if (b[i] < minB)
              {
                  minB = b[i];
                  indexB = i;
              }
           }

            // If indexes of minimum elements are
            // not same, return their sum.
            if (indexA != indexB)
            return (minA + minB);

            // When index of A is not same as previous
            // and value is also less than other minimum
            // Store new minimum and store its index
            int minA2 = Integer.MAX_VALUE, indexA2 = 0;
            for (int i=0; i<n; i++)
            {
               if (i != indexA && a[i] < minA2)
               {
                   minA2 = a[i];
                   indexA2 = i;
               }
            }

            // When index of B is not same as previous
            // and value is also less than other minimum.
            // Store new minimum and store its index
            int minB2 = Integer.MAX_VALUE, indexB2 = 0;
            for (int i=0; i<n; i++)
            {
                if (i != indexB && b[i] < minB2)
                {
                   minB2 = b[i];
                   indexB2 = i;
                }
            }

            // Taking sum of previous minimum of a[]
            // with new minimum of b[]
            // and also sum of previous minimum of b[]
            // with new minimum of a[]
            // and return whichever is minimum.
            return Math.min(minB + minA2, minA + minB2);
        }

    public static void main(String[] args)
    {
        int a[] = {5, 4, 3, 8, 1};
        int b[] = {2, 3, 4, 2, 1};
        int n = 5;
        System.out.print(minSum(a, b, n));
    }
}

// This code is contributed by rishabh_jain
```

## 蟒蛇 3

```
# Python3 code to find minimum sum of
# two elements chosen from two arrays
# such that they are not at same index.
import sys

# Function which returns minimum sum
# of two array elements such that their
# indexes arenot same
def minSum(a, b, n):

    # Finding minimum element in array A
    # and also storing its index value.
    minA = a[0]
    indexA = 0
    for i in range(1,n):
        if a[i] < minA:
            minA = a[i]
            indexA = i

    # Finding minimum element in array B
    # and also storing its index value
    minB = b[0]
    indexB = 0
    for i in range(1, n):
        if b[i] < minB:
            minB = b[i]
            indexB = i

    # If indexes of minimum elements
    # are not same, return their sum.
    if indexA != indexB:
        return (minA + minB)

    # When index of A is not same as
    # previous and value is also less
    # than other minimum. Store new
    # minimum and store its index
    minA2 = sys.maxsize
    indexA2=0
    for i in range(n):
        if i != indexA and a[i] < minA2:
            minA2 = a[i]
            indexA2 = i

    # When index of B is not same as
    # previous and value is also less
    # than other minimum. Store new
    # minimum and store its index
    minB2 = sys.maxsize
    indexB2 = 0
    for i in range(n):
        if i != indexB and b[i] < minB2:
            minB2 = b[i]
            indexB2 = i

    # Taking sum of previous minimum of
    # a[] with new minimum of b[]
    # and also sum of previous minimum
    # of b[] with new minimum of a[]
    # and return whichever is minimum.
    return min(minB + minA2, minA + minB2)

# Driver code
a = [5, 4, 3, 8, 1]
b = [2, 3, 4, 2, 1]
n = len(a)
print(minSum(a, b, n))

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to find minimum sum of
// two elements chosen from two arrays
// such that they are not at same index.
using System;

public class GFG {

    // Function which returns minimum
    // sum of two array elements such
    // that their indexes are not same
    static int minSum(int []a, int []b,
                                  int n)
    {

        // Finding minimum element in
        // array A and also/ storing its
        // index value.
        int minA = a[0], indexA = 0;

        for (int i = 1; i < n; i++)
        {
            if (a[i] < minA)
            {
                minA = a[i];
                indexA = i;
            }
        }

        // Finding minimum element in
        // array B and also storing its
        // index value
        int minB = b[0], indexB = 0;

        for (int i = 1; i < n; i++)
        {
            if (b[i] < minB)
            {
                minB = b[i];
                indexB = i;
            }
        }

        // If indexes of minimum elements
        // are not same, return their sum.
        if (indexA != indexB)
            return (minA + minB);

        // When index of A is not same as
        // previous and value is also less
        // than other minimum Store new
        // minimum and store its index
        int minA2 = int.MaxValue;

        for (int i=0; i<n; i++)
        {
            if (i != indexA && a[i] < minA2)
            {
                minA2 = a[i];
            }
        }

        // When index of B is not same as
        // previous and value is also less
        // than other minimum. Store new
        // minimum and store its index
        int minB2 = int.MaxValue;

        for (int i=0; i<n; i++)
            if (i != indexB && b[i] < minB2)
                minB2 = b[i];

        // Taking sum of previous minimum
        // of a[] with new minimum of b[]
        // and also sum of previous minimum
        // of b[] with new minimum of a[]
        // and return whichever is minimum.
        return Math.Min(minB + minA2,
                            minA + minB2);
    }

    public static void Main()
    {
        int []a = {5, 4, 3, 8, 1};
        int []b = {2, 3, 4, 2, 1};
        int n = 5;

        Console.Write(minSum(a, b, n));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum
// sum of two elements chosen
// from two arrays such that
// they are not at same index.

// Function which returns
// minimum sum of two array
// elements such that their
// indexes are not same
function minSum($a, $b, $n)
{
    // Finding minimum element
    // in array A and also
    // storing its index value.
    $minA = $a[0];

    for ($i = 1; $i < $n; $i++)
    {
        if ($a[$i] < $minA)
        {
            $minA = $a[$i];
            $indexA = $i;
        }
    }

    // Finding minimum element
    // in array B and also
    // storing its index value
    $minB = $b[0];

    for ($i = 1; $i < $n; $i++)
    {
        if ($b[$i] < $minB)
        {
            $minB = $b[$i];
            $indexB = $i;
        }
    }

    // If indexes of minimum
    // elements are not same,
    // return their sum.
    if ($indexA != $indexB)
        return ($minA + $minB);

    // When index of A is not
    // same as previous and
    // value is also less than
    // other minimum. Store new
    // minimum and store its index
    $minA2 = 9999999;
    $indexA2 = 0;
    for ($i = 0; $i < $n; $i++)
    {
        if ($i != $indexA &&
            $a[$i] < $minA2)
        {
            $minA2 = $a[$i];
            $indexA2 = $i;
        }
    }

    // When index of B is not
    // same as previous and
    // value is also less than
    // other minimum. Store new
    // minimum and store its index
    $minB2 = 999999;
    $indexB2 = 0;
    for ($i = 0; $i < $n; $i++)
    {
        if ($i != $indexB &&
            $b[$i] < $minB2)
        {
            $minB2 = $b[$i];
            $indexB2 = $i;
        }
    }

    // Taking sum of previous
    // minimum of a[] with
    // new minimum of b[]
    // and also sum of previous
    // minimum of b[] with new
    // minimum of a[]
    // and return whichever
    // is minimum.
    return min($minB + $minA2,
               $minA + $minB2);
}

// Driver code
$a = array(5, 4, 3, 8, 1);
$b = array(2, 3, 4, 2, 1);
$n = count($a);
echo minSum($a, $b, $n);

// This code is contributed
// by Sam007
?>
```

## java 描述语言

```
<script>
// JavaScript program to find minimum sum of two
// elements chosen from two arrays such that
// they are not at same index.

// Function which returns minimum sum of two
// array elements such that their indexes are
// not same
function minSum(a, b, n)
{
    // Finding minimum element in array A and
    // also/ storing its index value.
    let minA = a[0], indexA;
    for (let i=1; i<n; i++)
    {
        if (a[i] < minA)
        {
            minA = a[i];
            indexA = i;
        }
    }

    // Finding minimum element in array B and
    // also storing its index value
    let minB = b[0], indexB;
    for (let i=1; i<n; i++)
    {
        if (b[i] < minB)
        {
            minB = b[i];
            indexB = i;
        }
    }

    // If indexes of minimum elements are
    // not same, return their sum.
    if (indexA != indexB)
        return (minA + minB);

    // When index of A is not same as previous
    // and value is also less than other minimum
    // Store new minimum and store its index
    let minA2 = Number.MAX_SAFE_INTEGER, indexA2;
    for (let i=0; i<n; i++)
    {
        if (i != indexA && a[i] < minA2)
        {
            minA2 = a[i];
            indexA2 = i;
        }
    }

    // When index of B is not same as previous
    // and value is also less than other minimum.
    // Store new minimum and store its index
    let minB2 = Number.MAX_SAFE_INTEGER, indexB2;
    for (let i=0; i<n; i++)
    {
        if (i != indexB && b[i] < minB2)
        {
            minB2 = b[i];
            indexB2 = i;
        }
    }

    // Taking sum of previous minimum of a[]
    // with new minimum of b[]
    // and also sum of previous minimum of b[]
    // with new minimum of a[]
    // and return whichever is minimum.
    return Math.min(minB + minA2, minA + minB2);
}

// Driver code
    let a = [5, 4, 3, 8, 1];
    let b = [2, 3, 4, 2, 1];
    let n = a.length;
    document.write(minSum(a, b, n));

// This code is contributed by Surbhi Tyagi.
</script>
```

**输出:**

```
3
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)

本文由 [**萨赫勒拉吉普特**](https://www.linkedin.com/in/sahil-rajput-3ba2b3134/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。