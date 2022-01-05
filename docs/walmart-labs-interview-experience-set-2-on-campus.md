# 沃尔玛实验室面试体验|第二集(校内)

> 原文:[https://www . geesforgeks . org/Walmart-labs-interview-experience-set-2-在校园内/](https://www.geeksforgeeks.org/walmart-labs-interview-experience-set-2-on-campus/)

**第一轮(笔试)**

这是一个 90 分钟的在线测试，在黑客帝国上进行。它由 10 道 MCQ 题和 3 道编码题组成。MCQ 的问题包括一般能力倾向问题，与网络、编程等相关的问题，非常简单。

编码问题如下:
**1。**T3【http://www.spoj.com/problems/FARIDA/】T4。问题就是这个。(标准 dp 问题)。
(本题 35 分)。

**2。**给定员工在办公室的到达和离开时间。找到需要的最大椅子数量，这样在任何情况下，员工都不必站立。(30 个问号)。

示例-
输入-
5.00 6.00 7.00
6.30 7.00 8.00
输出-2
类似于[这个](https://practice.geeksforgeeks.org/problems/minimum-platforms/0)。这个问题的主要内容是读取输入，因为事先没有给出员工人数。还要求它检查所有无效输入，并在这些情况下返回-1。

**3。**给定一个 n×m 的 2D 矩阵，该矩阵包含整数。给定一个人的来源位置和目的地位置，找出该人从来源到达目的地的方法数量，满足以下条件-
(一)移动只能是北、南、东或西方向。
(ii)当且仅当一个单元格的值小于当前单元格的值时，一个人才能从一个单元格移动到另一个单元格。(标准 bfs 问题)。(25 个问号)。

**第二轮(技术面试)-**
**1。** [给定一棵二叉树，打印其底视图。](https://practice.geeksforgeeks.org/problems/bottom-view-of-binary-tree/1)她让我把代码写在纸上。

**2。** [给定一个字符数组和一个字典，在这个数组中的任意一个字符后面加上空格，找出可以组成的有效句子的数量。一个有效的句子是所有单词都出现在字典里的句子。](https://practice.geeksforgeeks.org/problems/word-break/0)在纸上写代码。
示例-
输入-猫沙狗
输出- 2(猫沙狗&猫和狗)

**3。**

[给定一个随机整数数组，求其中子序列的最大长度，使子序列的元素连续。](https://practice.geeksforgeeks.org/problems/maximum-sum-subsequence-of-length-k/0)

示例-输入[25，1，26，2，27，3，29，28]
Ans=5(子序列 25，26，27，29，28)

我告诉她 O(n^2 的蛮力方法)和 O(nlogn)解决方案，但她正在寻找 O(n) dp 解决方案。这一轮持续了大约 1 个小时。

**第三轮(技术面试)**–
T3】1。给定一个数组和一只青蛙，在向前的方向上可以有一个从任何索引到任何索引的桥，在向后的方向上可以有一个从任何索引到任何其他索引的隧道。青蛙指数最初为-1。给定一个整数 k，从最多可以跳 k-1 次。即，如果 k=4 并且 frog 最初为-1，则它可以到达小区 0，1，2(最大 3 跳)。一只青蛙在一个有桥或隧道的牢房里着陆时，可以避免使用那个桥或隧道，只呆在那里。找出青蛙到达给定目的地“D”的最小步数。

我将整个问题转换成一个图，其中每个节点都将连接到其下一个 k-1 节点，并且还连接到该节点上的桥或隧道所通向的节点(如果该节点上有桥或隧道的话)，然后应用 BFS。然后他让我在纸上写代码。复杂性-0(n * k)

**2。** [给定一个有循环的链表，检测该循环并返回该循环的起点。](https://practice.geeksforgeeks.org/problems/remove-loop-in-linked-list/1)

**3。**他问我什么是 map(map 的一般概念，不像 c++或 java 那样语言特定)。然后，他告诉我使用基本数据结构设计一个数据结构，这样在 95%的情况下可以在 O(1)中进行搜索，而在 5%的情况下，搜索可能需要 O(1)以上的时间，并且要搜索的元素可以是整数或字符串。

我告诉他用任何方法(乘以素数等)都行。)然后取模 10^6 作为数组的最大尺寸可以是 10^6.然后他问我如何消除由于相同的哈希值而发生的冲突。我告诉他在冲突索引处使用带有平衡 BST 的链接，以便实现最小的复杂性(o(logn))。然后他问我，如果假设在 1 年期间，在上述问题中只需要将 100 个元素存储在数组中并进行搜索，并且在 1 年之后元素变成 10^6，那么在 1 年期间，如果我最初分配 10^6，将会浪费大量内存；他问我会怎么做。我告诉他，最初分配 100 大小数组的内存，然后在 1 年后，分配 10^6 元素的新内存，并将元素从原始数组复制到新数组。这一轮持续了大约 1 个小时。

**第 4 轮(管理轮)—**
这是一个近 10-15 分钟的短回合。面试官让我自我介绍。然后他问我为什么要加入沃尔玛。为什么我不想追求更高的学业，工作和职业的区别，我想要什么，工作还是职业？然后他问我未来 5 年想实现什么。然后他要求对我简历中提到的项目做一个简短的描述。

**第 5 轮(HR 轮)—**
也是近 5-10 分钟的短回合。HR 让我自我介绍。问我的爱好。我提到的一个爱好是阅读 quora 上的新闻提要，所以她问我是否活跃在 quora 上，我在 quora 上关注什么话题。然后她问我为什么想加入沃尔玛，2 年后我在哪里看自己。她问我是否对编程感兴趣，我在哪些网站上参加编码比赛。我提到了 codeforces，codechef，hackerrank。然后她告诉了我在沃尔玛的工作，问我是愿意从事网络开发前端和后端还是物流后端的工作。

**建议:**
准备极客的所有数据结构，最多只问极客的问题。面试时大声思考。每当你遇到任何问题时，面试官都会给你一些提示。

如果你喜欢 GeeksforGeeks 并想投稿，也可以写一篇文章，把文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

[All Practice Problems for Walmart](https://practice.geeksforgeeks.org/company/Walmart/) !

## 相关实践问题

[Bottom View of Binary Tree](https://practice.geeksforgeeks.org/problems/bottom-view-of-binary-tree/1)[Longest consecutive subsequence](https://practice.geeksforgeeks.org/problems/longest-consecutive-subsequence/0)[Word Break](https://practice.geeksforgeeks.org/problems/word-break/0)[Remove loop in Linked List](https://practice.geeksforgeeks.org/problems/remove-loop-in-linked-list/1)[Minimum Platforms](https://practice.geeksforgeeks.org/problems/minimum-platforms/0)