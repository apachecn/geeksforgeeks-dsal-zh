# Python3 编程将正方形矩阵旋转 90 度|设置 1

> 原文:[https://www . geesforgeks . org/python 3-程序到位置-旋转-90 度方形矩阵-set-1/](https://www.geeksforgeeks.org/python3-program-to-inplace-rotate-square-matrix-by-90-degrees-set-1/)

给定一个正方形矩阵，在不使用任何额外空间的情况下，将其逆时针旋转 90 度。
**例:**

```
Input:
Matrix:
 1  2  3
 4  5  6
 7  8  9
Output:
 3  6  9 
 2  5  8 
 1  4  7 
The given matrix is rotated by 90 degree 
in anti-clockwise direction.

Input:
 1  2  3  4 
 5  6  7  8 
 9 10 11 12 
13 14 15 16 
Output:
 4  8 12 16 
 3  7 11 15 
 2  6 10 14 
 1  5  9 13
The given matrix is rotated by 90 degree 
in anti-clockwise direction.
```

需要额外空间的方法已经在这里讨论过[](https://www.geeksforgeeks.org/turn-an-image-by-90-degree/)**。
**方法:**要在没有任何额外空间的情况下解决问题，请以正方形的形式旋转数组，将矩阵分成正方形或圆形。*例如*
一个 4 X 4 的矩阵会有 2 个循环。第一个周期由第一行、最后一列、最后一行和第一列组成。第二周期由第二行、倒数第二列、倒数第二行和第二列构成。其思想是，对于每个正方形循环，以逆时针方向，即从上到下、从左到下、从下到右和从右到上一次交换与矩阵中相应单元格相关的元素，只使用一个临时变量来实现这一点。
**演示:**** 

```
**First Cycle (Involves Red Elements)**
 1  2  3 4 
 5  6  7 8 
 9 10 11 12 
 13 14 15 16 

Moving first group of four elements (First
elements of 1st row, last row, 1st column 
and last column) of first cycle in counter
clockwise. 
 4  2  3 16
 5  6  7 8 
 9 10 11 12 
 1 14  15 13 

Moving next group of four elements of 
first cycle in counter clockwise 
 4  8  3 16 
 5  6  7  15  
 2  10 11 12 
 1  14  9 13 

Moving final group of four elements of 
first cycle in counter clockwise 
 4  8 12 16 
 3  6  7 15 
 2 10 11 14 
 1  5  9 13 

**Second Cycle (Involves Blue Elements)**
 4  8 12 16 
 3  6 7  15 
 2  10 11 14 
 1  5  9 13 

Fixing second cycle
 4  8 12 16 
 3  7 11 15 
 2  6 10 14 
 1  5  9 13
```

****算法:**** 

1.  **N 边的矩阵中有 N/2 个正方形或圈，一次处理一个正方形。一次运行一个循环遍历矩阵一个循环，即从 0 到 N/2–1 的循环，循环计数器为 *i***
2.  **考虑当前正方形中 4 个元素的组，一次旋转 4 个元素。所以一个周期中这样的群的数量是 N–2 * I**
3.  **所以在从 x 到 N–x–1 的每个循环中运行一个循环，循环计数器为 *y***
4.  **当前组中的元素是(x，y)，(y，N-1-x)，(N-1-x，N-1-y)，(N-1-y，x)，现在旋转这 4 个元素，即(x，y)打印矩阵。->**

## **蟒蛇 3**

```
# Python3 program to rotate a matrix by 90 degrees
N = 4

# An Inplace function to rotate 
# N x N matrix by 90 degrees in
# anti-clockwise direction
def rotateMatrix(mat):

    # Consider all squares one by one
    for x in range(0, int(N / 2)):

        # Consider elements in group   
        # of 4 in current square
        for y in range(x, N-x-1):

            # store current cell in temp variable
            temp = mat[x][y]

            # move values from right to top
            mat[x][y] = mat[y][N-1-x]

            # move values from bottom to right
            mat[y][N-1-x] = mat[N-1-x][N-1-y]

            # move values from left to bottom
            mat[N-1-x][N-1-y] = mat[N-1-y][x]

            # assign temp to left
            mat[N-1-y][x] = temp

# Function to print the matrix
def displayMatrix( mat ):

    for i in range(0, N):

        for j in range(0, N):

            print (mat[i][j], end = ' ')
        print ("")

# Driver Code
mat = [[0 for x in range(N)] for y in range(N)]

# Test case 1
mat = [ [1, 2, 3, 4 ],
        [5, 6, 7, 8 ],
        [9, 10, 11, 12 ],
        [13, 14, 15, 16 ] ]

'''
# Test case 2
mat = [ [1, 2, 3 ],
        [4, 5, 6 ],
        [7, 8, 9 ] ]

# Test case 3
mat = [ [1, 2 ],
        [4, 5 ] ]

'''

rotateMatrix(mat)

# Print rotated matrix
displayMatrix(mat)

# This code is contributed by saloni1297
```

****输出:**** 

```
 4  8 12 16 
 3  7 11 15 
 2  6 10 14 
 1  5  9 13 
```

****复杂度分析:**** 

*   ****时间复杂度:** O(n*n)，其中 n 为数组的边。
    需要矩阵的单次遍历。**
*   ****空间复杂度:** O(1)。
    因为需要一个恒定的空间**

**更多详情请参考[原地旋转正方形矩阵 90 度|设置 1](https://www.geeksforgeeks.org/inplace-rotate-square-matrix-by-90-degrees/) 整篇文章！**