# Python 程序相乘两个矩阵

> 原文:[https://www . geesforgeks . org/python-program-multiple-two-matrix/](https://www.geeksforgeeks.org/python-program-multiply-two-matrices/)

给定两个矩阵，任务是我们必须用 python 创建一个乘法两个矩阵的程序。
示例:

```
Input : X = [[1, 7, 3],
             [3, 5, 6],
             [6, 8, 9]]
       Y = [[1, 1, 1, 2],
           [6, 7, 3, 0],
           [4, 5, 9, 1]]

Output : [55, 65, 49, 5]
         [57, 68, 72, 12]
         [90, 107, 111, 21]
```

**使用简单嵌套循环**
在这个程序中，我们必须使用嵌套 for 循环来遍历每一行和每一列。

## 蟒蛇 3

```
# Program to multiply two matrices using nested loops

# take a 3x3 matrix
A = [[12, 7, 3],
    [4, 5, 6],
    [7, 8, 9]]

# take a 3x4 matrix   
B = [[5, 8, 1, 2],
    [6, 7, 3, 0],
    [4, 5, 9, 1]]

result = [[0, 0, 0, 0],
        [0, 0, 0, 0],
        [0, 0, 0, 0]]

# iterating by row of A
for i in range(len(A)):

    # iterating by column by B
    for j in range(len(B[0])):

        # iterating by rows of B
        for k in range(len(B)):
            result[i][j] += A[i][k] * B[k][j]

for r in result:
    print(r)
```

输出:

```
[114, 160, 60, 27]
[74, 97, 73, 14]
[119, 157, 112, 23]
```

**方法 2:** 利用嵌套列表进行矩阵乘法。我们在 Python 中使用[zip](https://www.geeksforgeeks.org/using-iterations-in-python-effectively/)。

## 蟒蛇 3

```
# Program to multiply two matrices using list comprehension

# take a 3x3 matrix
A = [[12, 7, 3],
    [4, 5, 6],
    [7, 8, 9]]

# take a 3x4 matrix
B = [[5, 8, 1, 2],
    [6, 7, 3, 0],
    [4, 5, 9, 1]]

# result will be 3x4
result = [[sum(a * b for a, b in zip(A_row, B_col))
                        for B_col in zip(*B)]
                                for A_row in A]

for r in result:
    print(r)
```

输出:

```
[114, 160, 60, 27]
[74, 97, 73, 14]
[119, 157, 112, 23]
```

**方法 3:** 矩阵乘法(矢量化实现)。

## 蟒蛇 3

```
# Program to multiply two matrices (vectorized implementation)

# Program to multiply two matrices (vectorized implementation)
import numpy as np
# take a 3x3 matrix
A = [[12, 7, 3],
    [4, 5, 6],
    [7, 8, 9]]

# take a 3x4 matrix
B = [[5, 8, 1, 2],
    [6, 7, 3, 0],
    [4, 5, 9, 1]]

# result will be 3x4

result= [[0,0,0,0],
        [0,0,0,0],
        [0,0,0,0]]

result = np.dot(A,B)

for r in result:
    print(r)
```

输出:

```
[114, 160, 60, 27]
[74, 97, 73, 14]
[119, 157, 112, 23]
```