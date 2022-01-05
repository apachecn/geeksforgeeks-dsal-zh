# 顺时针旋转矩阵 90 度，不使用任何额外空间|设置 3

> 原文:[https://www . geesforgeks . org/rotate-a-matrix-顺时针旋转 90 度，不使用任何额外空间-set-3/](https://www.geeksforgeeks.org/rotate-a-matrix-clockwise-by-90-degree-without-using-any-extra-space-set-3/)

给定一个具有 **N** 行和 **M** 列的[矩形矩阵](https://www.geeksforgeeks.org/maximum-sum-rectangle-in-a-2d-matrix-dp-27/) **mat[][]** ，任务是在不使用额外空间的情况下将矩阵顺时针旋转 90 度。

**示例:**

> **输入:** mat[][] = {{1，2，3}，{4，5，6}，{7，8，9}，{10，11，12}}
> **输出:** 10 7 4 1
> 11 8 5 2
> 12 9 6 3
> 
> **输入:** mat[][] = {{1，2，3，4，5，6}，{7，8，9，10，11，12}}
> **输出:**7 1
> 8 2
> 9 3
> 10 4
> 11 5
> 12 6

**注:**旋转正方形矩阵的方法已经讨论如下:

*   有额外空间:[原地旋转正方形矩阵 90 度|设置 1](https://www.geeksforgeeks.org/inplace-rotate-square-matrix-by-90-degrees/)
*   逆时针方向无多余空间:[不使用任何多余空间将矩阵旋转 90 度|设置 2](https://www.geeksforgeeks.org/rotate-a-matrix-by-90-degree-in-clockwise-direction-without-using-any-extra-space/)

**进场:**主要思路是进行原地旋转。

按照以下步骤解决给定的问题:

1.  沿着主对角线，即从右上角到右下角，交换子矩阵 **min(N，M)** * **min(N，M)** 的所有元素。
2.  如果 **N** 大于 **M** ，
    *   将每列 I 中 **(min(N，M) ≤ i)** 处的所有未平移元素推到 i <sup>第</sup>行。
    *   否则，将每一行 I 中 **(min(N，M) ≤ i)** 处的所有未展开元素推到 i <sup>第</sup>列。
3.  [反转矩阵的每一行](https://www.geeksforgeeks.org/program-to-reverse-the-rows-in-a-2d-array/)
4.  [打印更新后的维度矩阵 **M × N** 。](https://www.geeksforgeeks.org/program-to-find-the-sum-of-each-row-and-each-column-of-a-matrix/)

**程序:**

**给定矩阵为:**
1 2 3
4 5 6
7 8 9
10 11 12
13 14 15
**交换子矩阵 min(N，M) * min(N，M)的所有元素，即本例中的 3 * 3**
1 4 7
2 5 8
3 6 9
10 11 12
13 14

**从 N > M 开始，将每一列 i (min(N，M) ≤ i)的所有未平移元素推到 i <sup>第</sup>行**T4】1 4 7 10 13
2 5 8 11 14
3 6 9 12 15

**反转每一列得到最终的旋转矩阵为:**
13 10 7 4 1
14 11 8 5 2
15 12 9 6 3

下面是上述方法的实现:

## C++

```
// C++ program for
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the matrix mat
// with N rows and M columns
void print(vector<vector<int> > mat,
           int N, int M)
{
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            cout << mat[i][j] << " ";
        }

        cout << "\n";
    }
}

// Function to rotate the matrix
// by 90 degree clockwise
void rotate(vector<vector<int> > mat)
{
    // Number of rows
    int N = mat.size();

    // Number of columns
    int M = mat[0].size();

    // Swap all the elements along main diagonal
    // in the submatrix min(N, M) * min(N, M)
    for (int i = 0; i < min(N, M); i++) {
        for (int j = i; j < min(N, M); j++) {

            // Swap mat[i][j] and mat[j][i]
            swap(mat[i][j], mat[j][i]);
        }
    }

    // If N is greater than M
    if (N > M) {

        // Push all the unswapped elements
        // of ith column to ith row
        for (int i = 0; i < M; i++) {
            for (int j = min(N, M); j < N; j++) {
                mat[i].push_back(mat[j][i]);
            }
        }
    }
    else {
        // Resize mat to have M rows
        mat.resize(M, {});

        // Push all the unswapped elements
        // of ith column to ith row
        for (int i = min(N, M); i < M; i++) {
            for (int j = 0; j < N; j++) {
                mat[i].push_back(mat[j][i]);
            }
        }
    }

    // Reverse each row of the matrix
    for (int i = 0; i < M; i++) {
        reverse(mat[i].begin(), mat[i].end());
    }

    // Print the final matrix
    print(mat, M, N);
}

// Driver Code
int main()
{
    // Input
    vector<vector<int> > mat = { { 1, 2, 3 },
                                 { 4, 5, 6 },
                                 { 7, 8, 9 },
                                 { 10, 11, 12 } };

    // Function Call
    rotate(mat);

    return 0;
}
```

**Output**

```
10 7 4 1 
11 8 5 2 
12 9 6 3 
```

***时间复杂度:** O(N * M)*
***辅助空间:** O(1)*