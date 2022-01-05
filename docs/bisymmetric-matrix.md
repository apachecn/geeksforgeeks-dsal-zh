# 双对称矩阵

> 原文:[https://www.geeksforgeeks.org/bisymmetric-matrix/](https://www.geeksforgeeks.org/bisymmetric-matrix/)

一个[双对称矩阵](https://en.wikipedia.org/wiki/Bisymmetric_matrix)是一个关于它的两条主对角线对称的正方形矩阵。给定一个矩阵大小 **n x n** 。任务是检查它是否是双对称的。
**例:**

```
Input : n = 3, m[][] = { { 1, 2, 3 },
                         { 2, 5, 2 },
                         { 3, 2, 1 } };

Output : Yes
Given matrix is symmetric along both the diagonal.

Input : n = 3, m[][] = { { 1, 2, 3 },
                         { 9, 5, 2 },
                         { 3, 2, 1 } };
Output : No
```

这个想法是检查给定的矩阵是否沿对角线对称。对于从左上角到右下角的对角线，检查 m[i][j]处的元素是否等于 m[j][i]。对于从右上到左下的对角线，检查 m[i][j]处的元素是否等于 m[n–j–1][n–I–1]。
如果上述两个条件都成立，那么给定的矩阵就是双对称矩阵，否则不是。

## C++

```
// CPP Program to check if a
// given matrix is Bisymmetric
// matrix
#include <bits/stdc++.h>
using namespace std;

#define MAX 100

// Return if the given
// matrix is Bisymmetric matrix
bool checkBisymmetric(int m[][MAX],
                      int n)
{
    // Checking Across
    // Forward Diagonal
    for (int i = 0; i < n; i++)
        for (int j = 0; j < i; j++)

            // check if corresponding
            // position element are equal.
            if (m[i][j] != m[j][i])
                return false;

    // Backward Diagonal
    for (int i = 0; i < n; i++)

        // for each column,
        // upto main diagonal
        for (int j = 0; j < n - i; j++)

            // check if corresponding
            // position element are equal.
            if (m[i][j] != m[n - j - 1]
                            [n - i - 1])
                return false;

    return true;
}

// Driven Code
int main()
{
    int n = 3;
    int m[][MAX] = { { 1, 2, 3 },
                    { 2, 5, 2 },
                    { 3, 2, 1 } };

    (checkBisymmetric(m, n) ? (cout << "Yes") :
                              (cout << "No"));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to check if a given matrix
// is Bisymmetric matrix
import java.io.*;

class GFG {

    static int MAX = 100;

    // Return if the given
    // matrix is Bisymmetric matrix
    static boolean checkBisymmetric(int m[][],
                        int n)
    {

        // Checking Across Forward Diagonal
        for (int i = 0; i < n; i++)
            for (int j = 0; j < i; j++)

                // check if corresponding
                // position element are equal.
                if (m[i][j] != m[j][i])
                    return false;

        // Backward Diagonal
        for (int i = 0; i < n; i++)

            // for each column,
            // upto main diagonal
            for (int j = 0; j < n - i; j++)

                // check if corresponding
                // position element are equal.
                if (m[i][j] != m[n - j - 1]
                                [n - i - 1])
                    return false;

        return true;
    }

    // Driven Code
    public static void main (String[] args)
    {
        int n = 3;

        int m[][] = { { 1, 2, 3 },
                      { 2, 5, 2 },
                      { 3, 2, 1 } };

        if(checkBisymmetric(m, n))
            System.out.println( "Yes");
        else
            System.out.println( "No");
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python3 Program to check if a
# given matrix is Bisymmetric
# matrix

# Return if the given matrix
# is Bisymmetric matrix
def checkBisymmetric(m, n) :

    # Checking Across
    # Forward Diagonal
    for i in range(0, n) :
        for j in range(0, i) :
            # check if corresponding
            # position element are equal.
            if (m[i][j] != m[j][i]) :
                return false            

    # Backward Diagonal
    for i in range(0, n) :
        # for each column,
        # upto main diagonal
        for j in range(0, n - i) :

            # check if corresponding
            # position element are
            # equal.
            if (m[i][j] !=
             m[n - j - 1][n - i - 1]) :
                return False
    return True;

# Driven Code
n = 3;
m = [[ 1, 2, 3 ],
     [ 2, 5, 2 ],
     [ 3, 2, 1 ]]

if(checkBisymmetric(m, n)) :
    print ("Yes")
else :
    print ("No")

# This code is contributed by
# Manish Shaw (manishshaw1)
```

## C#

```
// C# Program to check if a given matrix
// is Bisymmetric matrix
using System;

class GFG {

    //static int MAX = 100;

    // Return if the given
    // matrix is Bisymmetric matrix
    static bool checkBisymmetric(int [,]m,
                        int n)
    {

        // Checking Across Forward Diagonal
        for (int i = 0; i < n; i++)
            for (int j = 0; j < i; j++)

                // check if corresponding
                // position element are equal.
                if (m[i,j] != m[j,i])
                    return false;

        // Backward Diagonal
        for (int i = 0; i < n; i++)

            // for each column,
            // upto main diagonal
            for (int j = 0; j < n - i; j++)

                // check if corresponding
                // position element are equal.
                if (m[i,j] != m[n - j - 1,
                                n - i - 1])
                    return false;

        return true;
    }

    // Driven Code
    public static void Main ()
    {
        int n = 3;

        int [,]m = { { 1, 2, 3 },
                    { 2, 5, 2 },
                    { 3, 2, 1 } };

        if(checkBisymmetric(m, n))
            Console.WriteLine( "Yes");
        else
            Console.WriteLine( "No");
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to check if a
// given matrix is Bisymmetric
// matrix

// MAX = 100;

// Return if the given matrix
// is Bisymmetric matrix
function checkBisymmetric($m, $n)
{
    // Checking Across
    // Forward Diagonal
    for ( $i = 0; $i < $n; $i++)
        for ( $j = 0; $j < $i; $j++)

            // check if corresponding
            // position element are equal.
            if ($m[$i][$j] != $m[$j][$i])
                return false;

    // Backward Diagonal
    for ( $i = 0; $i < $n; $i++)

        // for each column,
        // upto main diagonal
        for ( $j = 0; $j < $n - $i; $j++)

            // check if corresponding
            // position element are equal.
            if ($m[$i][$j] != $m[$n - $j - 1]
                                [$n - $i - 1])
                return false;

    return true;
}

// Driven Code
$n = 3;
$m = array(array( 1, 2, 3 ),
           array( 2, 5, 2 ),
           array( 3, 2, 1 ));

if(checkBisymmetric($m, $n))
echo "Yes" ;
else
echo "No";

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript Program to check if a given matrix is Bisymmetric matrix
    let MAX = 100;

    // Return if the given
    // matrix is Bisymmetric matrix
    function checkBisymmetric(m, n)
    {

        // Checking Across Forward Diagonal
        for (let i = 0; i < n; i++)
            for (let j = 0; j < i; j++)

                // check if corresponding
                // position element are equal.
                if (m[i][j] != m[j][i])
                    return false;

        // Backward Diagonal
        for (let i = 0; i < n; i++)

            // for each column,
            // upto main diagonal
            for (let j = 0; j < n - i; j++)

                // check if corresponding
                // position element are equal.
                if (m[i][j] != m[n - j - 1]
                                [n - i - 1])
                    return false;

        return true;
    }

    let n = 3;

    let m = [ [ 1, 2, 3 ],
              [ 2, 5, 2 ],
              [ 3, 2, 1 ] ];

    if(checkBisymmetric(m, n))
      document.write( "Yes");
    else
      document.write( "No");

    // This code is contributed by divyeshrabadiya07.
</script>
```

**Output :** 

```
Yes
```