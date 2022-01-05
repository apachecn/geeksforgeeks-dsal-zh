# 在 Python 中用逗号作为 1000 分隔符打印数字

> 原文:[https://www . geesforgeks . org/print-number-逗号-1000-分隔符-python/](https://www.geeksforgeeks.org/print-number-commas-1000-separators-python/)

在这个程序中，我们需要以国际位置值格式打印给定整数的输出，并在右边适当的位置放置逗号。

示例:

```
Input : 1000000
Output : 1,000,000

Input : 1000
Output : 1,000

```

Python 2.7 中引入了将{}与 format()函数一起使用，并且通常在字符串格式中代替“%”使用。
<font size="+0.5">**句法**</font>

```
" ".format()

```

示例:

```
Input  : print ('{0}, {1}, {2}'.format('a', 'b', 'c'))
Output : a, b, c

Input :  print ('{2}, {0}, {1}'.format('a', 'b', 'c'))
Output : c, a, b

```

这里，我们使用了“{:，}”和 format()函数，从左边开始每隔一千个位置添加逗号。这是在 Python3 中引入的，它会在编写以下语法时自动添加一个逗号。

```
def place_value(number):
    return ("{:,}".format(number))

print(place_value(1000000))
```

输出:

```
1,000,000

```

本文由 [**【钦莫伊蕾恩卡】**](https://www.linkedin.com/in/lenkachinmoy/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。