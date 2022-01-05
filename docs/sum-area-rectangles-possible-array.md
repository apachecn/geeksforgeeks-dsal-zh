# 一个阵列可能的矩形面积之和

> 原文:[https://www . geesforgeks . org/sum-area-矩形-可能-array/](https://www.geeksforgeeks.org/sum-area-rectangles-possible-array/)

给定一个数组，任务是计算由数组元素构成的所有可能的最大面积矩形的和。此外，您最多可以将数组的元素减少 1。

**示例:**

```
Input: a = {10, 10, 10, 10, 11, 
            10, 11, 10}
Output: 210
Explanation: 
We can form two rectangles one square (10 * 10) 
and one (11 * 10). Hence, total area = 100 + 110 = 210.

Input: a = { 3, 4, 5, 6 }
Output: 15
Explanation: 
We can reduce 4 to 3 and 6 to 5 so that we got 
rectangle of (3 * 5). Hence area = 15.

Input: a = { 3, 2, 5, 2 }
Output: 0
```

**天真方法:**检查数组中所有可能的四个元素，然后选择能够形成矩形的元素。在这些矩形中，将这些元素形成的最大面积的所有矩形分开。得到矩形和它们的面积后，将它们相加得到我们想要的解。

**高效方法:**要得到面积最大的矩形，首先对非递增数组中的数组元素进行排序。排序后，开始选择数组元素的过程。这里，如果数组的两个元素相等 *(a[i] == a[i+1])* 或者如果较小元素 a[i+1]的长度比 a[i]小一(在这种情况下为*，我们的长度为 a[i+1]，因为 a[i]减少了 1* )，则可以选择数组的两个元素(如矩形的长度)。维护一个标志变量来检查*我们是否得到长度和宽度。*得到长度后，设置 flag 变量，现在用我们对长度做的同样方法计算宽度，并对矩形的面积求和。在获得长度和宽度后，再次将标志变量设置为 false，这样我们现在将搜索一个新的矩形。重复这个过程，最后，返回面积的最终总和。

## C++

```
// CPP code to find sum of all
// area rectangle possible
#include <bits/stdc++.h>
using namespace std;

// Function to find
// area of rectangles
int MaxTotalRectangleArea(int a[],
                          int n)
{
    // sorting the array in
    // descending order
    sort(a, a + n, greater<int>());

    // store the final sum of
    // all the rectangles area
    // possible
    int sum = 0;
    bool flag = false;

    // temporary variable to store
    // the length of rectangle
    int len;

    for (int i = 0; i < n; i++)
    {

        // Selecting the length of
        // rectangle so that difference
        // between any two number is 1
        // only. Here length is selected
        // so flag is set
        if ((a[i] == a[i + 1] || a[i] -
            a[i + 1] == 1) && (!flag))
        {
            // flag is set means
            // we have got length of
            // rectangle
            flag = true;

            // length is set to
            // a[i+1] so that if
            // a[i] a[i+1] is less
            // than by 1 then also
            // we have the correct
            // choice for length
            len = a[i + 1];

            // incrementing the counter
            // one time more as we have
            // considered a[i+1] element
            // also so.
            i++;
        }

        // Selecting the width of rectangle
        // so that difference between any
        // two number is 1 only. Here width
        // is selected so now flag is again
        // unset for next rectangle
        else if ((a[i] == a[i + 1] ||
                a[i] - a[i + 1] == 1) && (flag))
            {
                // area is calculated for
                // rectangle
                sum = sum + a[i + 1] * len;

                // flag is set false
                // for another rectangle
                // which we can get from
                // elements in array
                flag = false;

                // incrementing the counter
                // one time more as we have
                // considered a[i+1] element
                // also so.
                i++;
            }
    }

    return sum;
}

// Driver code
int main()
{
    int a[] = { 10, 10, 10, 10,
                11, 10, 11, 10,
                9, 9, 8, 8 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << MaxTotalRectangleArea(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find sum of
// all area rectangle possible
import java.io.*;
import java.util.Arrays;
import java.util.*;

class GFG
{
    // Function to find
    // area of rectangles
    static int MaxTotalRectangleArea(Integer []a,
                                     int n)
    {

        // sorting the array in
        // descending order
        Arrays.sort(a, Collections.reverseOrder());

        // store the final sum of
        // all the rectangles area
        // possible
        int sum = 0;
        boolean flag = false;

        // temporary variable to
        // store the length of rectangle
        int len = 0;

        for (int i = 0; i < n; i++)
        {

            // Selecting the length of
            // rectangle so that difference
            // between any two number is 1
            // only. Here length is selected
            // so flag is set
            if ((a[i] == a[i + 1] ||
                 a[i] - a[i+1] == 1) &&
                               !flag)
            {
                // flag is set means
                // we have got length of
                // rectangle
                flag = true;

                // length is set to
                // a[i+1] so that if
                // a[i] a[i+1] is less
                // than by 1 then also
                // we have the correct
                // choice for length
                len = a[i+1];

                // incrementing the counter
                // one time more as we have
                // considered a[i+1] element
                // also so.
                i++;
            }

            // Selecting the width of rectangle
            // so that difference between any
            // two number is 1 only. Here width
            // is selected so now flag is again
            // unset for next rectangle
            else if ((a[i] == a[i + 1] ||
                      a[i] - a[i+1] == 1) &&
                                    (flag))
                {
                    // area is calculated for
                    // rectangle
                    sum = sum + a[i+1] * len;

                    // flag is set false
                    // for another rectangle
                    // which we can get from
                    // elements in array
                    flag = false;

                    // incrementing the counter
                    // one time more as we have
                    // considered a[i+1] element
                    // also so.
                    i++;
                }
        }

        return sum;
    }

    // Driver code
    public static void main (String args[])
    {
    Integer []a = { 10, 10, 10, 10,
                11, 10, 11, 10,
                9, 9, 8, 8 };
    int n = a.length;

    System.out.print(MaxTotalRectangleArea(a, n));
    }
}
// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 蟒蛇 3

```
# Python3 code to find sum
# of all area rectangle
# possible

# Function to find
# area of rectangles
def MaxTotalRectangleArea(a, n) :

    # sorting the array in
    # descending order
    a.sort(reverse = True)

    # store the final sum of
    # all the rectangles area
    # possible
    sum = 0
    flag = False

    # temporary variable to store
    # the length of rectangle
    len = 0
    i = 0

    while (i < n-1) :
        if(i != 0) :
            i = i + 1

        # Selecting the length of
        # rectangle so that difference
        # between any two number is 1
        # only. Here length is selected
        # so flag is set
        if ((a[i] == a[i + 1] or
             a[i] - a[i + 1] == 1)
              and flag == False) :

            # flag is set means
            # we have got length of
            # rectangle
            flag = True

            # length is set to
            # a[i+1] so that if
            # a[i+1] is less than a[i]
            # by 1 then also we have
            # the correct chice for length
            len = a[i + 1]

            # incrementing the counter
            # one time more as we have
            # considered a[i+1] element
            # also so.
            i = i + 1

        # Selecting the width of rectangle
        # so that difference between any
        # two number is 1 only. Here width
        # is selected so now flag is again
        # unset for next rectangle
        elif ((a[i] == a[i + 1] or
              a[i] - a[i + 1] == 1)
                and flag == True) :

            # area is calculated for
            # rectangle
            sum = sum + a[i + 1] * len

            # flag is set false
            # for another rectangle
            # which we can get from
            # elements in array
            flag = False

            # incrementing the counter
            # one time more as we have
            # considered a[i+1] element
            # also so.
            i = i + 1

    return sum

# Driver code
a = [ 10, 10, 10, 10, 11, 10,
          11, 10, 9, 9, 8, 8 ]
n = len(a)

print (MaxTotalRectangleArea(a, n))

# This code is contributed by
# Manish Shaw (manishshaw1)
```

## C#

```
// C# code to find sum of all area rectangle
// possible
using System;

class GFG {

    // Function to find
    // area of rectangles
    static int MaxTotalRectangleArea(int []a,
                                       int n)
    {

        // sorting the array in descending
        // order
        Array.Sort(a);
        Array.Reverse(a);

        // store the final sum of all the
        // rectangles area possible
        int sum = 0;
        bool flag = false;

        // temporary variable to store the
        // length of rectangle
        int len =0;

        for (int i = 0; i < n; i++)
        {

            // Selecting the length of
            // rectangle so that difference
            // between any two number is 1
            // only. Here length is selected
            // so flag is set
            if ((a[i] == a[i + 1] || a[i] -
                a[i + 1] == 1) && (!flag))
            {
                // flag is set means
                // we have got length of
                // rectangle
                flag = true;

                // length is set to
                // a[i+1] so that if
                // a[i] a[i+1] is less
                // than by 1 then also
                // we have the correct
                // choice for length
                len = a[i + 1];

                // incrementing the counter
                // one time more as we have
                // considered a[i+1] element
                // also so.
                i++;
            }

            // Selecting the width of rectangle
            // so that difference between any
            // two number is 1 only. Here width
            // is selected so now flag is again
            // unset for next rectangle
            else if ((a[i] == a[i + 1] ||
                    a[i] - a[i + 1] == 1) && (flag))
                {
                    // area is calculated for
                    // rectangle
                    sum = sum + a[i + 1] * len;

                    // flag is set false
                    // for another rectangle
                    // which we can get from
                    // elements in array
                    flag = false;

                    // incrementing the counter
                    // one time more as we have
                    // considered a[i+1] element
                    // also so.
                    i++;
                }
        }

        return sum;
    }

    // Driver code
    static public void Main ()
    {
            int []a = { 10, 10, 10, 10,
                        11, 10, 11, 10,
                        9, 9, 8, 8 };
    int n = a.Length;

    Console.WriteLine(
                MaxTotalRectangleArea(a, n));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find sum
// of all area rectangle
// possible

// Function to find
// area of rectangles
function MaxTotalRectangleArea( $a, $n)
{
    // sorting the array in
    // descending order
    rsort($a);

    // store the final sum of
    // all the rectangles area
    // possible
    $sum = 0;
    $flag = false;

    // temporary variable to store
    // the length of rectangle
    $len;

    for ( $i = 0; $i < $n; $i++)
    {

        // Selecting the length of
        // rectangle so that difference
        // between any two number is 1
        // only. Here length is selected
        // so flag is set
        if (($a[$i] == $a[$i + 1] or $a[$i] -
             $a[$i + 1] == 1) and (!$flag))
        {
            // flag is set means
            // we have got length of
            // rectangle
            $flag = true;

            // length is set to
            // a[i+1] so that if
            // a[i+1] is less than a[i]
            // by 1 then also we have
            // the correct chice for length
            $len = $a[$i + 1];

            // incrementing the counter
            // one time more as we have
            // considered a[i+1] element
            // also so.
            $i++;
        }

        // Selecting the width of rectangle
        // so that difference between any
        // two number is 1 only. Here width
        // is selected so now flag is again
        // unset for next rectangle
        else if (($a[$i] == $a[$i + 1] or
                  $a[$i] - $a[$i + 1] == 1) and
                 ($flag))
            {
                // area is calculated for
                // rectangle
                $sum = $sum + $a[$i + 1] * $len;

                // flag is set false
                // for another rectangle
                // which we can get from
                // elements in array
                $flag = false;

                // incrementing the counter
                // one time more as we have
                // considered a[i+1] element
                // also so.
                $i++;
            }
    }

    return $sum;
}

// Driver code
$a = array( 10, 10, 10, 10,
            11, 10, 11, 10,
            9, 9, 8, 8 );
$n = count($a);

echo MaxTotalRectangleArea($a, $n);

//This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript code to find sum of all
// area rectangle possible

// Function to find
// area of rectangles
function MaxTotalRectangleArea( a, n)
{
    // sorting the array in
    // descending order
    a.sort();
    a.reverse();

    // store the final sum of
    // all the rectangles area
    // possible
    let sum = 0;
    let flag = false;

    // temporary variable to store
    // the length of rectangle
    let len;

    for (let i = 0; i < n; i++)
    {

        // Selecting the length of
        // rectangle so that difference
        // between any two number is 1
        // only. Here length is selected
        // so flag is set
        if ((a[i] == a[i + 1] || a[i] -
            a[i + 1] == 1) && (!flag))
        {
            // flag is set means
            // we have got length of
            // rectangle
            flag = true;

            // length is set to
            // a[i+1] so that if
            // a[i] a[i+1] is less
            // than by 1 then also
            // we have the correct
            // choice for length
            len = a[i + 1];

            // incrementing the counter
            // one time more as we have
            // considered a[i+1] element
            // also so.
            i++;
        }

        // Selecting the width of rectangle
        // so that difference between any
        // two number is 1 only. Here width
        // is selected so now flag is again
        // unset for next rectangle
        else if ((a[i] == a[i + 1] ||
                a[i] - a[i + 1] == 1) && (flag))
            {
                // area is calculated for
                // rectangle
                sum = sum + a[i + 1] * len;

                // flag is set false
                // for another rectangle
                // which we can get from
                // elements in array
                flag = false;

                // incrementing the counter
                // one time more as we have
                // considered a[i+1] element
                // also so.
                i++;
            }
    }

    return sum;
}

// Driver Code

let a = [ 10, 10, 10, 10,
        11, 10, 11, 10,
        9, 9, 8, 8 ];
let n = a.length;

document.write(MaxTotalRectangleArea(a, n));

</script>
```

**Output**

```
282
```

***时间复杂度:** O(nlog(n))*
***辅助空间:** O(1)*