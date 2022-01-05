# Python 中使用列表理解和排序的第 K 个非重复字符

> 原文:[https://www . geeksforgeeks . org/kth-非重复字符-python-使用-列表-理解-ordereddict/](https://www.geeksforgeeks.org/kth-non-repeating-character-python-using-list-comprehension-ordereddict/)

给定一个字符串和一个数字 k，找到字符串中的第 k 个非重复字符。考虑一个包含大量字符和一个小字符集的大输入字符串。如何只对输入字符串做一次遍历就能找到字符？

示例:

```
Input : str = geeksforgeeks, k = 3
Output : r
First non-repeating character is f,
second is o and third is r.

Input : str = geeksforgeeks, k = 2
Output : o

Input : str = geeksforgeeks, k = 4
Output : Less than k non-repeating
         characters in input.

```

此问题已有解决方案请参考链接。我们可以使用[列表理解](https://www.geeksforgeeks.org/python-list-comprehension-and-slicing/)和[排序](https://www.geeksforgeeks.org/remove-duplicates-given-string-python/)在 python 中快速解决这个问题。

```
# Function to find k'th non repeating character 
# in string 
from collections import OrderedDict 

def kthRepeating(input,k): 

    # OrderedDict returns a dictionary data 
        # structure having characters of input 
    # string as keys in the same order they 
        # were inserted and 0 as their default value 
    dict=OrderedDict.fromkeys(input,0) 

    # now traverse input string to calculate 
        # frequency of each character 
    for ch in input: 
        dict[ch]+=1

    # now extract list of all keys whose value 
        # is 1 from dict Ordered Dictionary 
    nonRepeatDict = [key for (key,value) in dict.items() if value==1] 

    # now return (k-1)th character from above list 
    if len(nonRepeatDict) < k: 
        return 'Less than k non-repeating characters in input.' 
    else: 
        return nonRepeatDict[k-1] 

# Driver function 
if __name__ == "__main__": 
    input = "geeksforgeeks"
    k = 3
    print (kthRepeating(input, k)) 
```

输出:

```
r

```

本文由 [**沙莎克·米什拉(古卢)**](https://auth.geeksforgeeks.org/profile.php?user=Shashank Mishra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。