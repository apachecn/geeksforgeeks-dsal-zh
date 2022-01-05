# Python 程序添加两个矩阵

> 原文:[https://www . geesforgeks . org/python-program-add-two-matrix/](https://www.geeksforgeeks.org/python-program-add-two-matrices/)

目的:编程计算两个矩阵的和，然后用 Python 打印出来。
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

**我们可以在 Python 中通过以下方式进行矩阵加法。**

1.  **用** [**为回路**](https://www.geeksforgeeks.org/loops-in-python/) **:**

## 计算机编程语言

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

**输出:**

```
[10, 10, 10]
[10, 10, 10]
[10, 10, 10]
```

***时间复杂度:**O(len(X)* len(X[0])*

***辅助空间:*** O(len(X) * len(X[0])

**另一种方法:**

1.  **解释:-**
    在这个程序中，我们使用了嵌套 for 循环来遍历每行每列。在每一点上，我们将两个矩阵中相应的元素相加，并将其存储在结果中。
2.  **使用嵌套** [**列表理解**](https://www.geeksforgeeks.org/python-list-comprehension-and-slicing/) **:** 在 Python 中，我们可以将一个矩阵实现为嵌套列表(列表内部的列表)。我们可以将每个元素视为矩阵的一行。

## 计算机编程语言

```
# Program to add two matrices
# using list comprehension

X = [[1,2,3],
    [4 ,5,6],
    [7 ,8,9]]

Y = [[9,8,7],
    [6,5,4],
    [3,2,1]]

result = [[X[i][j] + Y[i][j]  for j in range
(len(X[0]))] for i in range(len(X))]

for r in result:
    print(r)
```

**输出:**

```
[10, 10, 10]
[10, 10, 10]
[10, 10, 10]
```

**另一种方法:**

1.  **说明:-**
    这个程序的输出同上。我们使用嵌套列表理解来迭代矩阵中的每个元素。列表理解允许我们编写简洁的代码，我们必须尝试在 Python 中频繁使用它们。他们很有帮助。
2.  **使用** [**zip()**](https://www.geeksforgeeks.org/using-iterations-in-python-effectively/) **和 sum**

## 计算机编程语言

```
# Program to add two matrices
# using zip()

X = [[1,2,3],
    [4 ,5,6],
    [7 ,8,9]]

Y = [[9,8,7],
    [6,5,4],
    [3,2,1]]

result = [map(sum, zip(*t)) for t in zip(X, Y)]

print(result)
```

**输出:**

```
[[10, 10, 10], [10, 10, 10], [10, 10, 10]]
```

**解释:-**
zip 函数接受矩阵每个元素(列表)的迭代器 I，映射它们，使用 sum()将它们相加，并以映射形式存储它们。

本文由[**aja 0007**](https://auth.geeksforgeeks.org/profile.php?user=ajay0007&list=practice)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现任何不正确的地方，或者你想分享更多关于上述话题的信息，请写评论..