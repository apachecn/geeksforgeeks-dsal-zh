# 通过用平均值替换(I，j)和(j，I)处的元素，将给定矩阵转换为对称矩阵

> 原文:[https://www . geeksforgeeks . org/通过用它们的平均值替换元素 at-I-j-和-j-I-将给定矩阵转换为对称矩阵/](https://www.geeksforgeeks.org/convert-given-matrix-into-a-symmetric-matrix-by-replacing-elements-at-i-j-and-j-i-with-their-mean/)

给定一个整数 **N** 和一个 **N x N** 矩阵，任务是通过将 **(i，j) <sup>第</sup>** 和 **(j，i) <sup>第</sup>** 元素替换为它们的[算术平均值](https://www.geeksforgeeks.org/arithmetic-mean/)来将给定矩阵转换为[对称矩阵](https://www.geeksforgeeks.org/program-to-check-if-a-matrix-is-symmetric/)。

**示例:**

> **输入:** arr[] = {{1，2，3}，
> {4，5，6}，
> {7，8，9}}
> **输出:**
> 1 3 5
> 3 5 7
> 5 7 9
> **说明:**对角线元素相同。索引(0，1) = 2 和(1，0) = 4 处的元素被它们的算术平均值替换，即，(2 + 4) / 2 = 3。类似地，索引(2，0)和(0，2)、(2，1)和(1，2)处的元素也被它们的反对称均值所取代，并且得到的输出矩阵是对称矩阵。
> 
> **输入:** arr[] = {{12，43，65}，
> {23，75，13}，
> {51，37，81}}
> **输出:**
> 12 33 58
> 33 75 25
> 58 25 81

**方法:**给定的问题是基于实现的问题。其思想是[遍历下三角矩阵](https://www.geeksforgeeks.org/program-print-lower-triangular-upper-triangular-matrix-array/)，并用它们的[算术平均值](https://www.geeksforgeeks.org/arithmetic-mean/)替换元素及其各自的转置索引。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <iostream>
using namespace std;
const int N = 3;

// Function to convert the given matrix
// into a symmetric matrix by replacing
// transpose elements with their mean
void makeSymmetric(int mat[][N])
{
    // Loop to traverse lower triangular
    // elements of the given matrix
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            if (j < i) {
                mat[i][j] = mat[j][i]
                    = (mat[i][j] +
                       mat[j][i]) / 2;
            }
        }
    }
}

// Function to print the given matrix
void showMatrix(int mat[][N])
{
    // Loop to traverse the
    // given matrix
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {

            // Print current index
            cout << mat[i][j] << " ";
        }
        cout << "\n";
    }
}

// Driver Code
int main()
{
    int arr[][N]
        = { { 12, 43, 65 },
            { 23, 75, 13 },
            { 51, 37, 81 } };

    makeSymmetric(arr);
    showMatrix(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.util.*;

class GFG{

static int N = 3;

// Function to convert the given matrix
// into a symmetric matrix by replacing
// transpose elements with their mean
static void makeSymmetric(int mat[][])
{

    // Loop to traverse lower triangular
    // elements of the given matrix
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < N; j++)
        {
            if (j < i)
            {
                mat[i][j] = mat[j][i] = (mat[i][j] +
                                         mat[j][i]) / 2;
            }
        }
    }
}

// Function to print the given matrix
static void showMatrix(int mat[][])
{

    // Loop to traverse the
    // given matrix
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < N; j++)
        {

            // Print current index
            System.out.print(mat[i][j] + " ");
        }
        System.out.println();
    }
}

// Driver Code
public static void main(String args[])
{
    int arr[][] = { { 12, 43, 65 },
                    { 23, 75, 13 },
                    { 51, 37, 81 } };

    makeSymmetric(arr);
    showMatrix(arr);
}
}

// This code is contributed by sanjoy_62
```

**Output**

```
12 33 58 
33 75 25 
58 25 81 
```

***时间复杂度:**O(N<sup>2</sup>)*
***空间复杂度:** O(1)*