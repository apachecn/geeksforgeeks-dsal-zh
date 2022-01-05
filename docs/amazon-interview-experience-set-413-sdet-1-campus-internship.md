# 亚马逊面试体验|第 413 集(SDET-1 校内实习)

> 原文:[https://www . geesforgeks . org/Amazon-面试-体验-设置-413-sdet-1-校园-实习/](https://www.geeksforgeeks.org/amazon-interview-experience-set-413-sdet-1-campus-internship/)

这是亚马逊为实习而开设的泳池校园。

**线上回合:**有 20 道 mcq(+各 1 道)和 2 道编码题(+各 30 道)。MCQ 有更多的网络和 DS 问题。

1.  Given three linked list, add them. [GeeksforGeeks Link](https://practice.geeksforgeeks.org/problems/add-two-numbers-represented-by-linked-lists/1)

    输入将是这种格式

    ```
    1->0->1
    8->9->9
    5
    Output: 1->0->0->5

    ```

    用 python 解决上述问题比 C++容易。我用德格(30/30 分)用 C++解出来的。

2.  [Given an array of size n consisting of positive integers, choose three integers(not necessarily contiguous) such that they are in ascending order and their product is maximum.](https://practice.geeksforgeeks.org/problems/three-great-candidates/0) Input was given in this format.

    ```
    array = {5, 3, 6, 8, 9, 10}
    Output: array = {8, 9, 10}

    ```

    很多人(包括我)忽略了顺位部分，拿到了 20/30 分。后来面试的时候，面试官让我解释我的代码，并告诉了我角落的案例。

    注意:输入和我在两个问题中说的完全一样。这和通常的问题有点不同。首先你必须把字符串分解成整数，然后解决这个问题。

**第二轮:**

1.  [Tic-Tac-Toe](https://practice.geeksforgeeks.org/problems/tic-tac-toe/0')

    这是纸上谈兵。我听说有另一个更简单的解决方案使用幻方。从这一轮中选出了 8 名。

**第三轮:**

技术面试第一轮

面试从最常见的问题“说说你自己”和“项目/实习”开始。那时很少有像什么是二叉树这样的理论问题。什么是二叉查找树？然后是 2 道编码题。

1.  [层级顺序遍历](https://practice.geeksforgeeks.org/problems/level-order-traversal/1)
2.  [Find next greater number with same set of digits](https://practice.geeksforgeeks.org/problems/next-permutation/0)

    不是数字，而是字母串。我的代码有一个错误。面试官给了我一个测试用例，让我测试一下。改变了方法，通过排序来解决。他问是哪种排序，为什么？首先我说合并排序是因为 nlogn 的复杂性。然后我说既然范围小(1-26)，我们可以用计数排序。他问我们是否真的需要排序？然后我说反转第二部分就够了，因为是降序。

**第 4 轮:** 

技术面试第二轮

再谈“说说你自己”和“项目/实习”。

1.  [大小为 k 的所有子阵列的最大值](https://practice.geeksforgeeks.org/problems/maximum-of-all-subarrays-of-size-k/0)

他先问你怎么解决这个问题。给出了 3 种不同的方法。然后最后要求为德奎办法写代码。

DS 和 DAA 问了我几个理论问题。比如什么是算法范式？贪婪和 DP 的区别？关于 Dijkstra(复杂性，贪婪或 dp)的问题。最后给了我一个基于图的问题，问我用哪种算法范式来解决？答案是回溯。

面试官很友好。无论我们在哪里遇到困难，他们都帮助我们给出暗示。

我的建议是阅读 GeeksforGeeks 过去的面试经验，并在 GeeksforGeeks 法官上练习这些问题。复习你的计算机科学基础，如数据结构、算法、网络和数据库。

谢谢 GeeksforGeeks 在我准备面试时给我的帮助。🙂

[All Practice Problems for Amazon](https://practice.geeksforgeeks.org/company/Amazon/) !