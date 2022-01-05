# 检查给定矩阵是否正交

> 原文:[https://www . geesforgeks . org/check-是否-给定-矩阵-正交-非/](https://www.geeksforgeeks.org/check-whether-given-matrix-orthogonal-not/)

给我们一个矩阵，我们需要检查它是否是正交矩阵。正交矩阵是正方形矩阵，并且满足以下条件:

```
  A*At = I
```

**例:**

```
Input:  1 0 0
        0 1 0
        0 0 1
Output: Yes
Given Matrix is an orthogonal matrix. When
we multiply it with its transpose, we get
identity matrix.

Input:  1 2 3
        4 5 6
        7 8 9
Output: No
Given Matrix Is Not An Orthogonal Matrix
```

**简单解法:**思路很简单，我们先找到矩阵的转置。然后我们用给定的矩阵乘以转置。最后我们检查得到的矩阵是否恒等式。

## c++

```
// C++ code to check whether
// a matrix is orthogonal or not
#include <bits/stdc++.h>
using namespace std;

#define MAX 100

bool isOrthogonal(int a[][MAX],
                  int m, int n)
{
if (m != n)
    return false;

// Find transpose
int trans[n][n];
for (int i = 0; i < n; i++)
    for (int j = 0; j < n; j++)
    trans[i][j] = a[j][i];

// Find product of a[][]
// and its transpose
int prod[n][n];
for (int i = 0; i < n; i++)
{
    for (int j = 0; j < n; j++)
    {

    int sum = 0;
    for (int k = 0; k < n; k++)
    {

        // Since we are multiplying with
        // transpose of itself. We use
        sum = sum + (a[i][k] * a[j][k]);
    }

    prod[i][j] = sum;
    }
}

// Check if product is identity matrix
for (int i = 0; i < n; i++)
{
    for (int j = 0; j < n; j++)
    {
    if (i != j && prod[i][j] != 0)
        return false;
    if (i == j && prod[i][j] != 1)
        return false;
    }
}

return true;
}

// Driver Code
int main()
{

int a[][MAX] = {{1, 0, 0},
                {0, 1, 0},
                {0, 0, 1}};
if (isOrthogonal(a, 3, 3))
    cout << "Yes";
else
    cout << "No";
return 0;
}
```

## Java

```
// Java code to check whether
// a matrix is orthogonal or not
import java .io.*;
class GFG {

    //static int MAX =100;
    static boolean isOrthogonal(int [][]a,
                                int m,
                                int n)
    {
        if (m != n)
            return false;

        // Find transpose
        int [][]trans = new int[n][n];
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                trans[i][j] = a[j][i];

        // Find product of a[][]
        // and its transpose
        int [][]prod = new int[n][n];
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {

                int sum = 0;
                for (int k = 0; k < n; k++)
                {
                    // Since we are multiplying
                    // transpose of itself. We use
                    sum = sum + (a[i][k] * a[j][k]);
                }

                prod[i][j] = sum;
            }
        }

        // Check if product is
        // identity matrix
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {
                if (i != j && prod[i][j] != 0)
                    return false;
                if (i == j && prod[i][j] != 1)
                    return false;
            }
        }

        return true;
    }

    // Driver code
    static public void main (String[] args)
    {
        int [][]a = {{1, 0, 0},
                    {0, 1, 0},
                    {0, 0, 1}};
        if (isOrthogonal(a, 3, 3))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by anuj_67.
```

## python 3

```
# Python code to check
# whether a matrix is
# orthogonal or not

def isOrthogonal(a, m, n) :
    if (m != n) :
        return False

    trans = [[0 for x in range(n)]
                for y in range(n)]

    # Find transpose
    for i in range(0, n) :
        for j in range(0, n) :
            trans[i][j] = a[j][i]

    prod = [[0 for x in range(n)]
               for y in range(n)]

    # Find product of a[][]
    # and its transpose
    for i in range(0, n) :
        for j in range(0, n) :

            sum = 0
            for k in range(0, n) :

                # Since we are multiplying
                # with transpose of itself.
                # We use
                sum = sum + (a[i][k] *
                             a[j][k])

            prod[i][j] = sum

    # Check if product is
    # identity matrix
    for i in range(0, n) :
        for j in range(0, n) :

            if (i != j and prod[i][j] != 0) :
                return False
            if (i == j and prod[i][j] != 1) :
                return False

    return True

# Driver Code
a = [[1, 0, 0],
    [0, 1, 0],
    [0, 0, 1]]

if (isOrthogonal(a, 3, 3)) :
    print ("Yes")
else :
    print ("No")

# This code is contributed by
# Manish Shaw(manishshaw1)
```

## c#

```
// C# code to check whether
// a matrix is orthogonal or not
using System;

class GFG
{

    //static int MAX =100;
    static bool isOrthogonal(int [,]a,
                             int m,
                             int n)
    {
        if (m != n)
            return false;

        // Find transpose
        int [,]trans = new int[n, n];
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                trans[i, j] = a[j, i];

        // Find product of a[][]
        // and its transpose
        int [,]prod = new int[n, n];
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {

                int sum = 0;
                for (int k = 0; k < n; k++)
                {
                    // Since we are multiplying
                    // transpose of itself. We use
                    sum = sum + (a[i, k] * a[j, k]);
                }

                prod[i, j] = sum;
            }
        }

        // Check if product is
        // identity matrix
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {
                if (i != j && prod[i, j] != 0)
                    return false;
                if (i == j && prod[i, j] != 1)
                    return false;
            }
        }

        return true;
    }

    // Driver code
    static public void Main ()
    {
        int [,]a = {{1, 0, 0},
                    {0, 1, 0},
                    {0, 0, 1}};
        if (isOrthogonal(a, 3, 3))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by vt_m
```

## PHP

```
<?php
// PHP code to check whether
// a matrix is orthogonal or not

function isOrthogonal($a,
                      $m, $n)
{
    if ($m != $n)
        return false;

    // Find transpose
    for($i = 0; $i < $n; $i++)
        for ($j = 0; $j < $n; $j++)
        $trans[$i][$j] = $a[$j][$i];

    // Find product of a[][]
    // and its transpose
    for($i = 0; $i < $n; $i++)
    {
        for ($j = 0; $j < $n; $j++)
        {

        $sum = 0;
        for ($k = 0; $k < $n; $k++)
        {

            // Since we are multiplying with
            // transpose of itself. We use
            $sum = $sum + ($a[$i][$k] *
                           $a[$j][$k]);
        }

        $prod[$i][$j] = $sum;
        }
    }

    // Check if product is
    // identity matrix
    for($i = 0; $i < $n; $i++)
    {
        for ($j = 0; $j < $n; $j++)
        {
            if ($i != $j && $prod[$i][$j] != 0)
                return false;
            if ($i == $j && $prod[$i][$j] != 1)
                return false;
        }
    }

    return true;
}

    // Driver Code
    $a = array(array(1, 0, 0),
               array(0, 1, 0),
               array(0, 0, 1));
    if (isOrthogonal($a, 3, 3))
        echo "Yes";
    else
        echo "No";

// This code is contributed by ajit.
?>
```

## Javascript

```
<script>

// Javascript code to check whether
// a matrix is orthogonal or not

// static int MAX =100;
function isOrthogonal(a, m, n)
{
    if (m != n)
        return false;

    // Find transpose
    let trans = new Array(n);

    for(let i = 0; i < n; i++)
    {
        trans[i] = new Array(n);
        for(let j = 0; j < n; j++)
            trans[i][j] = a[j][i];
    }

    // Find product of a[][]
    // and its transpose
    let prod = new Array(n);
    for(let i = 0; i < n; i++)
    {
        prod[i] = new Array(n);
        for(let j = 0; j < n; j++)
        {
            let sum = 0;
            for(let k = 0; k < n; k++)
            {

                // Since we are multiplying
                // transpose of itself. We use
                sum = sum + (a[i][k] * a[j][k]);
            }
            prod[i][j] = sum;
        }
    }

    // Check if product is
    // identity matrix
    for(let i = 0; i < n; i++)
    {
        for(let j = 0; j < n; j++)
        {
            if (i != j && prod[i][j] != 0)
                return false;
            if (i == j && prod[i][j] != 1)
                return false;
        }
    }
    return true;
}

// Driver code
let a = [ [ 1, 0, 0 ],
          [ 0, 1, 0 ],
          [ 0, 0, 1 ] ];

if (isOrthogonal(a, 3, 3))
  document.write("Yes");
else
  document.write("No");

// This code is contributed by divyesh072019

</script>
```

**输出:**

```
Yes
```