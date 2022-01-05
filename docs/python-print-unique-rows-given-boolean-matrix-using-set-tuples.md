# Python |使用带元组的 Set 打印给定布尔矩阵中的唯一行

> 原文:[https://www . geesforgeks . org/python-print-unique-row-given-boolean-matrix-use-set-元组/](https://www.geeksforgeeks.org/python-print-unique-rows-given-boolean-matrix-using-set-tuples/)

给定一个二进制矩阵，打印给定矩阵的所有唯一行。行打印的顺序无关紧要。

示例:

```
Input:
    mat = [[0, 1, 0, 0, 1],
             [1, 0, 1, 1, 0],
             [0, 1, 0, 0, 1],
             [1, 1, 1, 0, 0]]
Output:
          (1, 1, 1, 0, 0)
          (0, 1, 0, 0, 1)
          (1, 0, 1, 1, 0)

```

这个问题我们已经有了解决方案，请参考链接。我们可以使用[设置数据结构](https://www.geeksforgeeks.org/sets-in-python/)在 python 中快速解决这个问题。方法很简单。

1.  我们给出了布尔值列表，将所有行(列表)放在集合中，因为集合包含唯一的值。
2.  由于列表是集合的不可交换类型，因为它是可变的，这就是为什么我们首先将每一行(列表)转换成[元组](https://www.geeksforgeeks.org/tuples-in-python/)，然后将所有元组放入集合中。
3.  结果集将只包含唯一值元组(行)。

```
# Python program to Print unique rows in a 
# given boolean matrix using Set with tuples

# Function to print unique rows in a given boolean matrix

def uniqueRows(input):

    # convert each row (list) into tuple
    # we are mapping tuple function on each row of 
    # input matrix
    input = map(tuple, input)

    # put all rows in set
    result = set(input)

    # print all unique rows
    for row in list(result):
        print (row)

# Driver program
if __name__ == "__main__":
    input = [[0, 1, 0, 0, 1],
             [1, 0, 1, 1, 0],
             [0, 1, 0, 0, 1],
             [1, 1, 1, 0, 0]]
    uniqueRows(input)
```

输出:

```
(1, 1, 1, 0, 0)
(0, 1, 0, 0, 1)
(1, 0, 1, 1, 0)

```