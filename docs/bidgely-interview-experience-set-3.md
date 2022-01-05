# Bidgely 面试体验|第三集

> 原文:[https://www . geeksforgeeks . org/bid gely-面试-经验-设置-3/](https://www.geeksforgeeks.org/bidgely-interview-experience-set-3/)

**资质和编码回合**

共有 12 个问题(10 个一般能力倾向+ 2 个编码问题)，时间为 1 小时。这是在 hackerrank 进行的在线测试。

正确答案的评分方案为+5，一般能力倾向的评分方案为-2。

能力倾向测验考查速度与时间、A.P、G.P、概率、排列组合等一般数学概念的知识。

其中一些问题是

1.有一组包含 30 个数字的字母组合。前 11 个数字的总和等于前 19 个数字的总和。所以，求字母组合中 30 个术语的总和

2.给定三个边(a，b，c)，使得 a+b+c=1。这三条边形成三角形的概率有多大？

3.两列速度分别为 30 公里/小时和 40 公里/小时、方向相反的火车在一点相遇。碰撞前 1 分钟他们之间的距离是多少？

两个编码问题是:-

1.**硬币兑换问题**-给定一个 N 值，当我们无限量供应 50 派萨和 1 卢比时，我们可以进行兑换的方式有多少种不同。这个问题类似于:

[动态编程|第 7 集(硬币兑换)–极客 forGeeks](https://www.geeksforgeeks.org/dynamic-programming-set-7-coin-change/)

2.给定两个字符串:-可以将第一个字符串转换为另一个字符串，但条件是

如果字符位于奇数位置，您可以将该字符与给定第一个字符串中仅位于奇数位置的字符进行交换。

如果字符位于偶数位置，您可以将该字符与给定第一个字符串中偶数位置的字符交换。

您不能自行插入或删除任何字符。

因此，如果可以将第一个字符串转换为另一个字符串，则必须打印“是”或“否”

例如

1.

第一串:-极客

第二个字符串:-用于

输出:- **否**(因为字符串的长度不同)

2.

第一弦:-斯基格

第二弦:-极客

输出:- **是**

解释:-

位于第一位置(奇数位置)的“s”可以与位于第五位置(奇数位置)的“g”交换

类似地，位于第二位置(偶数)的“k”可以与位于第四位置(偶数位置)的“e”交换

完成以上两个步骤后，我们可以将第一个字符串转换为另一个字符串

3.

第一个字符串:-abd

第二个字符串:-错误

输出:- **否**

解释:-

位于第一个位置(奇数位置)的“a”不能与位于第二个位置(偶数位置)的“b”交换。它只能与“d”(第三个位置-奇数)交换

4.

第一个字符串:-abcde

第二个字符串:- cdeba

输出:**-是**

解释:-

位于第 1 个位置(奇数位置)的“a”可以与位于第 3 个位置(奇数位置)的“c”交换

位于第二位置(偶数位置)的“b”可以与位于第四位置(偶数位置)的“d”交换

字符串已变成 cdabe

现在我们可以用 e 交换 a，然后我们把第一个字符串转换成另一个字符串

我能够解决 4 个智能和编码问题，我和另外 12 名学生一起被选中参加面试。

**面试第 1 轮:-**

*   Tell me about yourself (about technical skills)
*   Given a set of numbers and a number K, check whether the sum of any pair can be evenly divided by K (in the most effective way)

例如 int arr[]=[1，2，3，4，5]和 k = 6；

所以(5，1)和可以被 k 整除。

**面试第二轮:-**

在这里，他问了我在在线测试中解决编码问题的方法。

下一个问题是:-给定一个包含正数和负数的数组。你可以把数字排成一对，也可以不要管它。当你组成一对时，你必须把组成一对的数字相乘。一旦你做了，你必须总结它。

**目标**:-你必须得到最大和。

例如，如果 A[]={-1，0，1}

所以为了得到最大和，排列将是{-1，0}和{1}。所以答案是(-1*0)+1 ={1}。

如果 A[]={-1，9，4，5，-4，7}

成对队形将为{-1，-4} {9，7} {4，5}

Ans : (-1*-4)+(9*7)+(4*5)=87。

如果 A[]={8，7，9}

成对排列将是{9，8}，{7} Ans: (9*8)+7=79

然后他给了我一个难题。

该拼图与

1.  [The puzzles are exactly the same 1 | Use two identical wires](https://www.geeksforgeeks.org/puzzle-1-how-to-measure-45-minutes-using-two-identical-wires/)

测量 45 分钟

**面试最后一轮:-电话面试(30 分钟)**

这是最后一轮，包括技术问题和人力资源问题。一些技术问题包括:-

1.  He asked me to explain my DBMS project.
2.  What bugs are there in your project? How did you solve them?
3.  What is **hashmap** ? What are its advantages? Why is it faster to search in HashMap?
4.  Why is there multiple inheritance of **but not** in Java?
5.  How does Java manage deadlock?
6.  What is the set of **reflection** and **in Java?**
7.  How to create **thread** with java?
8.  What is the difference between a thread and a runnable interface? Which is better? Why?
9.  How to find the intermediate elements in the linked list in a single iteration?
10.  Which is better, linked list or array, and which scenario is better?
11.  What is **synchronization** ? How to achieve synchronization? Explain how to achieve synchronization?

**HR 提问**分别是:-

1.  Why do you think this role suits you best?
2.  When **developer** is available, what is the demand for **tester** ?
3.  Differences between testers and developers.
4.  Name your 3 strengths and 3 weaknesses.
5.  What to do at the weekend?
6.  How many friends do you have in college?
7.  How do you prioritize your work?

**比德格利**

9.  What's your passion?
10.  What is your career ambition?
11.  Where will you look at yourself three years later?
12.  What are your expectations of the company?

如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。