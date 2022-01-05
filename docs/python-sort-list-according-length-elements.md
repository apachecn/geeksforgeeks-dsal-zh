# Python |根据元素长度排序列表

> 原文:[https://www . geesforgeks . org/python-sort-list-resident-length-elements/](https://www.geeksforgeeks.org/python-sort-list-according-length-elements/)

在这个程序中，我们需要接受一个列表，并根据其中元素的长度进行排序。
示例:

```
Input : list = ["rohan", "amy", "sapna", "muhammad",
                "aakash", "raunak", "chinmoy"]
Output : ['amy', 'rohan', 'sapna', 'aakash', 'raunak', 
         'chinmoy', 'muhammad']

Input : list = [["ram", "mohan", "aman"], ["gaurav"], 
                 ["amy", "sima", "ankita", "rinku"]]
Output : [['gaurav'], ['ram', 'mohan', 'aman'], 
          ['amy', 'sima', 'ankita', 'rinku']]

Note: The first example comprises of Strings whose 
length can be calculated. The second example comprises 
of sublists, which is also arranged according to there 
length. 

```

有很多方法可以实现这一点。任何人都可以使用自己的算法技术，但是 Python 为我们提供了各种内置函数来执行这些操作。内置功能包括**排序()**和**排序()**以及关键参数。我们可以通过两种方式来执行这些操作。一种方法是通过创建一个新列表来对列表进行排序，另一种方法是在给定的列表中进行排序，从而节省空间。

**通过创建新列表进行排序的语法是:**

```
sorted_list = sorted(unsorted_list, key=len)
```

```
# Python code to sort a list by creating 
# another list Use of sorted()
def Sorting(lst):
    lst2 = sorted(lst, key=len)
    return lst2

# Driver code
lst = ["rohan", "amy", "sapna", "muhammad", 
       "aakash", "raunak", "chinmoy"]
print(Sorting(lst))
```

**不创建新列表进行排序的语法为:**

```
unsorted_list.sort(key=len)
```

```
# Python code to sort a list without 
# creating another list Use of sort()
def Sorting(lst):
    lst.sort(key=len)
    return lst

# Driver code
lst = ["rohan", "amy", "sapna", "muhammad", 
       "aakash", "raunak", "chinmoy"]
print(Sorting(lst))
```

输出:

```
['amy', 'rohan', 'sapna', 'aakash', 'raunak', 'chinmoy', 'muhammad']

```

**工作:**
Python 在排序时实现的这些关键功能被称为**修饰-排序-非修饰设计模式**。它遵循以下步骤:

1.  列表中的每个元素都被临时替换为一个“修饰”版本，其中包括应用于该元素的键函数的结果。
2.  列表根据键的自然顺序进行排序。
3.  修饰的元素被原始元素替换。

**通过创建新的虚拟列表进行排序的代码为:**

```
import numpy

def Sorting(lst):

    # list for storing the length of each string in list 
    lenlist=[]   
    for x in lst:
         lenlist.append(len(x))     

    # return a list with the index of the sorted
    # items in the list
    sortedindex = numpy.argsort(lenlist)  

    # creating a dummy list where we will place the 
    # word according to the sortedindex list 
    lst2 = ['dummy']*len(lst)   

    # print(sortedindex,lenlist)
    for i in range(len(lst)):    

        # placing element in the lst2 list by taking the
        # value from original list lst where it should belong 
        # in the sorted list by taking its index from sortedindex
        lst2[i] = lst[sortedindex[i]]     

    return lst2

# Driver code
lst = ["rohan", "amy", "sapna", "muhammad", 
       "aakash", "raunak", "chinmoy"]
print(Sorting(lst))
```

输出:

```
['amy', 'rohan', 'sapna', 'aakash', 'raunak', 'chinmoy', 'muhammad']

```

 **参考:** [斯塔科维奇](https://stackoverflow.com/questions/2587402/sorting-python-list-based-on-the-length-of-the-string)