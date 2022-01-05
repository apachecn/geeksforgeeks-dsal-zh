# Python 列表等式|检查两个给定矩阵是否相同的程序

> 原文:[https://www . geesforgeks . org/python-list-equality-program-check-two-给定矩阵-相同/](https://www.geeksforgeeks.org/python-list-equality-program-check-two-given-matrices-identical/)

给我们两个相同阶的方阵。检查两个给定的矩阵是否相同。

示例:

```
Input :     A = [ [1, 1, 1, 1],
                  [2, 2, 2, 2],
                  [3, 3, 3, 3],
                  [4, 4, 4, 4]]

            B = [ [1, 1, 1, 1],
                  [2, 2, 2, 2],
                  [3, 3, 3, 3],
                  [4, 4, 4, 4]]

Output:    Matrices are identical

```

对于这个问题我们已经有了解决方案，请参考 [C 程序检查两个给定的矩阵是否相同](https://www.geeksforgeeks.org/c-program-to-check-if-two-given-matices-are-identical/)链接。在 python 中，任何可迭代对象都是可比较的，因此我们可以借助 **List Equality** 在 python 中快速解决这个问题。

```
# Function to check if two given matrices are identical

def identicalMatrices(A,B):

     if A==B:
        print ('Matrices are identical')
     else:
        print ('Matrices are not identical')

# Driver program
if __name__ == "__main__":
    A = [ [1, 1, 1, 1],
          [2, 2, 2, 2],
          [3, 3, 3, 3],
          [4, 4, 4, 4]]

    B = [ [1, 1, 1, 1],
          [2, 2, 2, 2],
          [3, 3, 3, 3],
          [4, 4, 4, 4]]
    identicalMatrices(A,B)
```

输出:

```
Matrices are identical

```