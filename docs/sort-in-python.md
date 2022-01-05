# Python 中的排序()

> 原文:[https://www.geeksforgeeks.org/sort-in-python/](https://www.geeksforgeeks.org/sort-in-python/)

像 [C++ sort()](https://www.geeksforgeeks.org/sort-c-stl/) 、 [Java sort()](https://www.geeksforgeeks.org/arrays-sort-in-java-with-examples/) 等语言一样，python 也提供了内置的函数来进行排序。

排序功能可用于按升序和降序对列表进行排序。

按升序对列表进行排序。

**语法**

> #这将按升序对给定列表进行排序。
> #根据传递的参数返回排序列表。
> 列表 _ 名称.排序()

这个函数可以用来对整数、浮点数、字符串等进行排序。

```
# List of Integers
numbers = [1, 3, 4, 2]

# Sorting list of Integers
numbers.sort()

print(numbers)

# List of Floating point numbers
decimalnumber = [2.01, 2.00, 3.67, 3.28, 1.68]

# Sorting list of Floating point numbers
decimalnumber.sort()

print(decimalnumber)

# List of strings
words = ["Geeks", "For", "Geeks"]

# Sorting list of strings
words.sort()

print(words)
```

输出:

```
[1, 2, 3, 4]
[1.68, 2.0, 2.01, 3.28, 3.67]
['For', 'Geeks', 'Geeks']

```

按降序排列列表。

**语法**

```
list_name.sort(reverse=True)
This will sort the given list in descending order.

```

```
# List of Integers
numbers = [1, 3, 4, 2]

# Sorting list of Integers
numbers.sort(reverse=True)

print(numbers)

# List of Floating point numbers
decimalnumber = [2.01, 2.00, 3.67, 3.28, 1.68]

# Sorting list of Floating point numbers
decimalnumber.sort(reverse=True)

print(decimalnumber)

# List of strings
words = ["Geeks", "For", "Geeks"]

# Sorting list of strings
words.sort(reverse=True)

print(words)
```

输出:

```
[4, 3, 2, 1]
[3.67, 3.28, 2.01, 2.0, 1.68]
['Geeks', 'Geeks', 'For']
```

**语法:**

> list _ name . sort()–它按升序排序
> list _ name . sort(reverse = True)–它按降序排序
> list_name.sort(key=…，reverse =…)–它根据用户的选择进行排序

**参数:**
默认情况下，sort()不需要任何额外的参数。但是，它有两个可选参数:

> **反转**–如果为真，列表按降序排序
> **键**–用作排序比较的键的功能

```
# Python program to demonstrate sorting by user's
# choice

# function to return the second element of the
# two elements passed as the parameter
def sortSecond(val):
    return val[1] 

# list1 to demonstrate the use of sorting 
# using using second key 
list1 = [(1,2),(3,3),(1,1)]

# sorts the array in ascending according to 
# second element
list1.sort(key=sortSecond) 
print(list1)

# sorts the array in descending according to
# second element
list1.sort(key=sortSecond,reverse=True)
print(list1)
```

**输出:**

```
[(1, 1), (1, 2), (3, 3)]
[(3, 3), (1, 2), (1, 1)]

```

更多 Python 排序文章请参考 [Python 排序](https://www.geeksforgeeks.org/tag/python-sort/)文章。

感谢[奋斗者](https://auth.geeksforgeeks.org/user/Striver/articles)对此话题的投入。