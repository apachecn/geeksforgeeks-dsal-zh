# 如何在 Python 中对一组值进行排序？

> 原文:[https://www . geesforgeks . org/如何在 python 中对一组值进行排序/](https://www.geeksforgeeks.org/how-to-sort-a-set-of-values-in-python/)

排序意味着以递增或递减的方式排列值集。Python 中有各种方法对值进行排序。我们可以使用各种数据结构存储一组或一组值，如列表、元组、字典，这取决于我们存储的数据。因此，在本文中，我们将讨论一些在 Python 中对数据进行排序的方法和标准。

## 排序()方法

这是 python 中的一个预定义方法，可以对任何类型的对象进行排序。

**语法:**

```
sorted(iterable, key, reverse)
```

在这个方法中，我们传递了 3 个参数，其中 2 个(key 和 reverse)是可选的，第一个参数，即 iterable 可以是任何 iterable 对象。这个方法返回一个排序列表，但不改变原始数据结构。

**例 1:**

## 蟒蛇 3

```
# List
list_of_items = ['g', 'e', 'e', 'k', 's']
print(sorted(list_of_items))

# Tuple
tuple_of_items = ('g', 'e', 'e', 'k', 's')
print(sorted(tuple_of_items))

# String-sorted based on ASCII
# translations
string = "geeks"
print(sorted(string))

# Dictionary
dictionary = {'g': 1, 'e': 2, 'k': 3, 's': 4}
print(sorted(dictionary))

# Set
set_of_values = {'g', 'e', 'e', 'k', 's'}
print(sorted(set_of_values))

# Frozen Set
frozen_set = frozenset(('g', 'e', 'e', 'k', 's'))
print(sorted(frozen_set))
```

**Output**

```
['e', 'e', 'g', 'k', 's']
['e', 'e', 'g', 'k', 's']
['e', 'e', 'g', 'k', 's']
['e', 'g', 'k', 's']
['e', 'g', 'k', 's']
['e', 'g', 'k', 's']
```

**例 2:**

使用预定义函数作为关键参数。因此，第二个参数，即**键**用于通过一些预定义的函数(如 **len()** 或一些用户定义的函数)对给定的数据结构进行排序。它根据传递给键参数的函数对数据结构中的值进行排序。

## 蟒蛇 3

```
# using key parameter with pre-defined
# function i.e. len()

list_of_items = ["apple", "ball", "cat", "dog"]

print("Sorting without key parameter:", sorted(list_of_items))
print("Sorting with len as key parameter:", sorted(list_of_items, key=len))
```

**Output**

```
Sorting without key parameter: ['apple', 'ball', 'cat', 'dog']
Sorting with len as key parameter: ['cat', 'dog', 'ball', 'apple']
```

**例 3:**

对关键参数使用用户定义的函数。

## 蟒蛇 3

```
# using key parameter with user-defined
# function i.e. by_name
# using key parameter with user-defined
# function i.e. by_marks

# here is a list_of_tuples where the first
# item in tuple is the student name and the
# second item is his/her marks
list_of_items = [("Ramesh",56),("Reka",54),("Lasya",32),("Amar",89)]

# defining a user-defined function which returns
# the first item(name)
def by_name(ele):
  return ele[0]

# defining a user-defined function which returns
# the second item(marks)
def by_marks(ele):
  return ele[1]

print("Sorting without key parameter:", sorted(list_of_items))

print("Sorting with by_name as key parameter:",
      sorted(list_of_items, key=by_name))

print("Sorting with by_marks as key parameter:",
      sorted(list_of_items, key=by_marks))
```

**输出**

> 无关键参数排序:[('Amar '，89)、(' Lasya '，32)、(' Ramesh '，56)、(' Reka '，54)]
> 
> 排序以 by_name 为关键参数:[('Amar '，89)、(' Lasya '，32)、(' Ramesh '，56)、(' Reka '，54)]
> 
> 以 by_marks 为关键参数排序:[('Lasya '，32)、(' Reka '，54)、(' Ramesh '，56)、(' Amar '，89)]

**例 4:**

所以**第三个参数是反向的**，用于对可选项进行降序或降序排序。

## 蟒蛇 3

```
# using key parameter reverse

list_of_items = ["geeks","for","geeks"]

print("Sorting without key parameter:",
      sorted(list_of_items))

print("Sorting with len as key parameter:",
      sorted(list_of_items, reverse=True))
```

**Output**

```
Sorting without key parameter: ['for', 'geeks', 'geeks']
Sorting with len as key parameter: ['geeks', 'geeks', 'for']
```