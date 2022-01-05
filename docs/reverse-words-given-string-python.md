# 在 Python 中反转给定字符串中的单词

> 原文:[https://www . geesforgeks . org/reverse-words-given-string-python/](https://www.geeksforgeeks.org/reverse-words-given-string-python/)

给我们一个字符串，我们需要反转给定字符串的单词？

示例:

```
Input : str = geeks quiz practice code
Output : str = code practice quiz geeks

```

此问题已有解决方案请参考[给定字符串](https://www.geeksforgeeks.org/reverse-words-in-a-given-string/)链接中的倒字。我们将用 python 解决这个问题。下面给出了解决这个问题应遵循的步骤。

*   使用 python 中字符串数据类型的 [split()](https://www.geeksforgeeks.org/how-to-split-a-string-in-cc-python-and-java/) 方法分隔给定字符串中的每个单词。
*   颠倒单词分隔列表。
*   使用[将每个单词用空格连接后，以字符串形式打印列表中的单词。python 中的 join()](https://www.geeksforgeeks.org/python-string-methods-set-2-len-count-center-ljust-rjust-isalpha-isalnum-isspace-join/) 方法。

```
# Function to reverse words of string 

def rev_sentence(sentence): 

    # first split the string into words 
    words = sentence.split(' ') 

    # then reverse the split string list and join using space 
    reverse_sentence = ' '.join(reversed(words)) 

    # finally return the joined string 
    return reverse_sentence 

if __name__ == "__main__": 
    input = 'geeks quiz practice code'
    print (rev_sentence(input))
```

输出:

```
code practice quiz geeks

```

本文由 [**沙莎克·米什拉(古卢)**](https://auth.geeksforgeeks.org/profile.php?user=Shashank Mishra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。