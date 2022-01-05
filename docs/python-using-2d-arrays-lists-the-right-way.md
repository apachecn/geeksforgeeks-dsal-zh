# Python |使用 2D 数组/列表的正确方式

> 原文:[https://www . geesforgeks . org/python-using-2d-arrays-list-the-right-way/](https://www.geeksforgeeks.org/python-using-2d-arrays-lists-the-right-way/)

Python 提供了许多创建二维列表/数组的方法。然而，人们必须知道这些方法之间的区别，因为它们会在代码中产生复杂的东西，很难追踪出来。让我们从创建用 0 初始化的一维数组开始。
**法 1a**

## 蟒蛇 3

```
# First method to create a 1 D array
N = 5
arr = [0]*N
print(arr)
```

**Output:** 

```
[0, 0, 0, 0, 0]
```

**方法 1b**T2】

## 蟒蛇 3

```
# Second method to create a 1 D array
N = 5
arr = [0 for i in range(N)]
print(arr)
```

**Output:** 

```
[0, 0, 0, 0, 0]
```