# 统计矩阵中所有按降序排序的列

> 原文:[https://www . geeksforgeeks . org/count-矩阵中所有按降序排序的列/](https://www.geeksforgeeks.org/count-all-the-columns-in-a-matrix-which-are-sorted-in-descending/)

给定一个矩阵 **mat[][]** ，任务是计算按降序排序的列数。

**示例:**

> **输入:** mat[][] = {{1，3}，{0，2}}
> 输出: 2
> 第一列:1 > 0
> 第二列:3 > 2
> 因此，计数为 2
> 
> **输入:** mat[][] = {{2，2}，{1，3 } }
> T3】输出: 1

**方法:**逐个遍历每一列，检查同一列中的**下一个元素** ≥ **上一个元素**。如果条件对所有可能的元素都有效，那么将**计数**增加 **1** 。遍历完所有列后，打印**计数**。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python3 program to count the number of columns 
# in a matrix that are sorted in descending

# Function to count the number of columns 
# in a matrix that are sorted in descending
def countDescCol(A): 

    countOfCol = 0

    for col in zip(*A): 
        if all(col[i] >= col[i + 1] for i in range(len(col) - 1)): 
            countOfCol += 1

    return countOfCol 

# Driver code 
A = [[1, 3], [0, 2]] 
print(countDescCol(A)) 
```

**Output:**

```
2

```