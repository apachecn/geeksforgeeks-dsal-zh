# Python 中的 heapq，打印行和列排序矩阵中按排序顺序排列的所有元素

> 原文:[https://www . geesforgeks . org/heapq-python-print-elements-sorted-order-row-column-wise-sorted-matrix/](https://www.geeksforgeeks.org/heapq-python-print-elements-sorted-order-row-column-wise-sorted-matrix/)

给定一个 n×n 矩阵，其中每一行和每一列按非递减顺序排序。按排序顺序打印矩阵的所有元素。

示例:

```
Input : mat= [[10, 20, 30, 40],
              [15, 25, 35, 45],
              [27, 29, 37, 48],
              [32, 33, 39, 50]]

Output : Elements of matrix in sorted order
         [10, 15, 20, 25, 27, 29, 30, 32, 
          33, 35, 37, 39, 40, 45, 48, 50]

```

此问题已有解决方案请参考链接。我们将在 python 中使用[合并两个排序数组](https://www.geeksforgeeks.org/merge-two-sorted-arrays-python-using-heapq/)的相同方法，使用 [**heapq 模块**](https://www.geeksforgeeks.org/heap-queue-or-heapq-in-python/) 来解决这个问题。

```
# Function to print all elements in sorted order 
# from row and column wise sorted matrix 
from heapq import merge 

def sortedMatrix(mat): 

    # initialize result variable with first row of matrix 
    result=mat[0] 

    # now traverse through complete matrix 
    # after first row and merge each row with 
    # result one by one 
    # after last operation result will contain 
    # list of sorted elements of matrix 
    for row in mat[1:]: 
        result=list(merge(result,row)) 

    return result 

if __name__ == "__main__": 
    mat = [[10, 20, 30, 40],
           [15, 25, 35, 45],
           [27, 29, 37, 48],
           [32, 33, 39, 50]] 
    print ('Elements of matrix in sorted order')
    print (sortedMatrix(mat)) 
```

输出:

```
Elements of matrix in sorted order
[10, 15, 20, 25, 27, 29, 30, 32, 33, 35, 37, 39, 40, 45, 48, 50]

```

本文由 [**沙莎克·米什拉(古卢)**](https://auth.geeksforgeeks.org/profile.php?user=Shashank Mishra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。