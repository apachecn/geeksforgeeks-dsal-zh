# 使用集合模块

统计 Python 中数组中所有元素的频率

> 原文:[https://www . geesforgeks . org/count-frequency-elements-array-python-using-collections-module/](https://www.geeksforgeeks.org/count-frequencies-elements-array-python-using-collections-module/)

给定一个可以包含 n 个整数的 n 个整数的未排序数组。计算数组中所有元素的频率。
示例:

```
Input : arr[] = [1, 1, 1, 1, 2, 2, 2, 2, 3, 3, 4, 5, 5]
Output : 1 -> 4
         2 -> 4
         3 -> 2
         4 -> 1
         5 -> 2

```

这个问题可以通过多种方式解决，参考[统计数组](https://www.geeksforgeeks.org/count-frequencies-elements-array-o1-extra-space-time/)链接中所有元素的频率。在 Python 中，我们可以使用[集合](https://docs.python.org/2/library/collections.html#collections.Counter)模块快速解决这个问题。

```
# Function to count frequency of each element 
import collections

# it returns a dictionary data structure whose 
# keys are array elements and values are their 
# corresponding frequencies {1: 4, 2: 4, 3: 2, 
# 5: 2, 4: 1}
def CountFrequency(arr):
    return collections.Counter(arr)  

# Driver function
if __name__ == "__main__":

    arr = [1, 1, 1, 1, 2, 2, 2, 2, 3, 3, 4, 5, 5]
    freq = CountFrequency(arr)

    # iterate dictionary named as freq to print
    # count of each element
    for (key, value) in freq.items():
        print (key, " -> ", value)
```

输出:

```
1 -> 4
2 -> 4
3 -> 2
4 -> 1
5 -> 2

```

**相关文章:**
[使用 Python 中的字典计算列表中的频率](https://www.geeksforgeeks.org/counting-the-frequencies-in-a-list-using-dictionary-in-python/)

本文由 [**沙莎克·米什拉(古卢)**](https://auth.geeksforgeeks.org/profile.php?user=Shashank Mishra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。