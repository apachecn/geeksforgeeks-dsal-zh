# Python 中的排列组合

> 原文:[https://www . geesforgeks . org/python 中的排列组合/](https://www.geeksforgeeks.org/permutation-and-combination-in-python/)

Python 提供了找到序列排列和组合的直接方法。这些方法存在于 itertools 包中。

## **排列**

首先导入 itertools 包来实现 python 中的置换方法。此方法将列表作为输入，并返回包含列表形式的所有排列的元组对象列表。

## 蟒蛇 3

```
# A Python program to print all
# permutations using library function
from itertools import permutations

# Get all permutations of [1, 2, 3]
perm = permutations([1, 2, 3])

# Print the obtained permutations
for i in list(perm):
    print (i)
```

**输出:**

```
(1, 2, 3)
(1, 3, 2)
(2, 1, 3)
(2, 3, 1)
(3, 1, 2)
(3, 2, 1)
```

它生成 n！排列如果输入序列的长度是 n.
如果想得到长度为 L 的排列，那么就用这种方法实现。

## 蟒蛇 3

```
# A Python program to print all
# permutations of given length
from itertools import permutations

# Get all permutations of length 2
# and length 2
perm = permutations([1, 2, 3], 2)

# Print the obtained permutations
for i in list(perm):
    print (i)
```

**输出:**

```
(1, 2)
(1, 3)
(2, 1)
(2, 3)
(3, 1)
(3, 2)
```

它生成 nCr * r！如果输入序列的长度为 n，输入参数为 r，则为置换。

## **组合**

该方法以一个列表和一个输入 r 作为输入，返回一个包含列表形式的长度 r 的所有可能组合的元组的对象列表。

## 蟒蛇 3

```
# A Python program to print all
# combinations of given length
from itertools import combinations

# Get all combinations of [1, 2, 3]
# and length 2
comb = combinations([1, 2, 3], 2)

# Print the obtained combinations
for i in list(comb):
    print (i)
```

**输出:**

```
(1, 2)
(1, 3)
(2, 3)
```

1.组合按照输入的字典排序顺序发出。因此，如果输入列表被排序，组合元组将按排序顺序产生。

## 蟒蛇 3

```
# A Python program to print all
# combinations of a given length
from itertools import combinations

# Get all combinations of [1, 2, 3]
# and length 2
comb = combinations([1, 2, 3], 2)

# Print the obtained combinations
for i in list(comb):
    print (i)
```

**输出:**

```
(1, 2)
(1, 3)
(2, 3)
```

2.根据元素的位置，而不是它们的价值，元素被视为唯一的。因此，如果输入元素是唯一的，那么在每个组合中都不会有重复值。

## 蟒蛇 3

```
# A Python program to print all combinations
# of given length with unsorted input.
from itertools import combinations

# Get all combinations of [2, 1, 3]
# and length 2
comb = combinations([2, 1, 3], 2)

# Print the obtained combinations
for i in list(comb):
    print (i)
```

**输出:**

```
(2, 1)
(2, 3)
(1, 3)
```

3.如果我们想把同一个元素组合成同一个元素，那么我们就用 combinations_with_replacement。

## 蟒蛇 3

```
# A Python program to print all combinations
# with an element-to-itself combination is
# also included
from itertools import combinations_with_replacement

# Get all combinations of [1, 2, 3] and length 2
comb = combinations_with_replacement([1, 2, 3], 2)

# Print the obtained combinations
for i in list(comb):
    print (i)
```

**输出:**

```
(1, 1)
(1, 2)
(1, 3)
(2, 2)
(2, 3)
(3, 3) 
```