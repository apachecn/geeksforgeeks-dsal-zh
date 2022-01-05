# 检查是否可以按照宽度的非升序重新排列矩形

> 原文:[https://www . geeksforgeeks . org/check-如果有可能重新排列非宽度升序排列的矩形/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-rearrange-rectangles-in-a-non-ascending-order-of-breadths/)

给定 **n** 个矩形，其长度为 **L** ，宽度为 **B** 。我们可以将任何矩形旋转 90 度。换句话说，转动它们之后，宽度会变成长度，长度会变成宽度。
任务是检查是否有办法让矩形按照非上升宽度的顺序走。也就是说，每个矩形的宽度不得大于前一个矩形的宽度。
**注意:**不能改变矩形的顺序。
**举例:**

> **输入:** 3
> l = 3，b = 4
> l1 = 4，b1 = 6
> l2 = 3，b2 = 5
> **输出:** YES
> 给定的宽度为[ 4，6，5 ]我们可以旋转第二个和第三个矩形，使宽度满足上述条件[ 4，4，3 ] ( 3 不大于 4，4 不大于 4)，这就是为什么我们打印 YES。
> **输入:**3
> 1 60
> 70 55
> 56 80
> **输出:**否
> 宽度为【60，55，80】55 55 或 56 > 55。所以不可能以非升序排列宽度，这就是为什么我们要打印 NO

**方法:**下面是解决这个问题的分步算法:

1.  用矩形的长度和宽度初始化 *n* 。
2.  从左到右迭代矩形。
3.  转动每个矩形，使其宽度尽可能大，但不大于前一个矩形。
4.  如果在一些迭代中没有这样的方法来放置矩形，答案是“否”

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if it possible to form
// rectangles with heights as non-ascending
int rotateRec(int n, int L[], int B[])
{

    // set maximum
    int m = INT_MAX;

    for (int i = 0; i < n; i++) {
        // replace the maximum with previous maximum
        if (max(L[i], B[i]) <= m)
            m = max(L[i], B[i]);

        // replace the minimum with previous minimum
        else if (min(L[i], B[i]) <= m)
            m = min(L[i], B[i]);

        // print NO if the above
        // two conditions fail at least once
        else {
            return 0;
        }
    }
    return 1;
}

// Driver code
int main()
{
    // initialize the number of rectangles
    int n = 3;

    // initialize n rectangles with length and breadth
    int L[] = { 5, 5, 6 };
    int B[] = { 6, 7, 8 };
    rotateRec(n, L, B) == 1 ? cout << "YES"
                            : cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.io.*;

class GFG {

// Function to check if it possible to form
// rectangles with heights as non-ascending
 static int rotateRec(int n, int L[], int B[])
{

    // set maximum
    int m = Integer.MAX_VALUE;

    for (int i = 0; i < n; i++) {
        // replace the maximum with previous maximum
        if (Math.max(L[i], B[i]) <= m)
            m = Math.max(L[i], B[i]);

        // replace the minimum with previous minimum
        else if (Math.min(L[i], B[i]) <= m)
            m = Math.min(L[i], B[i]);

        // print NO if the above
        // two conditions fail at least once
        else {
            return 0;
        }
    }
    return 1;
}

// Driver code

    public static void main (String[] args) {
    // initialize the number of rectangles
    int n = 3;

    // initialize n rectangles with length and breadth
    int L[] = { 5, 5, 6 };
    int B[] = { 6, 7, 8 };
    if(rotateRec(n, L, B) == 1)
     System.out.println( "YES");
     else
     System.out.println( "NO");
    }
}
 // This Code is contributed by inder_verma..
```

## 蟒蛇 3

```
# Python3 implementation of above approach
import sys;

# Function to check if it possible
# to form rectangles with heights
# as non-ascending
def rotateRec(n, L, B):

    # set maximum
    m = sys.maxsize;

    for i in range(n):

        # replace the maximum with
        # previous maximum
        if (max(L[i], B[i]) <= m):
            m = max(L[i], B[i]);

        # replace the minimum
        # with previous minimum
        elif (min(L[i], B[i]) <= m):
            m = min(L[i], B[i]);

        # print NO if the above two
        # conditions fail at least once
        else:
            return 0;

    return 1;

# Driver code

# initialize the number
# of rectangles
n = 3;

# initialize n rectangles
# with length and breadth
L = [5, 5, 6];
B = [ 6, 7, 8 ];
if(rotateRec(n, L, B) == 1):
    print("YES");
else:
    print("NO");

# This code is contributed by mits
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Function to check if it possible
// to form rectangles with heights
// as non-ascending
static int rotateRec(int n, int []L,
                            int []B)
{

    // set maximum
    int m = int.MaxValue ;

    for (int i = 0; i < n; i++)
    {
        // replace the maximum with
        // previous maximum
        if (Math.Max(L[i], B[i]) <= m)
            m = Math.Max(L[i], B[i]);

        // replace the minimum with
        // previous minimum
        else if (Math.Min(L[i], B[i]) <= m)
            m = Math.Min(L[i], B[i]);

        // print NO if the above
        // two conditions fail
        // at least once
        else
        {
            return 0;
        }
    }
    return 1;
}

// Driver code
public static void Main ()
{
    // initialize the number
    // of rectangles
    int n = 3;

    // initialize n rectangles with
    // length and breadth
    int []L = { 5, 5, 6 };
    int []B = { 6, 7, 8 };
    if(rotateRec(n, L, B) == 1)
    Console.WriteLine("YES");
    else
    Console.WriteLine("NO");
}
}

// This code is contributed
// by inder_verma
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to check if it possible
// to form rectangles with heights
// as non-ascending
function rotateRec($n, $L, $B)
{

    // set maximum
    $m = PHP_INT_MAX;

    for ($i = 0; $i < $n; $i++)
    {
        // replace the maximum with
        // previous maximum
        if (max($L[$i], $B[$i]) <= $m)
            $m = max($L[$i], $B[$i]);

        // replace the minimum
        // with previous minimum
        else if (min($L[$i], $B[$i]) <= $m)
            $m = min($L[$i], $B[$i]);

        // print NO if the above two
        // conditions fail at least once
        else
        {
            return 0;
        }
    }
    return 1;
}

// Driver code

// initialize the number
// of rectangles
$n = 3;

// initialize n rectangles
// with length and breadth
$L = array(5, 5, 6 );
$B = array( 6, 7, 8 );
if(rotateRec($n, $L, $B) == 1)
    echo "YES";
else
    echo "NO";

// This code is contributed
// by Shashank
?>
```

## java 描述语言

```
<script>

// javascript implementation of above approach

// Function to check if it possible
// to form rectangles with heights
// as non-ascending
function rotateRec( n, L, B)
{

    // set maximum
    var m = Number.MAX_VALUE

    for (var i = 0; i < n; i++)
    {
        // replace the maximum with
        // previous maximum
        if (Math.max(L[i], B[i]) <= m)
            m = Math.max(L[i], B[i]);

        // replace the minimum with
        // previous minimum
        else if (Math.min(L[i], B[i]) <= m)
            m = Math.min(L[i], B[i]);

        // print NO if the above
        // two conditions fail
        // at least once
        else
        {
            return 0;
        }
    }
    return 1;
}

// Driver code

    // initialize the number
    // of rectangles
    var n = 3;

    // initialize n rectangles with
    // length and breadth
    var L = [ 5, 5, 6 ];
    var B = [ 6, 7, 8 ];
    if(rotateRec(n, L, B) == 1)
    document.write("YES");
    else
    document.write("NO");

</script>
```

**Output:** 

```
NO
```