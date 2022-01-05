# Python |按任意键递增排序元组

> 原文:[https://www . geesforgeks . org/python-sort-元组-递增-order-key/](https://www.geeksforgeeks.org/python-sort-tuples-increasing-order-key/)

给定一个元组，按元组中的任意键按升序对元组列表进行排序。

**例:**

```
Input : tuple = [(2, 5), (1, 2), (4, 4), (2, 3)] 
            m = 0
Output : [(1, 2), (2, 3), (2, 5), (4, 4)]
Explanation: Sorted using the 0th index key.

Input :  [(23, 45, 20), (25, 44, 39), (89, 40, 23)]
         m = 2
Output : Sorted: [(23, 45, 20), (89, 40, 23), (25, 44, 39)] 
Explanation: Sorted using the 2nd index key

```

给定元组，我们需要根据任何给定的关键字对它们进行排序。这可以使用 sorted()函数来完成，在该函数中，我们使用**键=last** 对它们进行排序，并将 last 存储为键索引，根据该索引我们必须对给定的元组进行排序。

*下面是上面方法的 Python 实现:*

```
# Python code to sort a list of tuples 
# according to given key.

# get the last key.
def last(n):
    return n[m]  

# function to sort the tuple   
def sort(tuples):

    # We pass used defined function last
    # as a parameter. 
    return sorted(tuples, key = last)

# driver code  
a = [(23, 45, 20), (25, 44, 39), (89, 40, 23)]
m = 2
print("Sorted:"),
print(sort(a))
```

输出:

```
Sorted: [(23, 45, 20), (89, 40, 23), (25, 44, 39)] 

```