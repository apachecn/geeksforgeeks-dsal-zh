# 在 Python 中根据值对字典列表进行排序的方法–使用 itemgetter

> 原文:[https://www . geesforgeks . org/way-sort-list-dictionary-values-python-using-item getter/](https://www.geeksforgeeks.org/ways-sort-list-dictionaries-values-python-using-itemgetter/)

本节的前一篇文章讨论了使用 lambda 函数按值对字典列表进行排序。

[Python 中按值对字典列表进行排序的方法–使用 lambda 函数](https://www.geeksforgeeks.org/ways-sort-list-dictionaries-values-python-using-lambda-function/)

本文旨在使用 itemgetter 执行此功能，并展示可见的差异。

Itemgetter 可以代替 lambda 函数来实现类似的功能。输出方式与 sorted()和 lambda 相同，但内部实现不同。它获取字典的关键字，并将其转换为元组。它减少了开销，速度更快，效率更高。必须导入“**操作员**”模块才能工作。代码解释如下

```
# Python code demonstrate the working of sorted()
# and itemgetter

# importing "operator" for implementing itemgetter
from operator import itemgetter

# Initializing list of dictionaries
lis = [{ "name" : "Nandini", "age" : 20}, 
{ "name" : "Manjeet", "age" : 20 },
{ "name" : "Nikhil" , "age" : 19 }]

# using sorted and itemgetter to print list sorted by age 
print "The list printed sorting by age: "
print sorted(lis, key=itemgetter('age'))

print ("\r")

# using sorted and itemgetter to print list sorted by both age and name
# notice that "Manjeet" now comes before "Nandini"
print "The list printed sorting by age and name: "
print sorted(lis, key=itemgetter('age', 'name'))

print ("\r")

# using sorted and itemgetter to print list sorted by age in descending order
print "The list printed sorting by age in descending order: "
print sorted(lis, key=itemgetter('age'),reverse = True)
```

输出:

```
The list printed sorting by age: 
[{'age': 19, 'name': 'Nikhil'}, {'age': 20, 'name': 'Nandini'}, {'age': 20, 'name': 'Manjeet'}]

The list printed sorting by age and name: 
[{'age': 19, 'name': 'Nikhil'}, {'age': 20, 'name': 'Manjeet'}, {'age': 20, 'name': 'Nandini'}]

The list printed sorting by age in descending order: 
[{'age': 20, 'name': 'Nandini'}, {'age': 20, 'name': 'Manjeet'}, {'age': 19, 'name': 'Nikhil'}]

```

**Advantages of itemgetter over lambda**

*   **性能** : itemgetter 在时间上下文中比 lambda 函数表现更好。*   **Concise :** : itemgetter looks more concise when accessing multiple values than lambda functions.

    ```

    itemgetter(1,3,4,5)  ---> Looks more concise
    key(s[1], s[2], s[3], s[4]) ---> Looks less concise

    ```

    本文由 **[【曼吉特·辛格】](https://www.facebook.com/manjeet.04.singh)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

    如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。