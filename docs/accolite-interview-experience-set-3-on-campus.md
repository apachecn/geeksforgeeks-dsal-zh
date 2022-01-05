# Accolite 面试体验|第三集(校内)

> 原文:[https://www . geesforgeks . org/accolite-面试-体验-设置-校园 3/](https://www.geeksforgeeks.org/accolite-interview-experience-set-3-on-campus/)

**笔试 MCQ**
30 分钟内有 20 道选择题要做，大部分技术题来自[极客 squiz](http://geeksquiz.com/) ，一个血缘关系题和一个简单概率题。

没有负面标记。

**论文编码轮**
第一轮 MCQ 有 21 名学生入围，这一轮我们被要求在 1 小时内写出 3 道题的代码(仅限函数)。
Q1。给你一个 MxN 大小的矩阵，矩阵中唯一可能的值是
0–代表空位置
1–代表一个新鲜苹果
2–代表一个腐烂的苹果
一个腐烂的苹果在 1 个单位时间内将所有的新鲜苹果转化为与其相邻的腐烂苹果。给定一个输入矩阵，你必须计算出所有新鲜苹果腐烂的时间。还要确定是否所有的新鲜苹果都能在有限的时间内腐烂。(20 分)

输入
2 1 0 2 1
1 0 1 2 1
1 0 2 1

1 个时间单位后，矩阵将转换为
2 2 0 2 2
2 0 2 2
1 0 0 2 2

2 个时间单位后，矩阵将看起来像
2 2 0 2 2
2 0 2 2 2
2 0 0 2 2

因此输出应该是 2 个时间单位。(相邻的定义仅包括左、右、下和上单元格，不包括对角线单元格)

Q2。[给你一棵二叉树，你需要找出二叉树任意 2 个叶节点之间的最大路径和](https://practice.geeksforgeeks.org/problems/maximum-path-sum/1)(最大路径和可以通过也可以不通过树根)。在规定时间内完成(20 分钟)

Q3。[给你一个未排序的整数数组，你需要找出其中是否存在多数元素](https://practice.geeksforgeeks.org/problems/majority-element/0)。(多数元素是在大小为 n 的数组中出现 n/2 次以上的元素)。
这一轮的结果在深夜宣布。大约有 7 到 8 名学生被要求参加面对面的面试。我是第一个被叫到的人，F2F 回合从晚上 11 点 30 分开始，到早上 5 点结束:-p 我很幸运在凌晨 1 点 15 分左右有空😀

**脸 2 脸圆 1**
Q1。我无法完成第一题(烂苹果)的论文编码。她(面试官)让我纠正其中的问题。我是借助 MxN 为 visited[][] matrix 提供的额外空间做到的。她说就地做。我将矩阵值修改为 3、4 等。🙂

Q2。[从单链表的最后一个元素中找出第 5 个](https://practice.geeksforgeeks.org/problems/nth-node-from-end-of-linked-list/1)。首先，我给出了一个解决方案，需要两次遍历。她说只用一次遍历就可以完成。我通过拿两个指针并保持它们之间 5 个节点的距离来做到这一点。Q3。给你一个字符串，例如，如果输入字符串是“我是 abc xyz”。输出应该是修改后的字符串“xyz abc am I”。这将在适当的时间就地完成。

Q4。[给你一个由正整数和负整数组成的未排序数组。你需要在 O(n)时间内找出子阵的最大和。您需要找到开始和结束索引以及总和。](https://practice.geeksforgeeks.org/problems/kadanes-algorithm/0)

Q5。给你一个 BST 和两个密钥 k1 和 k2。你需要[迭代找出两个键](https://practice.geeksforgeeks.org/problems/lowest-common-ancestor-in-a-binary-tree/1)的最低共同祖先。我建议的解决方案是将路径存储在一个向量中，并找到根到 k1 和根 t k2 路径中键值的第一个不匹配。

**面对面第二轮**T2】Q1。以纸编码圆烂苹果问题为例，建议一些算法，允许你改变烂苹果和新鲜苹果的位置，使得结果矩阵将最少数量的新鲜苹果转换成烂苹果。我提出了一种方法，首先统计腐烂和新鲜苹果的数量，从(0，0)位置开始将所有新鲜苹果排列在一个子矩阵中，类似地从(N-1，M-1)位置开始将所有腐烂苹果排列在子矩阵中。他对这种方法很满意

Q2。给你一个有 3 部电梯的电梯系统，你必须建议一些算法，其中一个人在某个 x 楼层等待并按下向上或向下按钮的时间应该等待最少的时间，并且电梯内的人也不应该等待太长时间到达他的目的地楼层。

Q3。问了一些关于什么是语言符号的一般性问题。什么是语法和产生式规则。然后他让我检查某种语言的给定代码在语法上是否正确。为您提供了该语言的有效标记集和符号表。

Q4。给你一个存储字符或单词的文本文件。建议一些压缩文件的方法，这样总有一些空间压缩是可能的。

我建议使用 trie 树，因为所有前缀将共享空间。他说，这种方法取决于输入是否有共同的前缀。
建议其他方式。然后我说，我们可以使用霍夫曼编码，将最小的代码分配给文件中最频繁的单词，等等。他又说这种方法也取决于你的输入是否有频繁出现的单词。

然后我建议，既然所有的字符都可以用 8 位或 1 字节来表示。我们可以对上一个字符和下一个字符进行异或运算，并将其存储在当前字符位置。这样，我就能在编码文件中始终获得 n/2 的大小缩减。这个想法类似于[https://www . geeksforgeeks . org/xor-link-list-a-memory-efficient-double-link-list-set-1/](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-1/)

他很满意，这是我第二轮 F2F 的结束。他告诉我去睡一会儿，因为明天早上你将和我们的技术经理进行一次 skype 面试，然后是人力资源部。

**第三轮(Skype)**
Q1。他让我先定义 NP 和 NP 难问题，然后是自动机和正则语言的定义。然后他问我是不是正则表达式。

Q2。他和我分享了一个谷歌文档，给了我一个像 abab*(a|b)这样的正则表达式和一个输入字符串 s，我需要写一个代码来检查给定的输入字符串是否可以从这个正则表达式中生成。返回布尔值真或假。我在 5 分钟内就把它编码好了

Q3。[给你一个 N 元树和值 k。如果存在一些和= k 的根到叶路径，你需要返回真，否则返回假。我用递归和 O(n)时间做了这件事。](https://practice.geeksforgeeks.org/problems/root-to-leaf-path-sum/1)

他告诉我，你将在某个时候进行最后一轮人力资源面试。我知道我进展顺利，因为他似乎对我的回答相当满意。

**最后一轮**
那是我等了几个小时的一轮😀
她(人力资源)首先问了一些一般性的问题，比如告诉我你自己以及你的人生目标。你的爱好是什么？我告诉她我热爱艺术和工艺。她问我如果明天是她的生日，我会给她做什么:-p 她很友好，很好说话。🙂我好像不是在和人力资源部说话，更像是在和朋友说话。她问我喜欢雅高什么，为什么想加入公司什么的。最后我们讨论了雅高的薪资水平和工作文化。

如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

## 相关实践问题

[XOR Linked List](https://practice.geeksforgeeks.org/problems/xor-linked-list/1)[Maximum path sum](https://practice.geeksforgeeks.org/problems/maximum-path-sum/1)[Majority Element](https://practice.geeksforgeeks.org/problems/majority-element/0)[n’th node from end of linked list](https://practice.geeksforgeeks.org/problems/nth-node-from-end-of-linked-list/1)[Lowest Common Ancestor in a BST](https://practice.geeksforgeeks.org/problems/lowest-common-ancestor-in-a-bst/1)[Reverse words in a given string](https://practice.geeksforgeeks.org/problems/reverse-words-in-a-given-string/0)[Kadane’s Algorithm](https://practice.geeksforgeeks.org/problems/kadanes-algorithm/0)[Rotten Oranges](https://practice.geeksforgeeks.org/problems/rotten-oranges/0)[All Practice Problems for Accolite](https://practice.geeksforgeeks.org/company/Accolite/) !