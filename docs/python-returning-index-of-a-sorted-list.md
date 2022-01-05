# Python |返回排序列表的索引

> 原文:[https://www . geeksforgeeks . org/python-返回排序列表索引/](https://www.geeksforgeeks.org/python-returning-index-of-a-sorted-list/)

在 python 中对列表进行排序，然后按照排序的顺序返回元素的索引。

**示例:**

```
Input  : [2, 3, 1, 4, 5] 
Output : [2, 0, 1, 3, 4]
After sorting list becomes [1, 2, 3, 4, 5] 
and their index as [2, 0, 1, 3, 4]

Input  : [6, 4, 7, 8, 1]
Output : [4, 1, 0, 2, 3]
After sorting the list becomes [1, 4, 6, 7, 8] 
and their index as [4, 1, 0, 2, 3].

```

**方法 1**

```
import numpy
s = numpy.array([2, 3, 1, 4, 5])
sort_index = numpy.argsort(s)
print(sort_index)
```

**输出:**

```
[2, 0, 1, 3, 4]

```

**方法二**

```
s = [2, 3, 1, 4, 5]
li=[]

for i in range(len(s)):
      li.append([s[i],i])
li.sort()
sort_index = []

for x in li:
      sort_index.append(x[1])

print(sort_index)
```

**输出:**

```
[2, 0, 1, 3, 4]
```