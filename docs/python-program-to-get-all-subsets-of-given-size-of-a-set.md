# Python 程序获取给定大小的集合的所有子集

> 原文:[https://www . geesforgeks . org/python-program-to-get-所有给定大小集合的子集/](https://www.geeksforgeeks.org/python-program-to-get-all-subsets-of-given-size-of-a-set/)

给定一个集合，编写一个 Python 程序来生成列表中给定集合的所有可能的大小子集 *n* 。

**示例:**

```
Input : {1, 2, 3}, n = 2
Output : [{1, 2}, {1, 3}, {2, 3}]

Input : {1, 2, 3, 4}, n = 3
Output : [{1, 2, 3}, {1, 2, 4}, {1, 3, 4}, {2, 3, 4}]
```

我们已经在本文中使用朴素方法讨论了相同的问题。本文重点介绍了打印给定大小集合的所有子集的 Pythonic 方法。

Python 有**ITER tools . combination(iterable，n)** ，它从输入 ITER able 返回 *n* 长度的元素子序列。这可用于打印集合中给定大小的所有子集。现在，我们有多种选择来使用这个函数。

**代码#1 :**
只需在 itertools.combinations()中将集合作为 ITER tools . combinations()中的参数传递，即可直接获取组合列表。

## 蟒蛇 3

```
# Python Program to Print
# all subsets of given size of a set

import itertools

def findsubsets(s, n):
    return list(itertools.combinations(s, n))

# Driver Code
s = {1, 2, 3}
n = 2

print(findsubsets(s, n))
```

**Output:** 

```
[(1, 2), (1, 3), (2, 3)]
```

**代码#2 :**
我们也可以使用上述方法的替代方法，即*将*设置映射到 itertools.combinations()函数。

## 蟒蛇 3

```
# Python Program to Print
# all subsets of given size of a set

import itertools
from itertools import combinations, chain

def findsubsets(s, n):
    return list(map(set, itertools.combinations(s, n)))

# Driver Code
s = {1, 2, 3}
n = 2

print(findsubsets(s, n))
```

**Output:** 

```
[{1, 2}, {1, 3}, {2, 3}]
```

**代码#3 :**
另一种方法是在 itertools.combinations()函数中使用 for 循环，并将组合集追加到列表中。

## 蟒蛇 3

```
# Python Program to Print
# all subsets of given size of a set

import itertools
# def findsubsets(s, n):
def findsubsets(s, n):
    return [set(i) for i in itertools.combinations(s, n)]

# Driver Code
s = {1, 2, 3, 4}
n = 3

print(findsubsets(s, n))
```

**输出:**

```
[{1, 2, 3}, {1, 2, 4}, {1, 3, 4}, {2, 3, 4}]
```

**代码#4:**

很多时候面试的时候问这个问题，用任何模块回答都比不用回答好。因此，这里是不使用 itertools 模块的解决方案:

## 蟒蛇 3

```
def subsets(numbers):
    if numbers == []:
        return [[]]
    x = subsets(numbers[1:])
    return x + [[numbers[0]] + y for y in x]

# wrapper function
def subsets_of_given_size(numbers, n):
    return [x for x in subsets(numbers) if len(x)==n]

if __name__ == '__main__':
    numbers = [1, 2, 3, 4]
    n = 3
    print(subsets_of_given_size(numbers, n))
```

**输出:**

```
[[2, 3, 4], [1, 3, 4], [1, 2, 4], [1, 2, 3]]
```