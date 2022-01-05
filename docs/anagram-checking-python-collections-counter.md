# 使用集合在 Python 中进行字谜检查。计数器()

> 原文:[https://www . geesforgeks . org/anagram-checking-python-collections-counter/](https://www.geeksforgeeks.org/anagram-checking-python-collections-counter/)

编写一个函数来检查两个给定的字符串是否是彼此的字谜。字符串的字谜是另一个包含相同字符的字符串，只有字符的顺序可以不同。例如，“abcd”和“dabc”是彼此的字谜。

示例:

```
Input : str1 = “abcd”, str2 = “dabc”
Output : True

Input : str1 = “abcf”, str2 = “kabc”
Output : False

```

此问题已有解决方案请参考[检查两个字符串是否为彼此的字谜](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/)链接。我们将使用[集合在 python 中一行解决这个问题。计数器()模块](https://www.geeksforgeeks.org/count-frequencies-elements-array-python-using-collections-module/)。

```
# Python code to check if two strings are
# anagram
from collections import Counter

def anagram(input1, input2):

    # Counter() returns a dictionary data
    # structure which contains characters 
    # of input as key and their frequencies
    # as it's corresponding value
    return Counter(input1) == Counter(input2)

# Driver function
if __name__ == "__main__":
    input1 = 'abcd'
    input2 = 'dcab'
    print anagram(input1, input2)
```

输出:

```
True

```

**python 中字典比较是如何工作的？**
如果我们在 python 中有两个字典数据结构 dict1 = {'a':2，' b':3，' c':1}和 dict2 = {'b':3，' c':1，' a':2}并且我们像 **dict1=dict2** 一样比较它们，那么结果将是 **True** 。在 python 中，普通字典的数据结构不遵循任何键的顺序，当我们比较两个字典时，它会按顺序比较三个检查**键的数量(如果它们不匹配，字典就不相等)**、**键的名称(如果它们不匹配，它们就不相等)**和每个键的**值(它们也必须是' = = ')**。

本文由 [**沙莎克·米什拉(古卢)**](https://auth.geeksforgeeks.org/profile.php?user=Shashank Mishra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。