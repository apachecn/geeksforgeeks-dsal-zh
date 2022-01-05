# Python |将嵌套列表转换为平面列表

> 原文:[https://www . geesforgeks . org/python-convert-a-nested-list-a-flat-list/](https://www.geeksforgeeks.org/python-convert-a-nested-list-into-a-flat-list/)

任务是将一个嵌套列表转换成 python 中的单个列表，也就是说，无论 python 列表中有多少个嵌套级别，都必须移除所有嵌套，以便将其转换成一个包含最外面括号内所有列表的所有值但内部没有任何括号的列表。

示例:

> 输入:l = [1，2，[3，4，[5，6] ]，7，8，[9，[10] ] ]
> 输出:l = [1，2，3，4，5，6，7，8，9，10]
> 
> 输入:l = [[['item1 '，' item2']]，[['item3 '，' item4']]]
> 输出:l = ['item1 '，' item2 '，' itm3，' item4']

我们使用递归是因为嵌套的层次不能预先确定。

```
# Python code to flat a nested list with
# multiple levels of nesting allowed.

# input list
l = [1, 2, [3, 4, [5, 6]], 7, 8, [9, [10]]]

# output list
output = []

# function used for removing nested 
# lists in python. 
def reemovNestings(l):
    for i in l:
        if type(i) == list:
            reemovNestings(i)
        else:
            output.append(i)

# Driver code
print ('The original list: ', l)
reemovNestings(l)
print ('The list after removing nesting: ', output)
```

**Output:**

```
The original list:  [1, 2, [3, 4, [5, 6]], 7, 8, [9, [10]]]
The list after removing nesting:  [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

```