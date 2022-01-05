# 在 Python 中设置 update()做 n 个数组的并集

> 原文:[https://www . geesforgeks . org/set-update-python-union-n-arrays/](https://www.geeksforgeeks.org/set-update-python-union-n-arrays/)

给我们 n 个任意大小的数组，这些数组可能有共同的元素，我们需要将所有这些数组组合起来，使得每个元素只出现一次，并且元素应该按排序顺序排列？

示例:

```
Input : arr = [[1, 2, 2, 4, 3, 6],
              [5, 1, 3, 4],
              [9, 5, 7, 1],
              [2, 4, 1, 3]]
Output : [1, 2, 3, 4, 5, 6, 7, 9]

```

这个问题的一个**简单解决方案**是创建一个空的**散列**并逐个遍历每个数组，这个散列包含数组列表中每个元素的频率。现在从头开始遍历散列并打印每个非零值的索引。

这里我们使用 python 中 [Set()](https://www.geeksforgeeks.org/sets-in-python/) 数据结构和 **Update()** 方法的属性，非常快速地在 python 中解决了这个问题。

**Update()方法对于 set 是如何工作的？**

**anySet.update(iterable)** ，此方法将名为 **anySet** 的集合与任何给定的 **iterable** 进行并集，并且不像 **union()** 方法那样返回集合的任何浅拷贝，它将结果更新为前缀集，即；**任意集**。

```
# Function to combine n arrays 

def combineAll(input): 

    # cast first array as set and assign it 
    # to variable named as result 
    result = set(input[0]) 

    # now traverse remaining list of arrays  
    # and take it's update with result variable 
    for array in input[1:]: 
        result.update(array) 

    return list(result) 

# Driver program 
if __name__ == "__main__": 
    input = [[1, 2, 2, 4, 3, 6],
             [5, 1, 3, 4],
             [9, 5, 7, 1],
             [2, 4, 1, 3]]  
    print (combineAll(input))
```

输出:

```
[1, 2, 3, 4, 5, 6, 7, 9]

```

本文由 [**沙莎克·米什拉(古卢)**](https://auth.geeksforgeeks.org/profile.php?user=Shashank Mishra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。