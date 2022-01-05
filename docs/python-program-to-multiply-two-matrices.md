# Python 程序相乘两个矩阵

> 原文:[https://www . geeksforgeeks . org/python-程序乘二矩阵/](https://www.geeksforgeeks.org/python-program-to-multiply-two-matrices/)

给定两个矩阵，将它们相乘的任务。矩阵可以是正方形或矩形。

**示例:**

```
Input : mat1[][] = {{1, 2}, 
                   {3, 4}}
        mat2[][] = {{1, 1}, 
                    {1, 1}}
Output : {{3, 3}, 
          {7, 7}}
Input : mat1[][] = {{2, 4}, 
                    {3, 4}}
        mat2[][] = {{1, 2}, 
                    {1, 3}}       
Output : {{6, 16}, 
          {7, 18}}
```

![](img/f817ce00b9c904bc4fa28109e9094336.png)

**方阵乘法:**
下面的程序将两个大小为 4*4 的方阵相乘，我们可以针对不同的维度改变 N。

## 蟒蛇 3

```
# 4x4 matrix multiplication using Python3
# Function definition
def matrix_multiplication(M, N):
    # List to store matrix multiplication result
    R = [[0, 0, 0, 0], 
        [0, 0, 0, 0], 
        [0, 0, 0, 0],
        [0, 0, 0, 0]] 

    for i in range(0, 4): 
        for j in range(0, 4):
            for k in range(0, 4): 
                R[i][j] += M[i][k] * N[k][j] 

    for i in range(0, 4): 
        for j in range(0, 4): 
            # if we use print(), by default cursor moves to next line each time, 
            # Now we can explicitly define ending character or sequence passing
            # second parameter as end ="<character or string>"
            # syntax: print(<variable or value to print>, end ="<ending with>")
            # Here space (" ") is used to print a gape after printing 
            # each element of R
            print(R[i][j], end =" ")
        print("
", end ="")

# First matrix. M is a list
M = [[1, 1, 1, 1], 
    [2, 2, 2, 2], 
    [3, 3, 3, 3],
    [4, 4, 4, 4]]

# Second matrix. N is a list
N = [[1, 1, 1, 1], 
    [2, 2, 2, 2], 
    [3, 3, 3, 3],
    [4, 4, 4, 4]] 

# Call matrix_multiplication function
matrix_multiplication(M, N)

# This code is contributed by Santanu
```

**Output**

```
Result matrix is 
10 10 10 10 
20 20 20 20 
30 30 30 30 
40 40 40 40
```

**时间复杂度:** O(n <sup>3</sup> )。它可以使用斯特拉森矩阵乘法进行优化

**辅助空间:** O(n <sup>2</sup> )

**矩形矩阵的乘法:**
我们使用 C 语言中的指针与矩阵相乘。请参考以下帖子作为代码的先决条件。
[如何在 C 中传递一个 2D 阵作为参数？](https://www.geeksforgeeks.org/pass-2d-array-parameter-c/)

## 蟒蛇 3

```
# Python3 program to multiply two
# rectangular matrices

# Multiplies two matrices mat1[][]
# and mat2[][] and prints result.
# (m1) x (m2) and (n1) x (n2) are
# dimensions of given matrices.
def multiply(m1, m2, mat1, 
             n1, n2, mat2):

    res = [[0 for x in range(n2)]
              for y in range (m1)]

    for i in range(m1):
        for j in range(n2): 
            res[i][j] = 0
            for x in range(m2):            
                res[i][j] += (mat1[ i][x] * 
                              mat2[ x][j])

    for i in range(m1):
        for j in range(n2):      
            print (res[i][j], 
                   end = " ")        
        print ()

# Driver code
if __name__ == "__main__":

    mat1 = [[2, 4], [3, 4]]
    mat2 = [[1, 2], [1, 3]]
    m1, m2, n1, n2 = 2, 2, 2, 2

    # Function call
    multiply(m1, m2, mat1, 
             n1, n2, mat2)

# This code is contributed by Chitranayal
```

**Output**

```
6 16 
7 18
```

**时间复杂度:** O(n <sup>3</sup> )。可以使用[斯特拉森的矩阵乘法](https://www.geeksforgeeks.org/strassens-matrix-multiplication/)进行优化

**辅助空间:** O(m1 * n2)

更多详情请参考[两矩阵相乘程序](https://www.geeksforgeeks.org/c-program-multiply-two-matrices/)整篇文章！