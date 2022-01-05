# 检查给定矩阵是否为汉克尔

> 原文:[https://www . geesforgeks . org/check-given-matrix-Hankel-not/](https://www.geeksforgeeks.org/check-given-matrix-hankel-not/)

给定大小为**n×n**的矩阵 **m[][]** 。任务是检查给定的矩阵是否是汉克尔矩阵。
在线性代数中，以赫尔曼·汉克尔命名的汉克尔矩阵(或称目录矩阵)是一个正方形矩阵，其中从左到右的每条斜对角都是常数。
**示例:**

> **输入:** n = 4，
> m[][] = {
> {1，2，3，5}，
> {2，3，5，8}，
> {3，5，8，0}，
> {5，8，0，9 }
> }；
> **输出:**是
> 所有对角线{1}、{2，2}、{3，3，3}、{5，5，5，5}、{8，8，8}、{9}都有常数值。
> 所以给定的矩阵是汉克尔矩阵。
> 
> **输入:** n = 3，
> m[][] = {
> {1，2，3}，
> {2，3，5}，
> {3，9，8 }
> }；
> **输出:**否

注意，一个矩阵要成为汉克尔矩阵，它必须是这样的形式，

```
a0  a1  a2  a3
a1  a2  a3  a4
a2  a3  a4  a5
a3  a4  a5  a6
```

因此，为了检查给定的矩阵是否是 Hankel 矩阵，我们需要检查每个 m[i][j] == a <sub>i + j</sub> 。现在，一个 <sub>i + j</sub> 可以定义为:

```
         m[i+j][0], if i + j < n
ai + j = 
         m[i + j - n + 1][n-1], otherwise
```

下面是上述方法的实现:

## C++

```
// C++ Program to check if given matrix is
// Hankel Matrix or not.
#include <bits/stdc++.h>
using namespace std;
#define N 4

// Function to check if given matrix is Hankel
// Matrix or not.
bool checkHankelMatrix(int n, int m[N][N])
{
    // for each row
    for (int i = 0; i < n; i++) {

        // for each column
        for (int j = 0; j < n; j++) {

            // checking if i + j is less than n
            if (i + j < n) {

                // checking if the element is equal to the
                // corresponding diagonal constant
                if (m[i][j] != m[i + j][0])
                    return false;
            }
            else {

                // checking if the element is equal to the
                // corresponding diagonal constant
                if (m[i][j] != m[i + j - n + 1][n - 1])
                    return false;
            }
        }
    }

    return true;
}

// Drivers code
int main()
{
    int n = 4;
    int m[N][N] = {
        { 1, 2, 3, 5 },
        { 2, 3, 5, 8 },
        { 3, 5, 8, 0 },
        { 5, 8, 0, 9 }
    };

    checkHankelMatrix(n, m) ? (cout << "Yes")
                            : (cout << "No");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to check if given matrix is
// Hankel Matrix or not.
import java.io.*;
import java.util.*;

class GFG {

    // Function to check if given matrix
    // is Hankel Matrix or not.
    static boolean checkHankelMatrix(int n,
                                 int m[][])
    {
        // for each row
        for (int i = 0; i < n; i++) {

            // for each column
            for (int j = 0; j < n; j++) {

                // checking if i + j is less
                // than n
                if (i + j < n) {

                    // checking if the element
                    // is equal to the
                    // corresponding diagonal
                    // constant
                    if (m[i][j] != m[i + j][0])
                        return false;
                }
                else {

                    // checking if the element
                    // is equal to the
                    // corresponding diagonal
                    // constant
                    if (m[i][j] !=
                       m[i + j - n + 1][n - 1])
                        return false;
                }
            }
        }

        return true;
    }

    // Drivers code
    public static void main(String args[])
    {
        int n = 4;
        int m[][] = {
            { 1, 2, 3, 5 },
            { 2, 3, 5, 8 },
            { 3, 5, 8, 0 },
            { 5, 8, 0, 9 }
        };

        if(checkHankelMatrix(n, m))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by Anuj_67.
```

## 蟒蛇 3

```
# Python 3 Program to check if given matrix is
# Hankel Matrix or not.

N = 4

# Function to check if given matrix is Hankel
# Matrix or not.
def checkHankelMatrix(n, m):

    # for each row
    for i in range( 0, n):

        # for each column
        for j in range( 0, n):

            # checking if i + j is less
            # than n
            if (i + j < n):

                # checking if the element is
                # equal to the corresponding
                # diagonal constant
                if (m[i][j] != m[i + j][0]):
                    return False

            else :

                # checking if the element is
                # equal to the corresponding
                # diagonal constant
                if (m[i][j] !=
                    m[i + j - n + 1][n - 1]):
                    return False

    return True

# Drivers code
n = 4
m =[[1, 2, 3, 5,],
    [2, 3, 5, 8,],
    [3, 5, 8, 0,],
    [5, 8, 0, 9]]
(print("Yes") if checkHankelMatrix(n, m)
                      else print("No"))

# This code is contributed by Smitha.
```

## C#

```
// C# Program to check if given matrix is
// Hankel Matrix or not.
using System;

class GFG {

    // Function to check if given matrix
    // is Hankel Matrix or not.
    static bool checkHankelMatrix(int n,
                                int [,]m)
    {
        // for each row
        for (int i = 0; i < n; i++) {

            // for each column
            for (int j = 0; j < n; j++) {

                // checking if i + j is less
                // than n
                if (i + j < n) {

                    // checking if the element
                    // is equal to the
                    // corresponding diagonal
                    // constant
                    if (m[i, j] != m[i + j, 0])
                        return false;
                }
                else {

                    // checking if the element
                    // is equal to the
                    // corresponding diagonal
                    // constant
                    if (m[i,j] != m[i + j - n
                                  + 1, n - 1])
                        return false;
                }
            }
        }

        return true;
    }

    // Drivers code
    public static void Main()
    {
        int n = 4;
        int [,]m = {
            { 1, 2, 3, 5 },
            { 2, 3, 5, 8 },
            { 3, 5, 8, 0 },
            { 5, 8, 0, 9 }
        };

        if(checkHankelMatrix(n, m))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by Anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to check if given matrix is
// Hankel Matrix or not.
$N = 4;

// Function to check if
// given matrix is Hankel
// Matrix or not.
function checkHankelMatrix( $n, $m)
{

    // for each row
    for($i = 0; $i < $n; $i++) {

        // for each column
        for ($j = 0;$j < $n; $j++) {

            // checking if i + j
            // is less than n
            if ($i + $j < $n) {

                // checking if the element
                // is equal to the corresponding
                // diagonal constant
                if ($m[$i][$j] != $m[$i + $j][0])
                    return false;
            }
            else {

                // checking if the element
                // is equal to the
                // corresponding diagonal constant
                if ($m[$i][$j] != $m[$i + $j -
                             $n + 1][$n - 1])
                    return false;
            }
        }
    }

    return true;
}

    // Driver code
    $n = 4;
    $m = array(array( 1, 2, 3, 5 ),
               array( 2, 3, 5, 8 ),
               array( 3, 5, 8, 0 ),
               array( 5, 8, 0, 9 ));
    if(checkHankelMatrix($n, $m))
        echo "Yes";
    else
        echo "No";

// This code is contributed by Anuj_67.
?>
```

## java 描述语言

```
<script>

// Java script Program to check if given matrix is
// Hankel Matrix or not.

    // Function to check if given matrix
    // is Hankel Matrix or not.
    function checkHankelMatrix(n,m)
    {
        // for each row
        for (let i = 0; i < n; i++) {

            // for each column
            for (let j = 0; j < n; j++) {

                // checking if i + j is less
                // than n
                if (i + j < n) {

                    // checking if the element
                    // is equal to the
                    // corresponding diagonal
                    // constant
                    if (m[i][j] != m[i + j][0])
                        return false;
                }
                else {

                    // checking if the element
                    // is equal to the
                    // corresponding diagonal
                    // constant
                    if (m[i][j] !=
                    m[i + j - n + 1][n - 1])
                        return false;
                }
            }
        }

        return true;
    }

    // Drivers code

        let n = 4;
        let m = [
            [1, 2, 3, 5 ],
            [ 2, 3, 5, 8] ,
            [ 3, 5, 8, 0 ],
            [ 5, 8, 0, 9 ]
        ];

        if(checkHankelMatrix(n, m))
            document.write("Yes");
        else
            document.write("No");

//this code is  contributed by mohan pavan pulamolu
</script>
```

**Output**

```
Yes
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*