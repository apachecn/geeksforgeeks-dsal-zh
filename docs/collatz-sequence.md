# G-Fact 21 |整理序列

> 原文:[https://www.geeksforgeeks.org/collatz-sequence/](https://www.geeksforgeeks.org/collatz-sequence/)

从任意正整数 N 开始，我们将 N 对应的[排序序列](https://en.wikipedia.org/wiki/Collatz_conjecture)定义为由以下运算形成的数:

```
N → N/2 ( if N is even)
N → 3N + 1 (if N is odd)

i.e. If N is even, divide it by 2 to get N/2\. 
If N is odd, multiply it by 3 and add 1 to obtain 3N + 1.

```

 ***推测但尚未证明的是，无论我们从哪个正整数开始；我们总是以 1 结尾。***

比如 10 → 5 → 16 → 8 → 4 → 2 → 1

[整理序列上的一个编码练习题](https://practice.geeksforgeeks.org/problems/maximum-collatz-sequence-length5849/1)

如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。