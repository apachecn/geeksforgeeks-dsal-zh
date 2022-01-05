# 亚马逊采访|第 69 集(针对 SDE-1)

> 原文:[https://www . geesforgeks . org/Amazon-interview-set-69-SDE-1/](https://www.geeksforgeeks.org/amazon-interview-set-69-sde-1/)

**在线编码回合:**

1.  查找给定字符串是否包含重复项
2.  给定一个 BST，求树的最大 N 个元素
3.  [给定一个 BST，将其转换为双向链表](https://practice.geeksforgeeks.org/problems/binary-tree-to-dll/1)
4.  [将二维矩阵旋转 90 度](https://practice.geeksforgeeks.org/problems/rotate-by-90-degree/0)

**电话面试 1:**

1.  [滑动窗口问题](https://practice.geeksforgeeks.org/problems/maximum-of-all-subarrays-of-size-k/0):给定一个较大的整数缓冲区/数组(比如大小 x)，现在给定一个窗口大小(比如 n)和一个数字(比如 k)。Windows 从 1 <sup>st</sup> 元素开始，一直向右移动一个元素。目标是找到每个窗口中存在的最小 k 个数。
2.  给定一个二叉树，每个节点都有一个整数数据，目标是使用这个二进制创建一个新的双向链表，这样 DLL 中的每个节点都有二叉树中节点的垂直和。DLL 中节点的顺序应与二叉树的垂直节点一样从左到右，即最左边的垂直和应为 DLL 中的 1 <sup>st</sup> 节点，最右边的垂直和应为 DLL 中的最后一个节点。

**电话面试 2:**

1.  [给定二叉树的根和指向该树中任意随机节点的指针，目标是打印距离给定随机节点‘k’距离的所有节点。](https://practice.geeksforgeeks.org/problems/nodes-at-given-distance-in-binary-tree/1)

**面对面**:**T3】**

***注*** **:** 时间和空间的复杂性分别在以下每个问题中进行了讨论。对于每个问题，我都被要求优化算法，然后为其编写工作代码。每一轮都讨论了当前的项目。

**第一轮:**

1.  [给定一个矩阵(m*n)，源(0，0) &目的地(m-1，n-1)(即最后一个单元格)，找出从源到达目的地的途径总数。](https://practice.geeksforgeeks.org/problems/count-all-possible-paths-from-top-left-to-bottom-right/0)
2.  给定一棵二叉树，将术语“完全路径和”定义为从根到叶的路径中节点值的和；现在给定一个值‘k’，我们必须找到 k 重路径并修剪二叉树，即修剪/删除完整路径和小于 k 的节点。

**第 2 轮(经理轮):**

对一个问题的彻底讨论:如果我是一家销售某种产品的公司的老板。那么，我应该如何将我的数据存储在数据库中，以便当任何分析师来询问任何信息时，我可以向他提供最精确的值。它主要包括哪些数据应该存储以及如何存储。

1.  [给定两个已排序的数组，创建最终的已排序数组。](https://practice.geeksforgeeks.org/problems/merge-two-sorted-arrays/0)后来，这个问题被扩展为，现在我们有“m”个大小为“n”的排序数组，现在有效地创建一个最终数组。对该方法的复杂性(时间和空间)进行了大量讨论。

**第三轮:**

1.  [给定一个二叉树，其中左边孩子的旅行成本为‘1’，右边孩子的旅行成本为‘2’。现在，给定树的根和值“k”，求距根距离/成本为“k”的节点总数。](https://practice.geeksforgeeks.org/problems/maximum-path-sum/1)
2.  [给定一个大小为‘n’的未排序整数(仅正值)数组，我们可以组成一个由两个或三个元素组成的组，该组中所有元素的和应该是 3 的倍数。求这样可以生成的最大组数](https://practice.geeksforgeeks.org/problems/possible-groups/0)。
3.  [给定一个整数数组，求到达数组末尾的最小跳转次数。](https://practice.geeksforgeeks.org/problems/minimum-number-of-jumps/0)

**第 4 轮:**

1.  [给定一个 BST，将其就地转换为双向链表。](https://practice.geeksforgeeks.org/problems/binary-tree-to-dll/1) *注* :我们不需要创建新的数据结构，也就是说，我们需要修改给定 BST 中的链接/指针。
2.  问题是这样提出的:[给定一条街的房子(一排房子)，每栋房子里面都有一定数量的钱；现在有一个小偷打算偷这笔钱，但他有一个限制/规则，他不能偷/抢两个相邻的房子。找到他能抢的最大金额](https://practice.geeksforgeeks.org/problems/max-sum-without-adjacents/0)。

*注* :我没有面对任何一轮 HR，尽管每轮都有人问我变化的原因。

总的来说，这是一次很棒的经历，面试官真的很酷，给了我足够的时间去思考和编码，有时会暗示我是否被卡住了。

GeeksforGeeks 对我的准备工作非常有帮助。

如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

[All Practice Problems for Amazon](https://practice.geeksforgeeks.org/company/Amazon/) !

## 相关实践问题

[Maximum money](https://practice.geeksforgeeks.org/problems/maximum-money/0)