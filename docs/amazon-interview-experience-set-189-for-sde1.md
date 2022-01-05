# 亚马逊面试体验|第 189 集(针对 SDE-1)

> 原文:[https://www . geesforgeks . org/Amazon-interview-experience-set-189-for-SDE 1/](https://www.geeksforgeeks.org/amazon-interview-experience-set-189-for-sde1/)

最近，我接受了亚马逊 SDE 一号职位的面试。有两个电话回合，接着是 4 个 F2F 回合。

电话第一轮:
——————————
他似乎对面试有点准备不足。他从一些关于当前工作的介绍和知识转移开始，然后创建了一个二叉树，并要求我为该树编写水平顺序、前序、后序和中序遍历。
然后，编码问题接踵而至。

1) [展平多级链表。](https://practice.geeksforgeeks.org/problems/flattening-a-linked-list/1)
第一次进场–>使用队列:T = O(n)，S = O(n)。编码了。
第二种方法–>与极客相同<T4】展平链表 T9:没让我编码。但是这个需要改变数据的结构。

2)展平多级链表，但深度节点先打印。所以，基本上第一个问题类似于 BFS，这个类似于 DFS。使用递归很容易做到。

3)进程与线程。当你输入网址时会发生什么？高级设计。握手协议。HTTPS 议定书等

电话第二轮:
——————————
我必须说采访我的这个人真的很聪明。这一轮是一个多小时，有 3 个问题。

1) [BST 到单链表到位。这个问题稍加修改](https://practice.geeksforgeeks.org/problems/binary-tree-to-dll/1)就编码了。

2)在棋盘上寻找可被车攻击的方块
有一个 NxN 棋盘。棋盘上的每个方块可以是空的，也可以有一个车。我们所知道的车可以水平或垂直攻击。给定一个 2D 矩阵，其中 0 代表一个空方块，1 代表一个车，我们必须用 1 填充矩阵中的所有单元格，1 代表棋盘上任何车都可以攻击的方块。你可以在这里找到这个问题更简单的版本——
[布尔矩阵问题](https://practice.geeksforgeeks.org/problems/boolean-matrix-problem/0)

3) [一排建筑正对着太阳。建筑物的高度是以阵列形式给出的。你必须知道哪些建筑会看到日落。](https://practice.geeksforgeeks.org/problems/buildings-receiving-sunlight/0)这很容易。第一栋建筑肯定会看到日落，对于其余的建筑，只需保持一个可变的 max _ height _ seen _ so _ far，并检查当前建筑的高度。然而，他随后扭曲了这个问题，并问我，如果我从后向前而不是从前到后扫描建筑，我会采取什么方法。我使用了一个堆栈，并应用了类似于“下一个更大的元素”问题中使用的逻辑。

[![Capture](img/25196c82ec9c91bbb9c872bffdc95386.png)](https://media.geeksforgeeks.org/wp-content/uploads/Facing_the_sun.jpg)

F2F R1:
———
从介绍开始。很多关于当前公司、当前工作、当前项目的问题，然后是一个设计问题。

您将如何设计微软 Outlook 的会议邀请功能？将每个会议邀请视为一个对象，并且网络服务器是邀请的存储空间，设计一个数据结构以高效的方式接收邀请并将其发送给用户。必须根据会议时间以有序的方式接收消息对象。我建议使用二叉查找树，并证明了使用这种 DS 的合理性。我给出了一个 O(NlogN)解。然后我被要求编码。我用 C#编码的。

接着是很多人力资源问题。

F2F R2:
———
1)[反转一个数组中的子数组。](https://practice.geeksforgeeks.org/problems/reverse-array-in-groups/0)相当容易。

2) [旋转阵列中的子阵列，其中提供子阵列的开始和结束索引，并且提供“k”，这是要完成的旋转次数。](https://practice.geeksforgeeks.org/problems/rotate-and-delete/0)面试官在这个问题上表现得真的很傻。他想要的只是一个解决方案。他让我一遍又一遍地试运行代码，他并没有真正为这个概念或方法而烦恼。我不认为他能理解我的解决方案，时间上是 0(n)，空间上是 0(1)。

3) [查找链表是否有循环。](https://practice.geeksforgeeks.org/problems/detect-loop-in-linked-list/1)老问题。拿一个快指针和一个慢指针。但得到这个解决方案并不是他的真正动机。他问为什么慢指针一次要移动一个节点，为什么快指针一次要以两个节点的速度移动。在讨论的引导下，我被要求为一个给定的链表找到慢速和快速指针的最佳速度。再次，在讨论的引导下，他问如果给定链表有一个循环，并且给出了循环的大小，我能找到慢速和快速指针的最佳速度吗？

F2F R3:
———
1)与电话会议中 Q3 问的问题相同，唯一的区别是建筑物的高度是在链表中提供的。用 c 编码。然后，面试官扭曲了这个问题，把太阳放在最后一栋建筑的后面(以前太阳放在第一栋建筑的前面)。使用了堆栈。但是，这可以简单地通过反转高度数组并使用为问题的第一部分编写的相同函数来实现。

2)设计一个数据结构来表示组织中员工的层次结构。此外，设计应该是这样的，您可以非常快地检索经理的下属人数(不仅仅是直接下属，还有他手下的所有员工)(O(1)是预期的)。此外，插入新员工和移除员工也应该很快。

我建议使用 n 元哈希表树。另外，使用了一个额外的哈希表，其中键是 employeeId，值是 n 元树中哈希表(或节点)的地址。我的解决方案确实给出了 O(1)中的报告人数，员工的增加和删除是在 O(n)时间内，其中 n 是员工总数。但是没有足够的时间编码。

F2F R4:
——————
这一轮有很多 HR 问题。文化信息。当前项目。他还问了一些编码问题，但他并不真正担心解决方案的最优性。

1) [交换一个 BST 中的两个节点。找到他们](https://practice.geeksforgeeks.org/problems/fixed-two-nodes-of-a-bst/1)。告诉我的方法。没让我编码。

2) [按字典顺序](https://practice.geeksforgeeks.org/problems/permutations-of-a-given-string/0)打印一个字符串的所有排列。编码了。我花了很多时间让他明白代码是正确的😀

如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

[All Practice Problems for Amazon](https://practice.geeksforgeeks.org/company/Amazon/) !