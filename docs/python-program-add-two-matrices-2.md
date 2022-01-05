# Python 程序添加两个矩阵

> 原文:[https://www . geesforgeks . org/python-program-add-two-matrix-2/](https://www.geeksforgeeks.org/python-program-add-two-matrices-2/)

**先决条件:**[Python 中的数组](https://www.geeksforgeeks.org/array-python-set-1-introduction-functions/)、[循环](https://www.geeksforgeeks.org/loops-in-python/)、[列表理解](https://www.geeksforgeeks.org/python-list-comprehension-and-slicing/)

程序计算两个矩阵的和，然后用 Python 打印出来。我们可以在 Python 中以各种方式执行矩阵加法。这里有两个。
示例:

```
Input :
 X= [[1,2,3],
    [4 ,5,6],
    [7 ,8,9]]

Y = [[9,8,7],
    [6,5,4],
    [3,2,1]]

Output :
 result= [[10,10,10],
         [10,10,10],
         [10,10,10]]

```

**使用嵌套[循环](https://www.geeksforgeeks.org/loops-in-python/)**

```
# Program to add two matrices using nested loop

X = [[1,2,3],
    [4 ,5,6],
    [7 ,8,9]]

Y = [[9,8,7],
    [6,5,4],
    [3,2,1]]

result = [[0,0,0],
         [0,0,0],
         [0,0,0]]

# iterate through rows
for i in range(len(X)):

   # iterate through columns
   for j in range(len(X[0])):
       result[i][j] = X[i][j] + Y[i][j]

for r in result:
     print(r)
```

输出:

```
[10, 10, 10]
[10, 10, 10]
[10, 10, 10]

```

**解释:-**
在这个程序中，我们使用了嵌套 for 循环来遍历每行每列。在每一点上，我们将两个矩阵中相应的元素相加，并将其存储在结果中。

**使用嵌套[列表理解](https://www.geeksforgeeks.org/python-list-comprehension-and-slicing/)**

这是另一种使用嵌套列表理解进行两个矩阵相加的方法。

```
# Program to add two matrices
# using list comprehension

X = [[1,2,3],
    [4 ,5,6],
    [7 ,8,9]]

Y = [[9,8,7],
    [6,5,4],
    [3,2,1]]

result = [[X[i][j] + Y[i][j]  for j in range(len(X[0]))] for i in range(len(X))]

for r in result:
    print(r)
```

输出:

```
[10, 10, 10]
[10, 10, 10]
[10, 10, 10]

```

**说明:-** 这个程序的输出同上。我们使用嵌套列表理解来迭代矩阵中的每个元素。