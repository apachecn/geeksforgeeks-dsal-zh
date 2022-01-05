# 矩阵中包含重复值的行数和列数

> 原文:[https://www . geesforgeks . org/包含重复值的矩阵中的行数和列数/](https://www.geeksforgeeks.org/number-of-rows-and-columns-in-a-matrix-that-contain-repeated-values/)

给定一个只包含 1 到 N 之间的整数的 **N x N** [正方形矩阵](https://www.geeksforgeeks.org/how-to-access-elements-of-a-square-matrix/) **arr[][]** ，任务是计算矩阵中包含重复值的行数和列数。

**示例:**

> **输入:** N = 4，arr[][] = {{1，2，3，4}，{2，1，4，3}，{3，4，1，2}，{4，3，2，1}}
> **输出:** 0 0
> **解释:**
> 没有一行或一列包含重复值。
> 
> **输入:** N = 4，arr[][]= {{2，2，2，2}，{2，3，2，3}，{2，2，2，3}，{2，2，2，2}}
> **输出:** 4 4
> **解释:**
> 在方阵的每一列每一行中，值都是重复的。
> 因此，行和列的总数都是 4。

**方法:**想法是使用 [NumPy 库](https://www.geeksforgeeks.org/numpy-in-python-set-1-introduction/)。

*   制作正方形矩阵中每行每列的 [NumPy 数组](https://www.geeksforgeeks.org/numpy-array-creation/)。
*   找出独特元素的长度。
*   如果长度等于 **N** ，则在该特定行或列中不存在重复值。

下面是上述方法的实现:

```
# Python program to count the number of 
# rows and columns in a square matrix 
# that contain repeated values

import numpy as np

# Function to count the number of rows
# and number of columns that contain 
# repeated values in a square matrix.
def repeated_val(N, matrix):
    column = 0
    row = 0
    for i in range (N):

    # For every row, an array is formed. 
    # The length of the unique elements 
    # is calculated, which if not equal 
    # to 'N' then the row has repeated values.
        if (len(np.unique(np.array(matrix[i])))!= N):
            row += 1 

    # For every column, an array is formed.
    # The length of the unique elements 
    # is calculated, which if not equal 
    # to N then the column has repeated values.
    for j in range (N):
        if (len(np.unique(np.array([m[j] for m in matrix])))!= N):
            column += 1

    # Returning the count of 
    # rows and columns
    return row, column

# Driver code
if __name__ == '__main__': 

    N = 3
    matrix = [ [ 2, 1, 3 ], [ 1, 3, 2 ], [ 1, 2, 3 ] ]

    print(repeated_val(N, matrix))  
```

**Output:**

```
(0, 2)

```