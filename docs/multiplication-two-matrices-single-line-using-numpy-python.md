# 使用 Python 中的 Numpy 进行单行两个矩阵的乘法

> 原文:[https://www . geeksforgeeks . org/乘法-两个矩阵-单行-使用-numpy-python/](https://www.geeksforgeeks.org/multiplication-two-matrices-single-line-using-numpy-python/)

矩阵乘法是将两个矩阵作为输入，通过将第一个矩阵的行乘以第二个矩阵的列来产生单个矩阵的运算。在矩阵乘法中，确保第一个矩阵的行数等于第二个矩阵的列数。
**例:**大小为 3×3 的两个矩阵相乘。

```
Input:matrix1 = ([1, 2, 3],
                 [3, 4, 5],
                 [7, 6, 4])
      matrix2 = ([5, 2, 6],
                 [5, 6, 7],
                 [7, 6, 4])

Output : [[36 32 32]
          [70 60 66]
          [93 74 100]]

```

python 中两个矩阵相乘的方法
1。**对循环使用显式:**这是一种简单的矩阵乘法技术，但对于较大的输入数据集，这是一种昂贵的方法。在这里，我们使用嵌套的循环来迭代每行和每列。
如果矩阵 1 是**n×m**矩阵，矩阵 2 是**m×l**矩阵。

```
# input two matrices of size n x m
matrix1 = [[12,7,3],
        [4 ,5,6],
        [7 ,8,9]]
matrix2 = [[5,8,1],
        [6,7,3],
        [4,5,9]]

res = [[0 for x in range(3)] for y in range(3)] 

# explicit for loops
for i in range(len(matrix1)):
    for j in range(len(matrix2[0])):
        for k in range(len(matrix2)):

            # resulted matrix
            res[i][j] += matrix1[i][k] * matrix2[k][j]

print (res)
```

输出:

```
[[114 160  60]
 [ 74  97  73]
 [119 157 112]]

```

在这个程序中，我们使用了嵌套 for 循环来计算结果，它将遍历矩阵的每一行和每一列，最后它将累加结果中乘积的和。
2。**使用 Numpy :** 使用 Numpy 的乘法也称为矢量化，其主要目的是减少或消除程序中 for 循环的显式使用，从而使计算变得更快。
Numpy 是 python 中用于数组处理和操作的包中的构建。对于较大的矩阵运算，我们使用 numpy python 包，它比迭代一种方法快 1000 倍。
有关 Numpy 的详细信息，请访问[链接](https://pypi.python.org/pypi/numpy)

```
# We need install numpy in order to import it
import numpy as np

# input two matrices
mat1 = ([1, 6, 5],[3 ,4, 8],[2, 12, 3])
mat2 = ([3, 4, 6],[5, 6, 7],[6,56, 7])

# This will return dot product
res = np.dot(mat1,mat2)

# print resulted matrix
print(res)
```

输出:

```
[[ 63 320  83]
 [ 77 484 102]
 [ 84 248 117]]

```

**使用 [numpy](https://www.geeksforgeeks.org/numpy-in-python-set-1-introduction/)**

```
# same result will be obtained when we use @ operator 
# as shown below(only in python >3.5)
import numpy as np

# input two matrices
mat1 = ([1, 6, 5],[3 ,4, 8],[2, 12, 3])
mat2 = ([3, 4, 6],[5, 6, 7],[6,56, 7])

# This will return matrix product of two array
res = mat1 @ mat2

# print resulted matrix
print(res)
```

输出:

```
[[ 63 320  83]
 [ 77 484 102]
 [ 84 248 117]]

```

在上面的例子中，我们使用了点积，在数学中，点积是一种代数运算，它取两个大小相等的向量，并返回一个数字。计算结果是将相应的条目相乘，然后将这些乘积相加。

本文由 [**泽拉·夏尔马**](https://auth.geeksforgeeks.org/profile.php?user=dheerajsharma) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。