# Python |按绝对差排序数组

> 原文:[https://www . geesforgeks . org/python-按绝对差排序数组/](https://www.geeksforgeeks.org/python-sort-an-array-according-to-absolute-difference/)

给定一个由 **N** 个不同元素组成的数组和一个数值 **val** ，根据与 **val** 的绝对差值重新排列数组元素，即差值最小的元素优先，依此类推。此外，如果两个或多个元素具有相等的差异，则应保持数组元素的顺序。

示例:

> **输入:** val = 6，a = [7，12，2，4，8，0]
> **输出:** a = [7 4 8 2 12 0]
> 
> 说明:
> 考虑每个数组元素与‘val’
> 的绝对差 7–6 = 1
> 12-6 = 6
> 2–6 = 4(ABS)
> 4–6 = 2(ABS)
> 8–6 = 2
> 0–6 = 6(ABS)
> 于是，根据得到的差，对数组差进行递增排序，得到
> 1、2、2、4、6、6，它们对应的数组元素为 7、4、8、2、6
> 
> **输入:** val = -2，a = [5，2，0，-4]
> **输出:** a = [0 -4 2 5]

**方法:**通常 Python 中的字典只能保存一个键对应的一个值。但是在这个问题中，我们可能需要为一个特定的键存储多个值。显然，简单的字典是不能用的，我们需要一个类似于 C++ 中[的多重映射。因此，这里使用默认字典，它在 Python 中作为 Multimap 工作。以下是解决问题的步骤。](https://www.geeksforgeeks.org/multimap-associative-containers-the-c-standard-template-library-stl/)

*   将值存储在字典中，其中 key 是“val”和数组元素(即 abs(val-a[i])之间的绝对差值，value 是数组元素(即 a[i])
*   在 multiimap 中，这些值已经按照关键字进行了排序，因为它在内部实现了自平衡二进制搜索树。
*   通过逐个存储字典元素来更新原始数组的值。

下面是上述方法的实现。

```
# Python program to sort the array
# according to a value val 

# Using Default dictionary (works as Multimap in Python)
from collections import defaultdict
def rearrange(a, n, val):
     # initialize Default dictionary
     dict = defaultdict(list)  

     # Store values in dictionary (i.e. multimap) where,
     # key: absolute difference between 'val' 
     # and array elements (i.e. abs(val-a[i])) and
     # value: array elements (i.e. a[i])
     for i in range(0, n):
          dict[abs(val-a[i])].append(a[i])

     index = 0  

     # Update the values of original array 
     # by storing the dictionary elements one by one
     for i in dict:

          pos = 0
          while (pos<len(dict[i])):
               a[index]= dict[i][pos]
               index+= 1
               pos+= 1

# Driver code     
a =[7, 12, 2, 4, 8, 0]
val = 6

# len(a) gives the length of the list
rearrange(a, len(a), val)

# print the modified final list
for i in a:
     print(i, end =' ')  
```

**Output:**

```
7 4 8 2 12 0

```

**时间复杂度:**O(N * Log N)
T3】辅助空间: O(N)

**替代方法:**使用大小为 n*2 的二维矩阵，将绝对差值和索引存储在(I，0)和(I，1)处。对二维矩阵进行排序。根据内置的矩阵属性，矩阵根据第一个元素进行排序，如果第一个元素相同，则根据第二个元素进行排序。获取索引并相应地打印数组元素。

下面是上述方法的实现。

```
def printsorted(a, n, val):

    # declare a 2-D matrix 
    b =[[0 for x in range(2)] for y in range(n)]

    for i in range(0, n): 
        b[i][0] = abs(a[i]-val) 
        b[i][1] = i

    b.sort() 

    for i in range(0, n): 
        print a[b[i][1]],

a = [7, 12, 2, 4, 8, 0]
n = len(a) 
val = 6
printsorted(a, n, val) 
```

**Output:**

```
7 4 8 2 12 0

```

**时间复杂度:**O(N * Log N)
T3】辅助空间: O(N)