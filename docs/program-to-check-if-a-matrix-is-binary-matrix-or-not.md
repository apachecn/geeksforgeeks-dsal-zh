# 检查矩阵是否为二进制矩阵的程序

> 原文:[https://www . geesforgeks . org/program-to-check-if-a-matrix-is-binary-matrix-or-not/](https://www.geeksforgeeks.org/program-to-check-if-a-matrix-is-binary-matrix-or-not/)

给定一个矩阵，任务是检查该矩阵是否是**二进制矩阵**。二进制矩阵是所有元素要么是 **0 要么是 1 的矩阵。**又称**逻辑矩阵、布尔矩阵、关系矩阵。**
**例:**

```
Input: 
{{1, 0, 1, 1},
{0, 1, 0, 1}
{1, 1, 1, 0}}
Output: Yes

Input:
{{1, 0, 1, 1},
{1, 2, 0, 1},
{0, 0, 1, 1}}
Output: No
```

**方法:**遍历矩阵，检查每个元素是 0 还是 1。如果有除 0 和 1 之外的任何元素，则打印否，否则打印是。
**以下是上述方法的实施:**

## C++

```
// C++ code to check if a matrix
// is binary matrix or not.
#include <bits/stdc++.h>
using namespace std;

#define M 3
#define N 4

// function to check if a matrix
// is binary matrix or not
bool isBinaryMatrix(int mat[][N])
{
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++) {
            // Returns false if element is other than 0 or 1.
            if (!(mat[i][j] == 0 || mat[i][j] == 1))
                return false;
        }
    }

    // Returns true if all the elements
    // are either 0 or 1.
    return true;
}

// Driver code
int main()
{
    int mat[M][N] = { { 1, 0, 1, 1 },
                      { 0, 1, 0, 1 },
                      { 1, 1, 1, 0 } };

    if (isBinaryMatrix(mat))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA code to check if a matrix
// is binary matrix or not.

import java.io.*;
class GFG {
    static int M = 3;
    static int N = 4;

    // function to check if a matrix is binary matrix
    // or not
    static boolean isBinaryMatrix(int mat[][])
    {
        for (int i = 0; i < M; i++) {
            for (int j = 0; j < N; j++) {
                // Returns false if element is other than 0 or 1.
                if (!(mat[i][j] == 0 || mat[i][j] == 1))
                    return false;
            }
        }

        // Returns true if all the elements
        // are either 0 or 1.
        return true;
    }

    // Driver code
    public static void main(String args[])
    {
        int mat[][] = { { 1, 0, 1, 1 },
                        { 0, 1, 0, 1 },
                        { 1, 1, 1, 0 } };

        if (isBinaryMatrix(mat))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# Python3 code to check if a matrix
# is binary matrix or not.

M = 3;
N = 4;

# function to check if a matrix
# is binary matrix or not
def isBinaryMatrix(mat):
    for i in range(M):
        for j in range(N):
            # Returns false if element
            # is other than 0 or 1.
            if ((mat[i][j] == 0 or mat[i][j] == 1)==False):
                return False;

    # Returns true if all the
    # elements are either 0 or 1.
    return True;

# Driver code
if __name__=='__main__':
    mat = [[ 1, 0, 1, 1 ],[0, 1, 0, 1 ],[ 1, 1, 1, 0 ]];

    if (isBinaryMatrix(mat)):
        print("Yes");
    else:
        print("No");

# This code is contributed by mits
```

## C#

```
// C# code to check if a matrix
// is binary matrix or not.

using System;
class GFG {
    static int M = 3;
    static int N = 4;

    // function to check if a matrix is binary matrix
    // or not
    static bool isBinaryMatrix(int [,]mat)
    {
        for (int i = 0; i < M; i++) {
            for (int j = 0; j < N; j++) {
                // Returns false if element is other than 0 or 1.
                if (!(mat[i,j] == 0 || mat[i,j] == 1))
                    return false;
            }
        }

        // Returns true if all the elements
        // are either 0 or 1.
        return true;
    }

    // Driver code
    public static void Main()
    {
        int [,]mat = { { 1, 0, 1, 1 },
                        { 0, 1, 0, 1 },
                        { 1, 1, 1, 0 } };

        if (isBinaryMatrix(mat))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}
// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to check if a matrix
// is binary matrix or not.

$M = 3;
$N = 4;

// function to check if a matrix
// is binary matrix or not
function isBinaryMatrix($mat)
{
    global $M, $N;
    for ($i = 0; $i < $M; $i++)
    {
        for ($j = 0; $j < $N; $j++)
        {
            // Returns false if element
            // is other than 0 or 1.
            if (!($mat[$i][$j] == 0 ||
                  $mat[$i][$j] == 1))
                return false;
        }
    }

    // Returns true if all the
    // elements are either 0 or 1.
    return true;
}

// Driver code
$mat = array(array( 1, 0, 1, 1 ),
             array( 0, 1, 0, 1 ),
             array( 1, 1, 1, 0 ));

if (isBinaryMatrix($mat))
    echo "Yes";
else
    echo "No";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JAVA SCRIPT  code to check if a matrix
// is binary matrix or not.

    let M = 3;
   let N = 4;

    // function to check if a matrix is binary matrix
    // or not
    function isBinaryMatrix(mat)
    {
        for (let i = 0; i < M; i++) {
            for (let j = 0; j < N; j++) {
                // Returns false if element is other than 0 or 1.
                if (!(mat[i][j] == 0 || mat[i][j] == 1))
                    return false;
            }
        }

        // Returns true if all the elements
        // are either 0 or 1.
        return true;
    }

    // Driver code
    let mat = [[ 1, 0, 1, 1 ],
                        [ 0, 1, 0, 1 ],
                        [ 1, 1, 1, 0 ]];

        if (isBinaryMatrix(mat))
            document.write("Yes");
        else
            document.write("No");

// this code is  contributed by mohan pavan pulamolu
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:**O(M X N)
T3】空间复杂度: O(1)