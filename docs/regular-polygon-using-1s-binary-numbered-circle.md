# 在二进制编号圆中仅使用 1 的正多边形

> 原文:[https://www . geesforgeks . org/正多边形-使用-1s-二进制-编号-圆形/](https://www.geeksforgeeks.org/regular-polygon-using-1s-binary-numbered-circle/)

给定一个二进制整数数组，假设这些值以相等的距离保持在圆周上。我们需要知道是否有可能只使用 1 作为顶点来绘制正多边形，如果有可能，那么打印正多边形的最大边数。
**例:**

```
Input : arr[] = [1, 1, 1, 0, 1, 0]
Output : Polygon possible with side length 3
We can draw a regular triangle having 1s as 
its vertices as shown in below diagram (a).

Input : arr[] = [1, 0, 1, 0, 1, 0, 1, 0, 1, 1]
Output : Polygon possible with side length 5
We can draw a regular pentagon having 1s as its 
vertices as shown in below diagram (b).
```

我们可以通过得到一个可能的多边形的顶点数和数组中值的总数之间的关系来解决这个问题。假设圆中一个可能的正多边形有 K 个顶点或 K 条边，那么它应该满足两个条件才能得到答案，
如果给定的数组大小是 N，那么 K 应该划分 N，否则 K 个顶点不能以相等的方式划分 N 个顶点成为正多边形。
下一件事是在所选多边形的每个顶点都应该有一个。
经过以上几点，我们可以看到，为了解决这个问题，我们需要迭代 N 的除数，然后检查在所选除数的距离上数组的每个值是否都是 1。如果是 1，那么我们找到了解决方案。我们只需从 1 迭代到 sqrt(N)，就可以在 O(sqrt(N))时间内迭代所有除数。你可以在这里阅读更多关于[的信息](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)。

## C++

```
// C++ program to find whether a regular polygon
// is possible in circle with 1s as vertices
#include <bits/stdc++.h>
using namespace std;

// method returns true if polygon is possible with
// 'midpoints' number of midpoints
bool checkPolygonWithMidpoints(int arr[], int N,
                                  int midpoints)
{
    // loop for getting first vertex of polygon
    for (int j = 0; j < midpoints; j++)
    {
        int val = 1;

        // loop over array values at 'midpoints' distance
        for (int k = j; k < N; k += midpoints)
        {
            // and(&) all those values, if even one of
            // them is 0, val will be 0
            val &= arr[k];
        }

        /*  if val is still 1 and (N/midpoints) or (number
            of vertices) are more than two (for a polygon
            minimum) print result and return true */
        if (val && N/midpoints > 2)
        {
            cout << "Polygon possible with side length " <<
                 << (N/midpoints) << endl;
            return true;
        }
    }
    return false;
}

// method prints sides in the polygon or print not
// possible in case of no possible polygon
void isPolygonPossible(int arr[], int N)
{
    //  limit for iterating over divisors
    int limit = sqrt(N);
    for (int i = 1; i <= limit; i++)
    {
        // If i divides N then i and (N/i) will
        // be divisors
        if (N % i == 0)
        {
            //  check polygon for both divisors
            if (checkPolygonWithMidpoints(arr, N, i) ||
                checkPolygonWithMidpoints(arr, N, (N/i)))
                return;
        }
    }

    cout << "Not possiblen";
}

// Driver code to test above methods
int main()
{
    int arr[] = {1, 0, 1, 0, 1, 0, 1, 0, 1, 1};
    int N = sizeof(arr) / sizeof(arr[0]);
    isPolygonPossible(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find whether a regular polygon
// is possible in circle with 1s as vertices

class Test
{
    // method returns true if polygon is possible with
    // 'midpoints' number of midpoints
    static boolean checkPolygonWithMidpoints(int arr[], int N,
                                      int midpoints)
    {
        // loop for getting first vertex of polygon
        for (int j = 0; j < midpoints; j++)
        {
            int val = 1;

            // loop over array values at 'midpoints' distance
            for (int k = j; k < N; k += midpoints)
            {
                // and(&) all those values, if even one of
                // them is 0, val will be 0
                val &= arr[k];
            }

            /*  if val is still 1 and (N/midpoints) or (number
                of vertices) are more than two (for a polygon
                minimum) print result and return true */
            if (val != 0 && N/midpoints > 2)
            {
                System.out.println("Polygon possible with side length " +
                                               N/midpoints);
                return true;
            }
        }
        return false;
    }

    // method prints sides in the polygon or print not
    // possible in case of no possible polygon
    static void isPolygonPossible(int arr[], int N)
    {
        //  limit for iterating over divisors
        int limit = (int)Math.sqrt(N);
        for (int i = 1; i <= limit; i++)
        {
            // If i divides N then i and (N/i) will
            // be divisors
            if (N % i == 0)
            {
                //  check polygon for both divisors
                if (checkPolygonWithMidpoints(arr, N, i) ||
                    checkPolygonWithMidpoints(arr, N, (N/i)))
                    return;
            }
        }

        System.out.println("Not possible");
    }

    // Driver method
    public static void main(String args[])
    {
        int arr[] = {1, 0, 1, 0, 1, 0, 1, 0, 1, 1};

        isPolygonPossible(arr, arr.length);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find whether a
# regular polygon is possible in circle
# with 1s as vertices
from math import sqrt

# method returns true if polygon is
# possible with 'midpoints' number
# of midpoints
def checkPolygonWithMidpoints(arr, N, midpoints) :

    # loop for getting first vertex of polygon
    for j in range(midpoints) :

        val = 1

        # loop over array values at
        # 'midpoints' distance
        for k in range(j , N, midpoints) :

            # and(&) all those values, if even 
            # one of them is 0, val will be 0
            val &= arr[k]

        # if val is still 1 and (N/midpoints) or (number
        # of vertices) are more than two (for a polygon
        # minimum) print result and return true
        if (val and N // midpoints > 2) :

            print("Polygon possible with side length" ,
                                      (N // midpoints))
            return True

    return False

# method prints sides in the polygon or print
# not possible in case of no possible polygon
def isPolygonPossible(arr, N) :

    # limit for iterating over divisors
    limit = sqrt(N)
    for i in range(1, int(limit) + 1) :

        # If i divides N then i and (N/i)
        # will be divisors
        if (N % i == 0) :

            # check polygon for both divisors
            if (checkPolygonWithMidpoints(arr, N, i) or
                checkPolygonWithMidpoints(arr, N, (N // i))):
                return

    print("Not possiblen")

# Driver code
if __name__ == "__main__" :

    arr = [1, 0, 1, 0, 1, 0, 1, 0, 1, 1]
    N = len(arr)
    isPolygonPossible(arr, N)

# This code is contributed by Ryuga
```

## C#

```
// C# program to find whether
// a regular polygon is possible
// in circle with 1s as vertices
using System;

class GFG
{

// method returns true if
// polygon is possible
// with 'midpoints' number
// of midpoints
static bool checkPolygonWithMidpoints(int []arr, int N,
                                      int midpoints)
{
    // loop for getting first
    // vertex of polygon
    for (int j = 0; j < midpoints; j++)
    {
        int val = 1;

        // loop over array values
        // at 'midpoints' distance
        for (int k = j; k < N; k += midpoints)
        {
            // and(&) all those values,
            // if even one of them is 0,
            // val will be 0
            val &= arr[k];
        }

        /* if val is still 1 and
           (N/midpoints) or (number
           of vertices) are more than
           two (for a polygon minimum)
           print result and return true */
        if (val != 0 && N / midpoints > 2)
        {
            Console.WriteLine("Polygon possible with " +
                                        "side length " +
                                         N / midpoints);
            return true;
        }
    }
    return false;
}

// method prints sides in the
// polygon or print not possible
// in case of no possible polygon
static void isPolygonPossible(int []arr,
                              int N)
{
    // limit for iterating
    // over divisors
    int limit = (int)Math.Sqrt(N);
    for (int i = 1; i <= limit; i++)
    {
        // If i divides N then i
        // and (N/i) will be divisors
        if (N % i == 0)
        {
            // check polygon for
            // both divisors
            if (checkPolygonWithMidpoints(arr, N, i) ||
                checkPolygonWithMidpoints(arr, N, (N / i)))
                return;
        }
    }

    Console.WriteLine("Not possible");
}

// Driver Code
static public void Main ()
{
    int []arr = {1, 0, 1, 0, 1,
                 0, 1, 0, 1, 1};

    isPolygonPossible(arr, arr.Length);
}
}

// This code is contributed by jit_t
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find whether
// a regular polygon is possible
// in circle with 1s as vertices
// method returns true if polygon
// is possible with 'midpoints'
// number of midpoints

function checkPolygonWithMidpoints($arr, $N,
                                   $midpoints)
{
    // loop for getting first
    // vertex of polygon
    for ($j = 0; $j < $midpoints; $j++)
    {
        $val = 1;

        // loop over array values
        // at 'midpoints' distance
        for ($k = $j; $k < $N; $k += $midpoints)
        {
            // and(&) all those values,
            // if even one of them is 0,
            // val will be 0
            $val &= $arr[$k];
        }

        /* if val is still 1 and
        (N/midpoints) or (number
        of vertices) are more than
        two (for a polygon minimum)
        print result and return true */
        if ($val && $N / $midpoints > 2)
        {
            echo "Polygon possible with side length " ,
                              ($N / $midpoints) , "\n";
            return true;
        }
    }
    return false;
}

// method prints sides in
// the polygon or print not
// possible in case of no
// possible polygon
function isPolygonPossible($arr, $N)
{
    // limit for iterating
    // over divisors
    $limit = sqrt($N);
    for ($i = 1; $i <= $limit; $i++)
    {
        // If i divides N then
        // i and (N/i) will be
        // divisors
        if ($N % $i == 0)
        {
            // check polygon for
            // both divisors
            if (checkPolygonWithMidpoints($arr, $N, $i) ||
                checkPolygonWithMidpoints($arr, $N, ($N / $i)))
                return;
        }
    }

echo "Not possiblen";
}

// Driver Code
$arr = array(1, 0, 1, 0, 1,
             0, 1, 0, 1, 1);
$N = sizeof($arr);
isPolygonPossible($arr, $N);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// Javascript program to
// find whether a regular polygon
// is possible in circle with 1s as vertices

// method returns true if polygon is possible with
// 'midpoints' number of midpoints
function checkPolygonWithMidpoints(arr, N, midpoints)
{
    // loop for getting first vertex of polygon
    for (let j = 0; j < midpoints; j++)
    {
        let val = 1;

        // loop over array values at
        // 'midpoints' distance
        for (let k = j; k < N; k += midpoints)
        {
            // and(&) all those values,
            // if even one of
            // them is 0, val will be 0
            val &= arr[k];
        }

        /*  if val is still 1 and
            (N/midpoints) or (number
            of vertices) are more than
            two (for a polygon
            minimum) print result and return true */
        if (val && parseInt(N/midpoints) > 2)
        {
            document.write(
            "Polygon possible with side length " +
            parseInt(N/midpoints) + "<br>"
            );
            return true;
        }
    }
    return false;
}

// method prints sides in the polygon or print not
// possible in case of no possible polygon
function isPolygonPossible(arr, N)
{
    //  limit for iterating over divisors
    let limit = Math.sqrt(N);
    for (let i = 1; i <= limit; i++)
    {
        // If i divides N then i and (N/i) will
        // be divisors
        if (N % i == 0)
        {
            //  check polygon for both divisors
            if (checkPolygonWithMidpoints(arr, N, i) ||
                checkPolygonWithMidpoints(arr, N,
                parseInt(N/i)))
                return;
        }
    }

    document.write("Not possible");
}

// Driver code to test above methods
    let arr = [1, 0, 1, 0, 1, 0, 1, 0, 1, 1];
    let N = arr.length;
    isPolygonPossible(arr, N);

</script>
```

**输出:**

```
Polygon possible with side length 5
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。