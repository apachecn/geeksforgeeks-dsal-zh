# Python 计数器|在二进制矩阵中查找重复行

> 原文:[https://www . geeksforgeeks . org/python-counter-find-duplicate-row-binary-matrix/](https://www.geeksforgeeks.org/python-counter-find-duplicate-rows-binary-matrix/)

给定一个元素只有 0 和 1 的二进制矩阵，我们需要打印与矩阵中已经存在的行重复的行。

示例:

```
Input : [[1, 1, 0, 1, 0, 1],
         [0, 0, 1, 0, 0, 1],
         [1, 0, 1, 1, 0, 0],
         [1, 1, 0, 1, 0, 1],
         [0, 0, 1, 0, 0, 1],
         [0, 0, 1, 0, 0, 1]]

Output : (1, 1, 0, 1, 0, 1)
         (0, 0, 1, 0, 0, 1)

```

这个问题我们已经有了解决方案，请参考[在二进制矩阵](https://www.geeksforgeeks.org/find-duplicate-rows-binary-matrix/)链接中查找重复行。我们可以使用[计数器()](https://www.geeksforgeeks.org/counters-in-python-set-1/)方法在 Python 中非常快速地解决这个问题。方法很简单，

1.  使用计数器方法创建一个字典，将行作为关键字，将其频率作为值。
2.  现在完全遍历字典，打印频率大于 1 的所有行。

```
# Function to find duplicate rows in a binary matrix
from collections import Counter

def duplicate(input):

     # since lists are unhasable for counter method
     # because lists are mutable so first we will cast
     # each row (list) into tuple
     input = map(tuple,input)

     # now create dictionary
     freqDict = Counter(input)

     # print all rows having frequency greater than 1
     for (row,freq) in freqDict.items():
          if freq>1:
              print (row)

# Driver program
if __name__ == "__main__":
    input = [[1, 1, 0, 1, 0, 1],
            [0, 0, 1, 0, 0, 1],
            [1, 0, 1, 1, 0, 0],
            [1, 1, 0, 1, 0, 1],
            [0, 0, 1, 0, 0, 1],
            [0, 0, 1, 0, 0, 1]]
    duplicate(input)
```

输出:

```
(1, 1, 0, 1, 0, 1)
(0, 0, 1, 0, 0, 1)

```