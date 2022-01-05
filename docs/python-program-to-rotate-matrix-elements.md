# 旋转矩阵元素的 Python 程序

> 原文:[https://www . geeksforgeeks . org/python-旋转矩阵元素程序/](https://www.geeksforgeeks.org/python-program-to-rotate-matrix-elements/)

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

## 计算机编程语言

```
# Python program to rotate a matrix

# Function to rotate a matrix
def rotateMatrix(mat):

    if not len(mat):
        return

    """
        top : starting row index
        bottom : ending row index
        left : starting column index
        right : ending column index
    """

    top = 0
    bottom = len(mat)-1

    left = 0
    right = len(mat[0])-1

    while left < right and top < bottom:

        # Store the first element of next row,
        # this element will replace first element of
        # current row
        prev = mat[top+1][left]

        # Move elements of top row one step right
        for i in range(left, right+1):
            curr = mat[top][i]
            mat[top][i] = prev
            prev = curr

        top += 1

        # Move elements of rightmost column one step downwards
        for i in range(top, bottom+1):
            curr = mat[i][right]
            mat[i][right] = prev
            prev = curr

        right -= 1

        # Move elements of bottom row one step left
        for i in range(right, left-1, -1):
            curr = mat[bottom][i]
            mat[bottom][i] = prev
            prev = curr

        bottom -= 1

        # Move elements of leftmost column one step upwards
        for i in range(bottom, top-1, -1):
            curr = mat[i][left]
            mat[i][left] = prev
            prev = curr

        left += 1

    return mat

# Utility Function
def printMatrix(mat):
    for row in mat:
        print row

# Test case 1
matrix =[ 
            [1,  2,  3,  4 ],
            [5,  6,  7,  8 ],
            [9,  10, 11, 12 ],
            [13, 14, 15, 16 ]  
        ]
# Test case 2
"""
matrix =[
            [1, 2, 3],
            [4, 5, 6],
            [7, 8, 9]
        ]
"""

matrix = rotateMatrix(matrix)
# Print modified matrix
printMatrix(matrix)
```

**输出:**

```
5 1 2 3
9 10 6 4
13 11 7 8
14 15 16 12
```

更多详情请参考[旋转矩阵元素](https://www.geeksforgeeks.org/rotate-matrix-elements/)整篇文章！