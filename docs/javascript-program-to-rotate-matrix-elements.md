# 旋转矩阵元素的 Javascript 程序

> 原文:[https://www . geesforgeks . org/JavaScript-程序旋转矩阵元素/](https://www.geeksforgeeks.org/javascript-program-to-rotate-matrix-elements/)

给定一个矩阵，顺时针旋转其中的元素。

**示例:**

```
Input
1    2    3
4    5    6
7    8    9

Output:
4    1    2
7    5    3
8    9    6

For 4*4 matrix
Input:
1    2    3    4    
5    6    7    8
9    10   11   12
13   14   15   16

Output:
5    1    2    3
9    10   6    4
13   11   7    8
14   15   16   12
```

这个想法是使用类似于[程序的循环来打印螺旋形式的矩阵](https://www.geeksforgeeks.org/print-a-given-matrix-in-spiral-form/)。一个接一个地旋转元素的所有环，从最外面开始。要旋转环，我们需要执行以下操作。
1)移动顶行的元素。
2)移动最后一列的元素。
3)移动最下面一行的元素。
4)移动第一列的元素。
有内圈时，对内圈重复上述步骤。

以下是上述想法的实现。感谢 Gaurav Ahirwar 提出以下解决方案。

## java 描述语言

```
<script>

// Javascript program to rotate a matrix    

let R = 4;
let C = 4;

// A function to rotate a matrix 
// mat[][] of size R x C.
// Initially, m = R and n = C
function rotatematrix(m, n, mat)
{
    let row = 0, col = 0;
    let prev, curr;

    /*
    row - Staring row index
    m - ending row index
    col - starting column index
    n - ending column index
    i - iterator
    */
    while (row < m && col < n)
    {
        if (row + 1 == m || col + 1 == n)
            break;

        // Store the first element of next
        // row, this element will replace 
        // first element of current row
        prev = mat[row + 1][col];

        // Move elements of first row 
        // from the remaining rows 
        for(let i = col; i < n; i++)
        {
            curr = mat[row][i];
            mat[row][i] = prev;
            prev = curr;
        }
        row++;

        // Move elements of last column
        // from the remaining columns 
        for(let i = row; i < m; i++)
        {
            curr = mat[i][n - 1];
            mat[i][n - 1] = prev;
            prev = curr;
        }
        n--;

        // Move elements of last row 
        // from the remaining rows 
        if (row < m)
        {
            for(let i = n - 1; i >= col; i--)
            {
                curr = mat[m - 1][i];
                mat[m - 1][i] = prev;
                prev = curr;
            }
        }
        m--;

        // Move elements of first column
        // from the remaining rows 
        if (col < n)
        {
            for(let i = m - 1; i >= row; i--)
            {
                curr = mat[i][col];
                mat[i][col] = prev;
                prev = curr;
            }
        }
        col++;
    }

    // Print rotated matrix
    for(let i = 0; i < R; i++)
    {
        for(let j = 0; j < C; j++)
            document.write( mat[i][j] + " ");

        document.write("<br>");
    }
}

// Driver code

// Test Case 1
let a = [ [ 1, 2, 3, 4 ],
          [ 5, 6, 7, 8 ],
          [ 9, 10, 11, 12 ],
          [ 13, 14, 15, 16 ] ];

rotatematrix(R, C, a);

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
5 1 2 3
9 10 6 4
13 11 7 8
14 15 16 12
```

更多详情请参考[旋转矩阵元素](https://www.geeksforgeeks.org/rotate-matrix-elements/)整篇文章！