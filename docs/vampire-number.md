# 吸血鬼号

> 原文:[https://www.geeksforgeeks.org/vampire-number/](https://www.geeksforgeeks.org/vampire-number/)

吸血鬼号介绍及其 python 实现。

**简介**
在数学中，吸血鬼数(或真正的吸血鬼数)是一个复合自然数 v，有偶数个数字 n，可以分解成两个整数 x 和 y，每个都有 n/2 个数字，而不是都有尾随零，其中 v 精确地包含从 x 到 y 的所有数字，以任何顺序，计算多重性。 *x 和 y 被称为獠牙。*【来源[维基](https://en.wikipedia.org/wiki/Vampire_number)

示例:

*   1260 是吸血鬼数字，21 和 60 是尖牙，因为 21 × 60 = 1260。
*   126000(可以表示为 21 × 6000 或 210 × 600)不是，因为 21 和 6000 没有正确的长度，并且 210 和 600 都有尾随零

吸血鬼的编号是:
1260，1395，1435，1530，1827，2187，6880，102510，104260，105210，105264，105750，108135，110758，115672，116725，117067，118440，120600

有很多已知的无限多吸血鬼数字的序列遵循一个模式，比如:
1530 = 30×51，150300 = 300×501，15003000 = 3000×5001，…

数字成为吸血鬼数字的条件:

1.  有一对数字。让我们调用数字的个数:n
2.  你可以通过将两个整数 x 和 y 相乘得到这个数，每个整数都有 n/2 个数字。x 和 y 是尖牙。
3.  两个尖牙不能同时以 0 结尾。
4.  数字可以由 x 和 y 的所有数字组成，可以是任何顺序，并且每个数字只能使用一次。

**伪代码**

```
if digitcount is odd return false
if digitcount is 2 return false
for A = each permutation of length digitcount/2 
        selected from all the digits,
  for B = each permutation of the remaining digits,
    if either A or B starts with a zero, continue
    if both A and B end in a zero, continue
    if A*B == the number, return true
```

```
# Python code to check if a number is Vampire
# and printing Vampire numbers upto n using
# it
import itertools as it

# function to get the required fangs of the
# vampire number
def getFangs(num_str):

    # to get all possible orderings of order that
    # is equal to the number of digits of the 
    # vampire number
    num_iter = it.permutations(num_str, len(num_str))

    # creating the possible pairs of number by 
    # brute forcing, then checking the condition 
    # if it satisfies what it takes to be the fangs 
    # of a vampire number
    for num_list in num_iter:

        v = ''.join(num_list)
        x, y = v[:int(len(v)/2)], v[int(len(v)/2):]

        # if numbers have trailing zeroes then skip
        if x[-1] == '0' and y[-1] == '0':
            continue

        # if x * y is equal to the vampire number
        # then return the numbers as its fangs
        if int(x) * int(y) == int(num_str):
            return x,y
    return False

# function to check whether the given number is 
# vampire or not
def isVampire(m_int):

    # converting the vampire number to string
    n_str = str(m_int)

    # if no of digits in the number is odd then 
    # return false
    if len(n_str) % 2 == 1:
        return False

    # getting the fangs of the number
    fangs = getFangs(n_str)
    if not fangs:
        return False
    return True

# main driver program
n = 16000
for test_num in range(n):
    if isVampire(test_num):
        print ("{}".format(test_num), end = ", ")
```

输出:

```
1260, 1395, 1435, 1530, 1827, 2187, 6880, 

```

更多详情请参考[数字爱好者](http://www.numberphile.com/videos/vampire_numbers.html):

**参考文献:**

1.  口红码
2.  [维基百科–吸血鬼号](https://en.wikipedia.org/wiki/Vampire_number)
3.  叠置溢出
4.  [ITER tools 上的 Python 文档](https://docs.python.org/3.6/library/itertools.html#itertools.permutations)

本文由 **[Subhajit Saha](https://www.linkedin.com/in/subhajit-saha-06aa29131/)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。