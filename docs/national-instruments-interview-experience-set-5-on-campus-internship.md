# 国家仪器面试体验|第五集(校内–实习)

> 原文:[https://www . geesforgeks . org/national-instruments-interview-experience-set-5-校园-实习/](https://www.geeksforgeeks.org/national-instruments-interview-experience-set-5-on-campus-internship/)

**第 1 轮(书面):**

资格:所有电路分支。

这是一轮笔试，包括能力和技术问题。只有 10 道题，时长 90 分钟。

1 个问题是关于[搜索未排序数组](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array/)的时间复杂度。
2 个问题是关于[递归](https://www.geeksforgeeks.org/tag/recursion/)，即递归调用的次数。
关于分析字符串上给定函数的 1 个问题。
1 个问题是关于[概率](https://www.geeksforgeeks.org/probability-gq/)(两家酒店，比如 A 和 B，从 A 搬到 B 的概率是 2/3，住在 A 的概率是 1/3。从 B 到 A，停留在 B 的概率是 1/2。如果他们每小时做一次决定，如果他们在晚上 7:00 在 A，他们在晚上 10:00 在 B 的概率是多少)。

如果一个[集合](https://www.geeksforgeeks.org/set-operations/)具有元素{1，2，3，4 }。n}。那么它的幂集的元素之和是多少？(例:S = {1，2}。那么幂集就是{{}、{1}、{2}、{1，2}}。总数是 6。

如果一个集合有元素{1，2，3，4，5，6，7，8，9，10}。那么有多少 3 个元素的子集没有连续的元素。

1 个问题是关于[为一个字符串](https://www.geeksforgeeks.org/designing-finite-automata-from-regular-expression-set-1/)设计一个 DFA，以 a 开头，以 c 结尾，其中至少有 b。

1 题有[机器指令](https://www.geeksforgeeks.org/machine-instructions/)。我们必须找出执行给定指令集所需的最小周期数。如果指令是按照给定的顺序执行的。如果指令以随机顺序执行。
1 谜题
这一轮他们不仅看到了答案。他们也会验证你是如何接近的(所以，给你的答案正确的解释。你会有充足的时间。)
350 个中有 32 个入围。我是其中之一。

 **第二轮(编码轮):**
有两个问题。持续 3 小时。

1.长长的问题，我记不太清了。我只举输入输出的例子。它基本上是基于字符串解码。如果 jon2snow3 存在，解码后的字符串将是 jonjonsnowjonjonsnowjonjonsnow。给定一个字符串和一个整数 k，我们已经打印出解码后的字符串中的第 k 个字符
**输入:**
Jon 2 now 3
8
**输出:**
n

2.给定一个数组和一个整数 k，返回其和可被 k 整除的连续[子数组的数量](https://www.geeksforgeeks.org/check-if-an-array-can-be-divided-into-pairs-whose-sum-is-divisible-by-k/)。
输入格式:
n k
T8】n 数组的元素>T5】输入:
4 5
10 0 4 5

输出:
4

解释:{10}、{0}、{10，0}、{5}是总和可被 5 整除的子数组。

请记住，在这里，他们还会检查每个人的代码。我通过了第一题的全部 10 个测试用例和第二题的 11 个测试用例(3 个案例超过了时间限制。1 例失败)
本轮入围 8 例。

**第三轮(技术+ HR 面试):**

说说你自己吧。
然后他们问了我的一个项目。关于我使用过的模块的特性)。
他们让我优化我为第一个问题编写的代码(我已经按照问题中的指定创建了新的字符串)，并为其编写代码。

给定一棵二叉树，找出从根到叶的最大和路径。这个问题，但是他们说树只有正整数。这是在 GeeksforGeeks 这里给出的。为了存储路径，我使用了全局数组。他们问我全局数组的替代方案，我说传递数组作为参数。然后他们问我使用全局变量的缺点。

给定一个单词列表。给定三个操作，找出从源字符串到达目标字符串的最小步骤。基本上这是对[这个](https://www.geeksforgeeks.org/length-of-shortest-chain-to-reach-a-target-word/)问题的一些修改。对于这个问题，我说过我将使用图遍历技术。于是，他们开始询问 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 和 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 什么时候用。

然后他们问我有没有问题。面试官是我们学院的校友，他得到了在北爱尔兰实习的机会。于是，我问他实习经历如何。他在做什么？他说他致力于图像处理新语言的开发。然后我问他目前在做什么。他说他正在研究 LabView。然后另一个面试官问我知不知道 LabView。我说我知道，但是没用过。

如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。