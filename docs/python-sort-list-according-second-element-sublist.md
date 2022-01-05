# Python |根据子列表

中的第二个元素对列表进行排序

> 原文:[https://www . geesforgeks . org/python-sort-list-accord-second-element-sublist/](https://www.geeksforgeeks.org/python-sort-list-according-second-element-sublist/)

在本文中，我们将学习如何根据主列表中子列表的第二个元素对任何列表进行排序。我们将看到两种方法。我们将学习执行这种排序的三种方法。一种是使用冒泡排序，第二种是使用 Sort()方法，最后一种是使用 sorted()方法。在这个程序中，我们已经按照升序对列表进行了排序。
示例:

```
Input : [['rishav', 10], ['akash', 5], ['ram', 20], ['gaurav', 15]]
Output : [['akash', 5], ['rishav', 10], ['gaurav', 15], ['ram', 20]]

Input : [['452', 10], ['256', 5], ['100', 20], ['135', 15]]
Output : [['256', 5], ['452', 10], ['135', 15], ['100', 20]]

```

**方法 1:使用冒泡排序技术**
这里我们使用了[冒泡排序](https://www.geeksforgeeks.org/bubble-sort/)的技术来执行排序。我们已经尝试使用嵌套循环访问子列表的第二个元素。这将执行就地排序方法。时间复杂度类似于冒泡排序(即 O(n^2)

```
# Python code to sort the lists using the second element of sublists
# Inplace way to sort, use of third variable
def Sort(sub_li):
    l = len(sub_li)
    for i in range(0, l):
        for j in range(0, l-i-1):
            if (sub_li[j][1] > sub_li[j + 1][1]):
                tempo = sub_li[j]
                sub_li[j]= sub_li[j + 1]
                sub_li[j + 1]= tempo
    return sub_li

# Driver Code
sub_li =[['rishav', 10], ['akash', 5], ['ram', 20], ['gaurav', 15]]
print(Sort(sub_li))
```

输出:

```
[['akash', 5], ['rishav', 10], ['gaurav', 15], ['ram', 20]]

```

**方法 2:使用 sort()方法进行排序**
通过这种方法进行排序时，元组的实际内容会发生变化，就像前面的方法一样，会执行就地排序的方法。

```
# Python code to sort the tuples using second element 
# of sublist Inplace way to sort using sort()
def Sort(sub_li):

    # reverse = None (Sorts in Ascending order)
    # key is set to sort using second element of 
    # sublist lambda has been used
    sub_li.sort(key = lambda x: x[1])
    return sub_li

# Driver Code
sub_li =[['rishav', 10], ['akash', 5], ['ram', 20], ['gaurav', 15]]
print(Sort(sub_li))
```

输出:

```
[['akash', 5], ['rishav', 10], ['gaurav', 15], ['ram', 20]]

```

**方法 3:使用 sorted()方法进行排序**
Sorted()对列表进行排序，并且总是以排序的方式返回包含元素的列表，而不修改原始序列。它需要三个参数，其中两个是可选的，这里我们尝试使用这三个参数:

1.  Iterable : sequence (list，tuple，string)或 collection (dictionary，set，frozenset)或任何其他需要排序的迭代器。
2.  键(可选) :作为键或排序比较基础的函数。
3.  反向(可选) :要按升序排序，我们可以忽略第三个参数，我们在这个程序中就这样做了。如果设置为真，则可迭代将按相反(降序)顺序排序，默认情况下设置为假。

```
# Python code to sort the tuples using second element 
# of sublist Function to sort using sorted()
def Sort(sub_li):

    # reverse = None (Sorts in Ascending order)
    # key is set to sort using second element of 
    # sublist lambda has been used
    return(sorted(sub_li, key = lambda x: x[1]))    

# Driver Code
sub_li =[['rishav', 10], ['akash', 5], ['ram', 20], ['gaurav', 15]]
print(Sort(sub_li))
```

输出:

```
[['akash', 5], ['rishav', 10], ['gaurav', 15], ['ram', 20]]

```