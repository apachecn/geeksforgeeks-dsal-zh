# Python 中的交集 _update()查找 n 个数组中的公共元素

> 原文:[https://www . geesforgeks . org/intersection _ update-python-find-common-elements-n-arrays/](https://www.geeksforgeeks.org/intersection_update-python-find-common-elements-n-arrays/)

我们给出 n 个数组的列表，找出给定数组中所有的公共元素？

示例:

```
Input :  arr = [[1,2,3,4],
               [8,7,3,2],
               [9,2,6,3],
               [5,1,2,3]]
Output :  Common Elements = [2,3]

```

我们可以使用 [Set()数据结构](https://www.geeksforgeeks.org/sets-in-python/)的**交集 _update()方法**在 python 中快速解决这个问题。

**interface _ update()是如何工作的？**

假设我们有两个集合 A 和 B，那么 A . interface _ update(B)操作用集合 A 和 B 中的公共元素更新集合 A，比如 A =集合([1，2，3])和 B =集合([4，2，3])现在取**A . interface _ update(B)**后，集合 A 的值将为[2，3]。语法为 **anySet.intersection_update(可迭代)**。

```
# Function to find common elements in n arrays 
def commonElements(arr): 

    # initialize result with first array as a set 
    result = set(arr[0]) 

    # now iterate through list of arrays starting from 
    # second array and take intersection_update() of 
    # each array with result. Every operation will 
    # update value of result with common values in 
    # result set and intersected set 
    for currSet in arr[1:]: 
        result.intersection_update(currSet) 

    return list(result) 

# Driver code 
if __name__ == "__main__": 
    arr = [[1,2,3,4], [8,7,3,2], [9,2,6,3], [5,1,2,3]] 
    output = commonElements(arr) 
    if len(output) > 0: 
        print ("Common Element = ",output) 
    else: 
        print ('No Common Elements Found')
```

输出:

```
Common Elements = [2,3]

```

本文由 [**沙莎克·米什拉(古卢)**](https://auth.geeksforgeeks.org/profile.php?user=Shashank Mishra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。