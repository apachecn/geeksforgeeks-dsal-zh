# Python 映射函数查找最大 1 个数的行

> 原文:[https://www . geesforgeks . org/python-map-function-find-row-maximum-number-1s/](https://www.geeksforgeeks.org/python-map-function-find-row-maximum-number-1s/)

给定一个布尔 2D 数组，其中每行都被排序。找到最大 1 个数的行。

示例:

```
Example
Input: matrix =
[[0, 1, 1, 1],
 [0, 0, 1, 1],
 [1, 1, 1, 1],  
 [0, 0, 0, 0]]
Output: 2

```

这个问题我们已经有解决方案了，请参考[找到最大 1 个数的行](https://www.geeksforgeeks.org/find-the-row-with-maximum-number-1s/)。我们可以使用 [map()](https://www.geeksforgeeks.org/sum-2d-array-python-using-map-function/) 函数在 python 中快速解决这个问题。方法很简单，找出每一行中所有 1 的和，然后在列表中打印最大和的**索引**，因为具有最大 1 的行也将具有最大和。

```
# Function to find the row with maximum number of 1's
def maxOnes(input):

     # map sum function on each row of
     # given matrix
     # it will return list of sum of all one's
     # in each row, then find index of maximum element
     result = list(map(sum,input))
     print (result.index(max(result)))

# Driver program
if __name__ == "__main__":
    input = [[0, 1, 1, 1],[0, 0, 1, 1],[1, 1, 1, 1],[0, 0, 0, 0]]
    maxOnes(input)
```

**复杂度:** O(M*N)

输出:

```
2

```