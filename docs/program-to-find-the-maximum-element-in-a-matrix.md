# 计算矩阵中最大元素的程序

> 原文:[https://www . geesforgeks . org/program-to-find-matrix 中的最大元素/](https://www.geeksforgeeks.org/program-to-find-the-maximum-element-in-a-matrix/)

给定 NxM 矩阵。任务是找到这个矩阵中的最大元素。
**例** :

```
Input: mat[4][4] = {{1, 2, 3, 4},
                    {25, 6, 7, 8},
                    {9, 10, 11, 12},
                    {13, 14, 15, 16}};
Output: 25

Input: mat[3][4] = {{9, 8, 7, 6},
                    {5, 4, 3, 2},
                    {1, 0, 12, 45}};
Output: 45
```

**方法:**想法是使用两个嵌套循环遍历矩阵，一个用于行，一个用于列，并找到最大元素。用最小值初始化一个变量 maxElement，遍历矩阵，如果当前元素大于 maxElement，则每次进行比较。如果是，那么用当前元素更新 maxElement。
以下是上述办法的实施情况:

## C++

```
// CPP code to find max element in a matrix
#include <bits/stdc++.h>
using namespace std;

#define N 4
#define M 4

// Function to find max element
// mat[][] : 2D array to find max element
int findMax(int mat[N][M])
{

    // Initializing max element as INT_MIN
    int maxElement = INT_MIN;

    // checking each element of matrix
    // if it is greater than maxElement,
    // update maxElement
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            if (mat[i][j] > maxElement) {
                maxElement = mat[i][j];
            }
        }
    }

    // finally return maxElement
    return maxElement;
}

// Driver code
int main()
{

    // matrix
    int mat[N][M] = { { 1, 2, 3, 4 },
                      { 25, 6, 7, 8 },
                      { 9, 10, 11, 12 },
                      { 13, 14, 15, 16 } };

    cout << findMax(mat) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find max element in a matrix

public class GFG {

    final static int N = 4;
    final static int  M = 4 ;

    // Function to find max element
    // mat[][] : 2D array to find max element
    static int findMax(int mat[][])
    {

        // Initializing max element as INT_MIN
        int maxElement = Integer.MIN_VALUE;

        // checking each element of matrix
        // if it is greater than maxElement,
        // update maxElement
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                if (mat[i][j] > maxElement) {
                    maxElement = mat[i][j];
                }
            }
        }

        // finally return maxElement
        return maxElement;
    }

    // Driver code
    public static void main(String args[])
    {
           // matrix
        int mat[][] = { { 1, 2, 3, 4 },
                          { 25, 6, 7, 8 },
                          { 9, 10, 11, 12 },
                          { 13, 14, 15, 16 } };

        System.out.println(findMax(mat)) ;

    }
    // This Code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python 3 code to find max element
# in a matrix
import sys
N = 4
M = 4

# Function to find max element
# mat[][] : 2D array to find max element
def findMax(mat):

    # Initializing max element as INT_MIN
    maxElement = -sys.maxsize - 1

    # checking each element of matrix
    # if it is greater than maxElement,
    # update maxElement
    for i in range(N):
        for j in range(M):
            if (mat[i][j] > maxElement):
                maxElement = mat[i][j]

    # finally return maxElement
    return maxElement

# Driver code
if __name__ == '__main__':

    # matrix
    mat = [[1, 2, 3, 4],
           [25, 6, 7, 8],
           [9, 10, 11, 12],
           [13, 14, 15, 16]]
    print(findMax(mat))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# code to find max element in a matrix
using System;

class GFG {

    static int N = 4;
    static int M = 4 ;

    // Function to find max element
    // mat[,] : 2D array to find max element
    static int findMax(int[,] mat)
    {

        // Initializing max element as INT_MIN
        int maxElement = int.MinValue;

        // checking each element of matrix
        // if it is greater than maxElement,
        // update maxElement
        for (int i = 0; i < N; i++) {

            for (int j = 0; j < M; j++) {

                if (mat[i,j] > maxElement) {

                    maxElement = mat[i,j];
                }
            }
        }

        // finally return maxElement
        return maxElement;
    }

    // Driver code
    public static void Main()
    {

        // matrix
        int[,]mat = {{ 1, 2, 3, 4},
                     {25, 6, 7, 8},
                     {9, 10, 11, 12},
                     {13, 14, 15, 16}};

        Console.Write(findMax(mat)) ;
    }

}

// This code is contributed by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find max element in a matrix

// Function to find max element
// mat[][] : 2D array to find max element
function findMax($mat)
{

    // Initializing max element as INT_MIN
    $maxElement = PHP_INT_MIN;

    // checking each element of matrix
    // if it is greater than maxElement,
    // update maxElement
    for ($i = 0; $i < 4; $i++)
    {
        for ($j = 0; $j < 4; $j++)
        {
            if ($mat[$i][$j] > $maxElement)
            {
                $maxElement = $mat[$i][$j];
            }
        }
    }

    // finally return maxElement
    return $maxElement;
}

// Driver code
$mat = array(array(1, 2, 3, 4),
             array(25, 6, 7, 8),
             array(9, 10, 11, 12),
             array(13, 14, 15, 16));

echo findMax($mat) . "\n";

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// Java script code to find max element in a matrix

let N = 4;
    let M = 4 ;

    // Function to find max element
    // mat[][] : 2D array to find max element
    function findMax(mat)
    {

        // Initializing max element as INT_MIN
        let maxElement = Number.MIN_VALUE;

        // checking each element of matrix
        // if it is greater than maxElement,
        // update maxElement
        for (let i = 0; i < N; i++) {
            for (let j = 0; j < M; j++) {
                if (mat[i][j] > maxElement) {
                    maxElement = mat[i][j];
                }
            }
        }

        // finally return maxElement
        return maxElement;
    }

    // Driver code

        // matrix
        let mat = [[ 1, 2, 3, 4 ],
                        [ 25, 6, 7, 8 ],
                        [ 9, 10, 11, 12 ],
                        [ 13, 14, 15, 16 ]];

        document.write(findMax(mat)) ;

// This code is contributed by manoj
</script>
```

**Output:** 

```
25
```

**时间复杂度** : O(N*M)