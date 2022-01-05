# 证明三个连续偶数中至少有一个可以被 6 整除

> 原文:[https://www . geesforgeks . org/prove-至少一个三连的偶数-可整除-6/](https://www.geeksforgeeks.org/prove-atleast-one-three-consecutive-even-numbers-divisible-6/)

给定三个连续的偶数。从数学上证明它们中至少有一个能被 6 整除。

示例:

```
Input : {2, 4, 6}
Output : 6 is divisible by 6

Input : {8, 10, 12}
Output : 12 is divisible by 6

```

**问题来源:** [亚马逊面试体验|第 383 集(校内实习)](https://www.geeksforgeeks.org/amazon-interview-experience-set-383-campus-internship/)

如果你看到任意三个连续的数字，你可以算出其中至少有一个能被 6 整除。
我们可以用数学归纳法进行数学证明。

一个数要能被 6 整除，就应该能被 2 和 3 整除。
因为都是偶数，所以这个数可以被 2 整除。

为了检查数被 3 除的可能性，
考虑下面的证明:

```
Consider 3 consecutive even numbers : 
P(i) = {i, i+2, i+4} (i is divisible by 2)

If one of these three numbers is divisible by 3, 
then their multiplication must be divisible by 3

Base case : i = 2
{2, 4, 6}
Multiplication = (2*4*6) = 3*(2*4*2)
So, it is divisible by 3

For i = n
P(n) = {n, n+2, n+4}
multiplication = (n*(n+2)*(n+4)) 
since P(n) is divisible by 3
means P(n) = n*(n+2)*(n+4) = 3k for positive number k

If the statement holds for i = n, it should hold for
next consecutive even number i.e. i = n + 2

P(n+2) = (n+2)*(n+4)*(n+6)

It can be written as
P(n+2) = n*(n+2)*(n+4) + 6*(n+2)*(n+4)
P(n+2) = P(n) + 6*x
where x = (n+2)*(n+4)

So, P(n+2) = 3*k + 6*x
both the summation elements of P(n+2) are 
divisible by 3, so P(n+2) is divisible by 3

Hence, there is atleast one number among three
even consecutive numbers which is divisible by 6\. 

```

本文由 **[曼德普·辛格](https://github.com/msdeep14)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。