# 在 Python 中生成集合的所有排列

> 原文:[https://www . geeksforgeeks . org/生成所有排列的 python 列表/](https://www.geeksforgeeks.org/generate-all-the-permutation-of-a-list-in-python/)

排列是按特定顺序排列物体。物体的排列顺序非常重要。一组 n 个元素上的排列数由 n 给出！。比如有 2 个！= 2*1 = 2 个{1，2}排列，即{1，2}和{2，1}以及 3！= 3*2*1 = 6 个{1，2，3}排列，即{1，2，3}、{1，3，2}、{2，1，3}、{2，3，1}、{3，1，2}和{3，2，1}。

**方法 1(回溯)**
我们可以使用这里讨论的基于回溯的递归解决方案。
**方法二**
思路是一个一个提取所有元素，放在第一个位置，对剩余列表重复。

## 计算机编程语言

```
# Python function to print permutations of a given list
def permutation(lst):

    # If lst is empty then there are no permutations
    if len(lst) == 0:
        return []

    # If there is only one element in lst then, only
    # one permutation is possible
    if len(lst) == 1:
        return [lst]

    # Find the permutations for lst if there are
    # more than 1 characters

    l = [] # empty list that will store current permutation

    # Iterate the input(lst) and calculate the permutation
    for i in range(len(lst)):
       m = lst[i]

       # Extract lst[i] or m from the list.  remLst is
       # remaining list
       remLst = lst[:i] + lst[i+1:]

       # Generating all permutations where m is first
       # element
       for p in permutation(remLst):
           l.append([m] + p)
    return l

# Driver program to test above function
data = list('123')
for p in permutation(data):
    print p
```

输出:

```
['1', '2', '3']
['1', '3', '2']
['2', '1', '3']
['2', '3', '1']
['3', '1', '2']
['3', '2', '1']
```

**方法 3(直接函数)**
我们可以通过简单地使用 itertools 库中内置的置换函数来实现。寻找排列是最短的技术。

## 计算机编程语言

```
from itertools import permutations
l = list(permutations(range(1, 4)))
print l
```

输出:

```
[(1, 2, 3), (1, 3, 2), (2, 1, 3), (2, 3, 1), (3, 1, 2), (3, 2, 1)] 
```

本文由 **Arpit Agarwal** 供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息