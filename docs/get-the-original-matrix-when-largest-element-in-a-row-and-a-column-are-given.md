# 给定一行一列中最大的元素时求原始矩阵

> 原文:[https://www . geesforgeks . org/get-原始矩阵-当给定一行和一列中最大的元素时/](https://www.geeksforgeeks.org/get-the-original-matrix-when-largest-element-in-a-row-and-a-column-are-given/)

分别给定 **N** 和 **M** 整数的两个数组 **A[]** 和 **B[]** 。还给出了一个 **N X M** 二进制矩阵，其中 1 表示原矩阵中有一个正整数，0 表示原矩阵中该位置用 0 填充。任务是形成原始矩阵，使得 **A[i]** 表示第 **i <sup>第</sup>** 行中的最大元素， **B[j]** 表示第 **j <sup>第</sup>列中的最大元素。
**举例:**** 

```
Input: A[] = {2, 1, 3}, B[] = {2, 3, 0, 0, 2, 0, 1},
matrix[] = {{1, 0, 0, 0, 1, 0, 0},
            {0, 0, 0, 0, 0, 0, 1},
            {1, 1, 0, 0, 0, 0, 0}}

Output: 
2 0 0 0 2 0 0 
0 0 0 0 0 0 1 
2 3 0 0 0 0 0

Input: A[] = {2, 4}, B[] = {4, 2},
matrix[] = {{1, 1},
            {1, 1}}
Output:
2 2
4 2
```

**方法:**对矩阵中的每个指标 **(i，j)** 进行迭代，如果 **mat[i][j] == 1** ，则用 **min(A[i]，B[j])** 填充该位置。这是因为当前元素是第 **i <sup>第</sup>** 行和第 **j <sup>第</sup>** 列的一部分，如果选择了**最大值(A[i]，B[j])** ，则无法满足其中一个条件，即所选元素可能超过当前行或当前列所需的最大元素。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define N 3
#define M 7

// Function that prints the original matrix
void printOriginalMatrix(int a[], int b[], int mat[N][M])
{
    // Iterate in the row
    for (int i = 0; i < N; i++) {

        // Iterate in the column
        for (int j = 0; j < M; j++) {

            // If previously existed an element
            if (mat[i][j] == 1)
                cout << min(a[i], b[j]) << " ";
            else
                cout << 0 << " ";
        }
        cout << endl;
    }
}

// Driver code
int main()
{
    int a[] = { 2, 1, 3 };
    int b[] = { 2, 3, 0, 0, 2, 0, 1 };
    int mat[N][M] = { { 1, 0, 0, 0, 1, 0, 0 },
                      { 0, 0, 0, 0, 0, 0, 1 },
                      { 1, 1, 0, 0, 0, 0, 0 } };
    printOriginalMatrix(a, b, mat);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static int N = 3;
static int M = 7;

// Function that prints the original matrix
static void printOriginalMatrix(int a[], int b[],
                                int[][] mat)
{

    // Iterate in the row
    for (int i = 0; i < N; i++)
    {

        // Iterate in the column
        for (int j = 0; j < M; j++)
        {

            // If previously existed an element
            if (mat[i][j] == 1)
                System.out.print(Math.min(a[i],
                                          b[j]) + " ");
            else
                System.out.print("0" + " ");
        }
        System.out.println();
    }
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 2, 1, 3 };
    int b[] = { 2, 3, 0, 0, 2, 0, 1 };
    int[][] mat = {{ 1, 0, 0, 0, 1, 0, 0 },
                   { 0, 0, 0, 0, 0, 0, 1 },
                   { 1, 1, 0, 0, 0, 0, 0 }};
    printOriginalMatrix(a, b, mat);
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 implementation of the approach
N = 3
M = 7

# Function that prints the original matrix
def printOriginalMatrix(a, b, mat) :

    # Iterate in the row
    for i in range(N) :

        # Iterate in the column
        for j in range(M) :

            # If previously existed an element
            if (mat[i][j] == 1) :
                print(min(a[i], b[j]), end = " ");
            else :
                print(0, end = " ");

        print()

# Driver code
if __name__ == "__main__" :

    a = [ 2, 1, 3 ]
    b = [ 2, 3, 0, 0, 2, 0, 1 ]

    mat = [[ 1, 0, 0, 0, 1, 0, 0 ],
           [ 0, 0, 0, 0, 0, 0, 1 ],
           [ 1, 1, 0, 0, 0, 0, 0 ]];

    printOriginalMatrix(a, b, mat);

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int N = 3;
static int M = 7;

// Function that prints the original matrix
static void printOriginalMatrix(int[] a, int[] b,
                                int[,] mat)
{

    // Iterate in the row
    for (int i = 0; i < N; i++)
    {

        // Iterate in the column
        for (int j = 0; j < M; j++)
        {

            // If previously existed an element
            if (mat[i,j] == 1)
                Console.Write(Math.Min(a[i],
                                        b[j]) + " ");
            else
                Console.Write("0" + " ");
        }
        Console.WriteLine();
    }
}

// Driver code
public static void Main()
{
    int[] a = { 2, 1, 3 };
    int[] b = { 2, 3, 0, 0, 2, 0, 1 };
    int[,] mat = {{ 1, 0, 0, 0, 1, 0, 0 },
                { 0, 0, 0, 0, 0, 0, 1 },
                { 1, 1, 0, 0, 0, 0, 0 }};
    printOriginalMatrix(a, b, mat);
}
}

// This code is contributed by Code_Mech
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

$N = 3;
$M = 7;

// Function that prints the original matrix
function printOriginalMatrix($a, $b, $mat)
{
    // Iterate in the row
    for ($i = 0; $i < $GLOBALS['N']; $i++)
    {
        // Iterate in the column
        for ($j = 0; $j < $GLOBALS['M']; $j++)
        {

            // If previously existed an element
            if ($mat[$i][$j] == 1)
                echo min($a[$i], $b[$j])." ";
            else
                echo "0"." ";
        }
        echo "\r\n";
    }   
}

// Driver code

$a = array( 2, 1, 3 );
$b = array(2, 3, 0, 0, 2, 0, 1 );
$mat = array( array( 1, 0, 0, 0, 1, 0, 0 ),
                array( 0, 0, 0, 0, 0, 0, 1 ),
                array( 1, 1, 0, 0, 0, 0, 0 ));
printOriginalMatrix($a, $b, $mat);

// This code is contributed by Shashank_Sharma
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

let N = 3;
let M = 7;

// Function that prints the original matrix
function printOriginalMatrix(a,b,mat)
{

    // Iterate in the row
    for (let i = 0; i < N; i++)
    {

        // Iterate in the column
        for (let j = 0; j < M; j++)
        {

            // If previously existed an element
            if (mat[i][j] == 1)
                document.write(Math.min(a[i],
                                b[j]) + " ");
            else
                document.write("0" + " ");
        }
        document.write("<br>");
    }
}

// Driver code

    let a = [ 2, 1, 3 ];
    let b = [ 2, 3, 0, 0, 2, 0, 1 ];
    let mat = [[ 1, 0, 0, 0, 1, 0, 0 ],
               [ 0, 0, 0, 0, 0, 0, 1 ],
               [ 1, 1, 0, 0, 0, 0, 0 ]];

    printOriginalMatrix(a, b, mat);

// This code is contributed Bobby

</script>
```

**Output:** 

```
2 0 0 0 2 0 0 
0 0 0 0 0 0 1 
2 3 0 0 0 0 0
```