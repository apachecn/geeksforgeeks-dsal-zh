# 统计未按递增顺序排序的列数

> 原文:[https://www . geeksforgeeks . org/未按递增顺序排序的列数/](https://www.geeksforgeeks.org/count-no-of-columns-that-are-not-sorted-in-increasing-order/)

给定一个由 N 个相同长度的小写字母字符串组成的数组 A。任务是查找未按递增顺序排序的列数。

**例:**

```
Input: A = ["cba", "dah", "ghi"]
Output: 1
2nd Column ["b", "a", "h"] is not sorted in increasing order.

Input: A = ["zyx", "wvu", "tsr"]
Output: 3
All columns are not sorted in increasing order.

```

**方法:**逐个遍历每一列，检查下一个元素是否大于同一列中的前一个元素。如果不是，将**列数**增加 1，并继续遍历，直到遍历完所有列。打印**计数的值**。

```
# function to count the unsorted columns
def countUnsorted(A):

    countOfCol = 0

    for col in zip(*A):
        if any(col[i] > col[i + 1] for i in range(len(col) - 1)):
            countOfCol += 1

    return countOfCol

# Driver code
A = ["cba", "daf", "ghi"]
print(countUnsorted(A))
```

**输出:**

```
1

```