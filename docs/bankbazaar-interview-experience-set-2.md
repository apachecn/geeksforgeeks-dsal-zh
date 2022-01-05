# 银行芭莎面试体验|第二集

> 原文:[https://www . geesforgeks . org/bank bazaar-面试-体验-设置-2/](https://www.geeksforgeeks.org/bankbazaar-interview-experience-set-2/)

我采访了 BankBazaar.com。他们的过程是在线编码测试，然后是电话和 f2f 面试。

**笔试**
写这道题的人正在经历人生中最糟糕的阶段。但是，幸运的是，他在上一次编程活动中赢得了一些现金。
现在为了让女朋友觉得特别，他想给她买一些巧克力。如上所述，他过得不好，所以他想尽可能少花钱。
考虑到这一点，他决定和她玩一个游戏。游戏规则如下:
1)1 型代表的巧克力有 N 种..N
2)他会以某种随机的顺序将它们排成一排
3)现在她(当然是他的女朋友)必须选择一个索引，比如 I，然后她会得到索引 j 处的所有巧克力，这样 j > i 和 j 处的巧克力类型就严格地小于索引 I 处的巧克力类型

他认为他的女朋友没有那么聪明，肯定不会选择最佳指数，但他想知道，如果她碰巧选择了最佳指数，那么他将不得不买多少巧克力。

输入:
第一行包含 N，然后下一行包含 N 个空格分隔的整数。

输出:
单个整数，这就是答案。

约束:
1 = N = 105

1 <=a[i]<=10^5 1 2 3 4 5 6 7 8 9 10 sample input (plaintext link) output explanation if she chooses i="3," then all the elements in right of have type less than 10, hence ans is 7\. none other case can get more chocolates 2) forgot 2nd question. **第 1 轮电话
给定一棵二叉树，找出违反 BST 属性的对。
在 BST 中，左子树中的每个元素必须小于右子树中的每个元素**

```
eg:                              50
                            30         60
			20      25  10     40 
```

 **在上面的树中，违反 BST 属性的对是(20，10)，(30，25)，(30，10)，(25，10)，(50，10)和(60，40)。
问题的预期时间复杂度是 O(nlogn)时间？
解决方法:按顺序遍历。将有序遍历存储在数组中。找到对属性

起作用的配对，我这一轮没有清除，所以没有 f2f 面试问题。

如果你喜欢 GeeksforGeeks 并愿意投稿，也可以写一篇文章，把文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

[银行集市所有练习题](https://practice.geeksforgeeks.org/company/BankBazaar/)！**=a[i]<=10^5>