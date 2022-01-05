# 亚马逊面试体验|第 350 集(针对 SDE I)

> 原文:[https://www . geesforgeks . org/Amazon-面试-体验-设置-350-sde/](https://www.geeksforgeeks.org/amazon-interview-experience-set-350-sde/)

**第 1 轮(编码轮+ MCQs ):**
平台:黑客帝国

1.  [最大 0 翻转子阵列](https://practice.geeksforgeeks.org/problems/flip-bits/0)
2.  [Find a tour that visits all stations](https://practice.geeksforgeeks.org/problems/circular-tour/1)

    测试用例非常弱，任何暴力解决方案都被接受。

基于操作系统、数据库管理系统的 20 个 MCQs。这些问题与极客网站上的问题非常相似。

**第 2 轮(电话面试 1，时长-1 小时):**

1.  [从 k 个列表中找到包含元素的最小范围/](https://practice.geeksforgeeks.org/problems/find-smallest-range-containing-elements-from-k-lists/1)
2.  [对一个 BST 进行删除操作。](https://practice.geeksforgeeks.org/problems/delete-a-node-from-bst/1)

**第 3 轮(电话面试 2，时长–35 分钟):**

1.  [使用链表添加两个多项式](https://practice.geeksforgeeks.org/problems/polynomial-addition/1)
2.  [为了二叉查找树的接班人](https://practice.geeksforgeeks.org/problems/inorder-successor-in-bst/1)

这一轮之后，我被邀请到亚马逊班加罗尔办事处进行现场面试。

**第 4 轮:(F2F，持续时间–45 分钟)**

1.  [相对排序](https://practice.geeksforgeeks.org/problems/relative-sorting/0)
    这个问题可以通过自定义的比较函数结合合并排序来轻松解决，这个我后来想通了。我提出了一个基于 2 个 hashmaps 的不同解决方案。时间复杂度为 0(对数 n)。我的方法有点复杂和冗长，所以面试官没有让我编写代码。
2.  [反转链表。](https://practice.geeksforgeeks.org/problems/reverse-a-linked-list/1)

他让我试运行我的代码，检查了所有角落的案例。

**第 5 轮:(F2F，时长–1 小时，2 名面试官)**

1.  [设计 LRU 缓存。](https://practice.geeksforgeeks.org/problems/lru-cache/1)
    我用无序 _ 地图和双链表设计的。我编写了自己的 DLL 类。之后，他们设计了不同的测试用例，并要求我解释我的代码是如何处理这些用例的。
    他们问了一些关于 hashmap 是如何实现的问题。
2.  [You are given a string and 2 operators ( & , | ). Return the total number of ways in which you can evaluate to true using the given string and operator set.](https://practice.geeksforgeeks.org/problems/boolean-parenthesization/0)

    ```
    Example  : Input : TF
                      Output : 1
                      Input : TFF
                      Output : 2  ( T | F & F ,    T | F | F )

    ```

    我用括号和记忆解决了这个问题。时间复杂性–0(n3)。

    我用三维数组来记忆。

    dp[i][j][0]:使用子串(I，j )
    形成 0 的方式数 dp[i][j][1]:使用子串(I，j)形成 1 的方式数

    面试官强调只使用一个二维数组，所以我必须包括以下预计算来计算长度为 n 的字符串括号的总方法数，比如 F( n)。

    F( n ) = 1 +总和(F(I)* F(n–I))I 从 1 到 n-1 不等。

**第 6 轮(F2F，时长–45 分钟)**
面试官警告我要通知他，以防我已经遇到这些问题。

1.  [到达目的地的最小步数](https://practice.geeksforgeeks.org/problems/minimum-number-of-steps-to-reach-a-given-number/0)。我告诉他我已经用 BFS 解决了这个问题。他让我解释方法，但没有要求编码。
2.  [Minimum number of jumps to reach the end of an array](https://practice.geeksforgeeks.org/problems/minimum-number-of-jumps/0)

    他在期待一个 O ( n)解决方案。我用两点法解决了这个问题。他让我试运行我的代码，并处理数组值为负或零的情况。

3.  [从具有一些公共节点的两个排序链表中构造最大和链表](https://www.geeksforgeeks.org/maximum-sum-linked-list-two-sorted-linked-lists-common-nodes/)

我告诉他这是经典问题，我之前已经解决了。告诉他方法，并处理所有角落的案件。

**第 7 轮(F2F，2 名面试官，时长–30 分钟):**

关于我的项目的详细讨论。一些关于我使用的技术的随机问题。

1.  [用和> = k](https://www.geeksforgeeks.org/remove-all-nodes-which-lie-on-a-path-having-sum-less-than-k/) 移除所有不在任何路径中的节点

如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息

[All Practice Problems for Amazon](https://practice.geeksforgeeks.org/company/Amazon/) !