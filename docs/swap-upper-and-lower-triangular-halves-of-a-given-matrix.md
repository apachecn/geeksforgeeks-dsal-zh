# 交换给定矩阵的上下三角形部分

> 原文:[https://www . geesforgeks . org/swap-给定矩阵的上半部分和下半部分三角形/](https://www.geeksforgeeks.org/swap-upper-and-lower-triangular-halves-of-a-given-matrix/)

给定尺寸为 **N * N** 的正方形[矩阵](https://www.geeksforgeeks.org/matrix/) **mat[][]** ，任务是打印在交换给定矩阵的上下三角形半部分的横向反转图像后可以获得的矩阵。

> 考虑矩阵 mat[][] = {{1，2，3}，{4，5，6}，{7，8，9}}
> 矩阵下三角半部分的横向图像
> 
> ```
> 4
> 7 8
> ```
> 
> 矩阵上三角形一半的横向图像
> 
> ```
>  6
>  3 2
> ```
> 
> 因此，需要执行以下矩阵重排
> 
> ```
> 1  2  3    1  8  7
> 4  5  6 to 6  5  4
> 7  8  9    3  2  9
> ```

**示例:**

> **输入:** mat[][] = {{1，2，3}，{4，5，6}，{7，8，9}}
> **输出:**
> 1 8 7
> 6 5 4
> 3 2 9
> **解释:**
> 
> ```
> 1  2  3    6  5  4
> 1  8  7 to 7  8  9
> 4  5  6    3  2  9
> ```
> 
> **输入:** mat[][] = {{1，2}，{4，5 } }
> T3】输出:T5】1 4
> 2 5

**方法:**按照以下步骤解决问题:

*   初始化向量的[数组](https://www.geeksforgeeks.org/array-of-vectors-in-c-stl/)、**上对角**和**下对角**，分别存储下半部分和上半部分的矩阵元素。
*   [使用变量 **i** 和 **j** 分别遍历给定矩阵](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)的行和列，并执行以下步骤:
    *   如果当前元素在主对角线上，则[从该迭代继续](https://www.geeksforgeeks.org/decision-making-c-c-else-nested-else/)。
    *   否则，如果当前元素出现在上半个三角形中，则在索引**ABS(I–j)**处将该元素添加到**向上倾斜**中。
    *   否则，将当前元素添加到索引**ABS(I–j)**处的**低对角线**中。
*   现在，再次[遍历矩阵](https://www.geeksforgeeks.org/traverse-a-given-matrix-using-recursion/)并用来自**下半部分**末端的元素替换存在于**上半部分**中的任何元素，反之亦然。
*   完成上述步骤后，打印结果矩阵。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to swap laterally inverted
// images of upper and lower triangular
// halves of a given matrix
void ReverseSwap(vector<vector<int> >& mat, int n)
{
    // Store the matrix elements from
    // upper & lower triangular halves
    vector<int> lowerEle[n];
    vector<int> upperEle[n];

    int index;

    // Traverse the matrix mat[][]
    for (int i = 0; i < n; i++) {

        for (int j = 0; j < n; j++) {

            // Find the index
            index = abs(i - j);

            // If current element lies
            // on the principal diagonal
            if (i == j) {
                continue;
            }

            // If current element lies
            // below the principal diagonal
            else if (j < i) {
                lowerEle[index].push_back(
                    mat[i][j]);
            }

            // If current element lies
            // above the principal diagonal
            else {
                upperEle[index].push_back(
                    mat[i][j]);
            }
        }
    }

    // Traverse again to swap values
    for (int i = 0; i < n; i++) {

        for (int j = 0; j < n; j++) {

            // Find the index
            index = abs(i - j);

            // Principal diagonal
            if (i == j) {
                continue;
            }

            // Below main diagonal
            else if (j < i) {

                mat[i][j] = upperEle[index].back();
                upperEle[index].pop_back();
            }

            // Above main diagonal
            else {
                mat[i][j] = lowerEle[index].back();
                lowerEle[index].pop_back();
            }
        }
    }

    // Traverse the matrix and print
    for (int i = 0; i < n; i++) {

        for (int j = 0; j < n; j++) {

            cout << mat[i][j] << " ";
        }
        cout << endl;
    }
}

// Driver Code
int main()
{
    // Given Matrix mat[][]
    vector<vector<int> > mat = { { 1, 2 },
                                 { 4, 5 } };

    int N = mat.size();

    // Swap the upper and lower
    // triangular halves
    ReverseSwap(mat, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to swap laterally inverted
// images of upper and lower triangular
// halves of a given matrix
static void ReverseSwap(int[][] mat, int n)
{

    // Store the matrix elements from
    // upper & lower triangular halves
    int[] lowerEle = new int[n];
    int[] upperEle = new int[n];

    int index;

    // Traverse the matrix mat[][]
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {

            // Find the index
            index = Math.abs(i - j);

            // If current element lies
            // on the principal diagonal
            if (i == j)
            {
                continue;
            }

            // If current element lies
            // below the principal diagonal
            else if (j < i)
            {
                lowerEle[index] = mat[i][j];
            }

            // If current element lies
            // above the principal diagonal
            else
            {
                upperEle[index] = mat[i][j];
            }
        }
    }

    // Traverse again to swap values
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {

            // Find the index
            index = Math.abs(i - j);

            // Principal diagonal
            if (i == j)
            {
                continue;
            }

            // Below main diagonal
            else if (j < i)
            {
                mat[i][j] = upperEle[index];
            }

            // Above main diagonal
            else
            {
                mat[i][j] = lowerEle[index--];
            }
        }
    }

    // Traverse the matrix and print
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {
            System.out.print(mat[i][j] + " ");
        }
        System.out.println();
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given Matrix mat[][]
    int[][] mat = new int[][]{ { 1, 2 }, { 4, 5 } };

    int N = mat.length;

    // Swap the upper and lower
    // triangular halves
    ReverseSwap(mat, N);
}
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to swap laterally inverted
# images of upper and lower triangular
# halves of a given matrix
def ReverseSwap(mat, n):

    # Store the matrix elements from
    # upper & lower triangular halves
    lowerEle = [[] for i in range(n)]
    upperEle = [[] for i in range(n)]

    index = 0

    # Traverse the matrix mat[][]
    for i in range(n):
        for j in range(n):

            # Find the index
            index = abs(i - j)

            # If current element lies
            # on the principal diagonal
            if (i == j):
                continue

            # If current element lies
            # below the principal diagonal
            elif (j < i):
                lowerEle[index].append(mat[i][j])

            # If current element lies
            # above the principal diagonal
            else:
                upperEle[index].append(mat[i][j])

    # Traverse again to swap values
    for i in range(n):
        for j in range(n):

            # Find the index
            index = abs(i - j)

            # Principal diagonal
            if (i == j):
                continue

            # Below main diagonal
            elif (j < i):
                mat[i][j] = upperEle[index][-1]
                del upperEle[index][-1]

            # Above main diagonal
            else:
                mat[i][j] = lowerEle[index][-1]
                del lowerEle[index][-1]

    # Traverse the matrix and pr
    for i in range(n):
        for j in range(n):
            print (mat[i][j], end = " ")

        print()

# Driver Code
if __name__ == '__main__':

    # Given Matrix mat[][]
    mat = [ [ 1, 2 ],
            [ 4, 5 ] ]

    N = len(mat)

    # Swap the upper and lower
    # triangular halves
    ReverseSwap(mat, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to swap laterally inverted
// images of upper and lower triangular
// halves of a given matrix
static void ReverseSwap(int[,] mat, int n)
{

    // Store the matrix elements from
    // upper & lower triangular halves
    int[] lowerEle = new int[n];
    int[] upperEle = new int[n];

    int index;

    // Traverse the matrix mat[][]
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {

            // Find the index
            index = Math.Abs(i - j);

            // If current element lies
            // on the principal diagonal
            if (i == j)
            {
                continue;
            }

            // If current element lies
            // below the principal diagonal
            else if (j < i)
            {
                lowerEle[index] = mat[i, j];
            }

            // If current element lies
            // above the principal diagonal
            else
            {
                upperEle[index] = mat[i, j];
            }
        }
    }

    // Traverse again to swap values
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {

            // Find the index
            index = Math.Abs(i - j);

            // Principal diagonal
            if (i == j)
            {
                continue;
            }

            // Below main diagonal
            else if (j < i)
            {
                mat[i, j] = upperEle[index];
            }

            // Above main diagonal
            else
            {
                mat[i, j] = lowerEle[index--];
            }
        }
    }

    // Traverse the matrix and print
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {
            Console.Write(mat[i, j] + " ");
        }
        Console.WriteLine();
    }
}

// Driver Code
static public void Main()
{

    // Given Matrix mat[][]
    int[,] mat = new int[,]{ { 1, 2 }, { 4, 5 } };

    int N = mat.GetLength(0);

    // Swap the upper and lower
    // triangular halves
    ReverseSwap(mat, N);
}
}

// This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to swap laterally inverted
// images of upper and lower triangular
// halves of a given matrix
function  ReverseSwap(mat,n)
{
    // Store the matrix elements from
    // upper & lower triangular halves
    let lowerEle = new Array(n);
    let upperEle = new Array(n);

    let index;

    // Traverse the matrix mat[][]
    for(let i = 0; i < n; i++)
    {
        for(let j = 0; j < n; j++)
        {

            // Find the index
            index = Math.abs(i - j);

            // If current element lies
            // on the principal diagonal
            if (i == j)
            {
                continue;
            }

            // If current element lies
            // below the principal diagonal
            else if (j < i)
            {
                lowerEle[index] = mat[i][j];
            }

            // If current element lies
            // above the principal diagonal
            else
            {
                upperEle[index] = mat[i][j];
            }
        }
    }

    // Traverse again to swap values
    for(let i = 0; i < n; i++)
    {
        for(let j = 0; j < n; j++)
        {

            // Find the index
            index = Math.abs(i - j);

            // Principal diagonal
            if (i == j)
            {
                continue;
            }

            // Below main diagonal
            else if (j < i)
            {
                mat[i][j] = upperEle[index];
            }

            // Above main diagonal
            else
            {
                mat[i][j] = lowerEle[index--];
            }
        }
    }

    // Traverse the matrix and print
    for(let i = 0; i < n; i++)
    {
        for(let j = 0; j < n; j++)
        {
            document.write(mat[i][j] + " ");
        }
        document.write("<br>");
    }
}

// Driver Code

let mat=[[1, 2],[ 4, 5 ]];
let N = mat.length;
// Swap the upper and lower
// triangular halves
ReverseSwap(mat, N);

// This code is contributed by patel2127

</script>
```

**Output:** 

```
1 4 
2 5
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*