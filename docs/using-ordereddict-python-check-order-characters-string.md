# Python |使用 ordereddct()

检查字符串中的字符顺序

> 原文:[https://www . geeksforgeeks . org/using-ordereddct-python-check-order-characters-string/](https://www.geeksforgeeks.org/using-ordereddict-python-check-order-characters-string/)

给定输入字符串和模式，检查输入字符串中的字符是否遵循由模式中的字符确定的相同顺序。假设模式中没有任何重复的字符。

示例:

```
Input: 
string = "engineers rock"
pattern = "er";
Output: true
Explanation: 
All 'e' in the input string are before all 'r'.

Input: 
string = "engineers rock"
pattern = "egr";
Output: false
Explanation: 
There are two 'e' after 'g' in the input string.

Input: 
string = "engineers rock"
pattern = "gsr";
Output: false
Explanation:
There are one 'r' before 's' in the input string.

```

对于这个问题，我们已经有了解决方案，请参考[检查字符串是否遵循模式定义的字符顺序|设置 1](https://www.geeksforgeeks.org/check-string-follows-order-characters-defined-pattern-not/) 。这里我们使用[ordereddct()](https://www.geeksforgeeks.org/remove-duplicates-given-string-python/)在 python 中快速解决这个问题。方法很简单，

*   创建一个输入字符串的有序列表，其中仅包含输入字符串的字符作为**键**。
*   现在在模式字符串的开头设置一个指针。
*   现在遍历生成的 OrderedDict 并将关键字与模式字符串的单个字符匹配，如果关键字和字符相互匹配，则将指针增加 1。
*   如果模式的指针到达它的末端，这意味着字符串遵循模式定义的字符顺序，否则不遵循。

```
# Function to check if string follows order of 
# characters defined by a pattern 
from collections import OrderedDict 

def checkOrder(input, pattern): 

    # create empty OrderedDict 
    # output will be like {'a': None,'b': None, 'c': None} 
    dict = OrderedDict.fromkeys(input) 

    # traverse generated OrderedDict parallel with 
    # pattern string to check if order of characters 
    # are same or not 
    ptrlen = 0
    for key,value in dict.items(): 
        if (key == pattern[ptrlen]): 
            ptrlen = ptrlen + 1

        # check if we have traverse complete 
        # pattern string 
        if (ptrlen == (len(pattern))): 
            return 'true'

    # if we come out from for loop that means 
    # order was mismatched 
    return 'false'

# Driver program 
if __name__ == "__main__": 
    input = 'engineers rock'
    pattern = 'egr'
    print (checkOrder(input,pattern)) 
```

输出:

```
true

```

本文由 [**沙莎克·米什拉(古卢)**](https://auth.geeksforgeeks.org/profile.php?user=Shashank Mishra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。