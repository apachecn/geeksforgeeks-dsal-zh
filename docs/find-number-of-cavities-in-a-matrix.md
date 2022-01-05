# 找出矩阵中空腔的数量

> 原文:[https://www . geeksforgeeks . org/find-矩阵中的空腔数量/](https://www.geeksforgeeks.org/find-number-of-cavities-in-a-matrix/)

计算二维矩阵中空腔的数量，空腔被定义为所有周围的数字都大于中间的数字。
**例:**

> 输入:a = {{4，5，6}，{7，1，5}，{4，5，6}}
> 输出:1
> 输入:a = {{1，2，3}，{4，5，6}，{7，8，9}}
> 输出:1

**来源** : [奥拉面试经验集 13](https://www.geeksforgeeks.org/ola-interview-experience-set-13-sde-2/)
以下是上述做法的执行情况。

## C++

```
// C++ program find number of cavities in a matrix
#include <bits/stdc++.h>
using namespace std;

const int MAX = 100;

int countCavities(int a[][MAX], int n)
{
    int A[n + 2][n + 2];
    int coun = 0;

    // form another matrix with one extra layer of
    // boundary elements.
    // Boundary elements will contain max value.
    for (int i = 0; i < n + 2; i++) {
        for (int j = 0; j < n + 2; j++) {
            if ((i == 0) || (j == 0) || (i == n + 1) ||
                                         (j == n + 1))
                A[i][j] = INT_MAX;
            else
                A[i][j] = a[i - 1][j - 1];
        }
    }

    // Check for cavities in the modified matrix
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= n; j++) {

            // check for all  directions
            if ((A[i][j] < A[i - 1][j]) && (A[i][j] < A[i + 1][j]) &&
                (A[i][j] < A[i][j - 1]) && (A[i][j] < A[i][j + 1]) &&
                (A[i][j] < A[i - 1][j - 1]) && (A[i][j] < A[i + 1][j + 1]) &&
                (A[i][j] < A[i - 1][j + 1]) && (A[i][j] < A[i + 1][j - 1]))
                coun++;
        }
    }

    return coun;
}

int main()
{
    int a[][MAX] = { { 4, 5, 6 }, { 7, 1, 5 }, { 4, 5, 6 } };
    int n = 3;
    cout << countCavities(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program find number of cavities in a matrix
class GfG {

static int MAX = 100;

static int countCavities(int a[][], int n)
{
    int A[][] = new int[n + 2][n + 2];
    int coun = 0;

    // form another matrix with one extra layer of
    // boundary elements.
    // Boundary elements will contain max value.
    for (int i = 0; i < n + 2; i++) {
        for (int j = 0; j < n + 2; j++) {
            if ((i == 0) || (j == 0) || (i == n + 1) || (j == n + 1))
                A[i][j] = Integer.MAX_VALUE;
            else
                A[i][j] = a[i - 1][j - 1];
        }
    }

    // Check for cavities in the modified matrix
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= n; j++) {

            // check for all directions
            if ((A[i][j] < A[i - 1][j]) && (A[i][j] < A[i + 1][j]) &&
                (A[i][j] < A[i][j - 1]) && (A[i][j] < A[i][j + 1]) &&
                (A[i][j] < A[i - 1][j - 1]) && (A[i][j] < A[i + 1][j + 1]) &&
                (A[i][j] < A[i - 1][j + 1]) && (A[i][j] < A[i + 1][j - 1]))
                coun++;
        }
    }

    return coun;
}

public static void main(String[] args)
{
    int a[][] = new int[][]{{ 4, 5, 6 }, { 7, 1, 5 }, { 4, 5, 6 }};
    int n = 3;
System.out.println(countCavities(a, n));
}
}
```

## C#

```
// C# program find number of cavities in a matrix
using System;

class GfG
{

    static int MAX = 100;

    static int countCavities(int [,]a, int n)
    {
        int [,]A = new int[n + 2, n + 2];
        int coun = 0;

        // form another matrix with one extra layer of
        // boundary elements.
        // Boundary elements will contain max value.
        for (int i = 0; i < n + 2; i++)
        {
            for (int j = 0; j < n + 2; j++)
            {
                if ((i == 0) || (j == 0) || (i == n + 1) || (j == n + 1))
                    A[i, j] = int.MaxValue;
                else
                    A[i, j] = a[i - 1, j - 1];
            }
        }

        // Check for cavities in the modified matrix
        for (int i = 1; i <= n; i++)
        {
            for (int j = 1; j <= n; j++)
            {

                // check for all directions
                if ((A[i, j] < A[i - 1, j]) && (A[i, j] < A[i + 1, j]) &&
                    (A[i, j] < A[i, j - 1]) && (A[i, j] < A[i, j + 1]) &&
                    (A[i, j] < A[i - 1, j - 1]) && (A[i, j] < A[i + 1, j + 1]) &&
                    (A[i, j] < A[i - 1, j + 1]) && (A[i, j] < A[i + 1, j - 1]))
                    coun++;
            }
        }
        return coun;
    }

    public static void Main(String[] args)
    {
        int [,]a = new int[,]{{ 4, 5, 6 }, { 7, 1, 5 }, { 4, 5, 6 }};
        int n = 3;
        Console.WriteLine(countCavities(a, n));
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program find number of cavities
// in a matrix
function countCavities($a, $n)
{
    $A = array();
    $coun = 0;

    // form another matrix with one extra
    // layer of boundary elements.
    // Boundary elements will contain
    // max value.
    for ($i = 0; $i < $n + 2; $i++)
    {
        for ($j = 0; $j < $n + 2; $j++)
        {
            if (($i == 0) || ($j == 0) ||
                ($i == $n + 1) || ($j == $n + 1))
                $A[$i][$j] = 100;
            else
                $A[$i][$j] = $a[$i - 1][$j - 1];
        }
    }

    // Check for cavities in the modified matrix
    for ($i = 1; $i <= $n; $i++)
    {
        for ($j = 1; $j <= $n; $j++)
        {

            // check for all directions
            if (($A[$i][$j] < $A[$i - 1][$j]) &&
                ($A[$i][$j] < $A[$i + 1][$j]) &&
                ($A[$i][$j] < $A[$i][$j - 1]) &&
                ($A[$i][$j] < $A[$i][$j + 1]) &&
                ($A[$i][$j] < $A[$i - 1][$j - 1]) &&
                ($A[$i][$j] < $A[$i + 1][$j + 1]) &&
                ($A[$i][$j] < $A[$i - 1][$j + 1]) &&
                ($A[$i][$j] < $A[$i + 1][$j - 1]))
                $coun++;
        }
    }

    return $coun;
}

// Driver Code
$a = array(array(4, 5, 6),
           array(7, 1, 5),
           array(4, 5, 6));
$n = 3;
echo(countCavities($a, $n));

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
// Javascript program find number of cavities in a matrix

MAX = 100;

function countCavities( a, n)
{
    var A = new Array(n+2).fill(0).map(() => new Array(n+2).fill(0));
    var coun = 0;

    // form another matrix with one extra layer of
    // boundary elements.
    // Boundary elements will contain max value.
    for (var i = 0; i < n + 2; i++) {
        for (var j = 0; j < n + 2; j++) {
            if ((i == 0) || (j == 0) || (i == n + 1) ||
                                         (j == n + 1))
                A[i][j] = Number.MAX_VALUE;
            else
                A[i][j] = a[i - 1][j - 1];
        }
    }

    // Check for cavities in the modified matrix
    for (var i = 1; i <= n; i++) {
        for (var j = 1; j <= n; j++) {

            // check for all  directions
            if ((A[i][j] < A[i - 1][j]) && (A[i][j] < A[i + 1][j]) &&
                (A[i][j] < A[i][j - 1]) && (A[i][j] < A[i][j + 1]) &&
                (A[i][j] < A[i - 1][j - 1]) && (A[i][j] < A[i + 1][j + 1]) &&
                (A[i][j] < A[i - 1][j + 1]) && (A[i][j] < A[i + 1][j - 1]))
                coun++;
        }
    }

    return coun;
}

 var a = [ [ 4, 5, 6 ],[ 7, 1, 5 ], [ 4, 5, 6 ] ];
 var n = 3;
 document.write( countCavities(a, n));

// This code is contributed by SoumikMondal
</script>
```

**输出:**

```
1
```

**优化**我们可以通过以下步骤避免使用额外的空间和额外的条件。
1)明确检查四个角元素，第一行、最后一行、第一列和最后一列的剩余元素。
2)使用上述逻辑检查剩余元素。